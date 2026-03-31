---
title: Blueprints Virtual Machine
tags:
  - Unreal
draft: false
---

La machine virtuelle d'Unreal Engine qui interprète le bytecode généré par le Blueprint Compiler et orchestre les appels vers le code natif C++ via des [[Custom Thunk|thunks]].
## C'est quoi le BPVM ?

Le BPVM (Blueprint Virtual Machine) est l'interpréteur intégré à Unreal Engine. Quand tu compiles un graphe Blueprint, le Blueprint Compiler traduit chaque nœud en une séquence d'**opcodes** et stocke le résultat dans `UFunction::Script`. Au runtime, le BPVM lit ce bytecode opcode par opcode et appelle la fonction native correspondante.

Chaque instruction est interprétée à chaque appel, sans jamais être compilée en code machine. C'est la raison structurelle pour laquelle le code Blueprint est plus lent que le C++ natif.

## Quelques définitions

**Opcode** (operation code) : un simple nombre qui représente une instruction. Le BPVM ne lit pas du texte comme `EX_CallMath`, il lit le byte `0x68`. Le Blueprint Compiler traduit chaque nœud du graphe en une suite de ces nombres. C'est ça le bytecode.

**`GNatives`** : un tableau interne au moteur où chaque index correspond à un opcode et chaque valeur est un pointeur vers la fonction C++ qui sait comment le traiter. Quand le BPVM lit `0x68`, il fait `GNatives[0x68]` et obtient directement la bonne fonction, sans avoir à comparer quoi que ce soit.

## Pipeline d'exécution

Pour chaque nœud du graphe, le BPVM suit ce processus :

1. Lit l'opcode courant depuis `UFunction::Script` et avance l'instruction pointer (`FFrame::Code`)
2. Appelle la fonction correspondante via `GNatives[opcode]`
3. Alloue un bloc mémoire continu (`parms memory`) = somme des `sizeof` de chaque paramètre
4. Empile un `FFrame`, la stack frame de la VM
5. Appelle le thunk natif (`execFunctionName`) via `UFunction::Func`
6. Dépile le `FFrame`, copie la valeur de retour, avance au prochain opcode

## La structure FFrame

`FFrame` est la stack frame de la VM. Elle est créée à chaque appel de fonction Blueprint et contient tout le contexte d'exécution.

|Champ|Type|Rôle|
|---|---|---|
|`FFrame::Object`|`UObject*`|L'instance sur laquelle la fonction est appelée|
|`FFrame::Code`|`uint8*`|Instruction pointer, pointe vers le prochain opcode|
|`FFrame::Locals`|`uint8*`|Bloc mémoire contenant les paramètres (parms memory)|
|`FFrame::MostRecentProperty`|`FProperty*`|Dernier paramètre lu, utile dans les [[Custom Thunk\|CustomThunks]]|
|`FFrame::MostRecentPropertyAddress`|`void*`|Adresse mémoire réelle du dernier paramètre lu|
|`FFrame::PreviousFrame`|`FFrame*`|Frame parente, forme la call stack de la VM|

## La mémoire des paramètres

Avant chaque appel de fonction, le BPVM :

1. Lit le `UFunction*` linké au nœud
2. Alloue un bloc mémoire (`parms memory`) = somme des `sizeof` de chaque paramètre
3. Copie les variables du graphe dans ce bloc
4. Expose ce bloc via `FFrame::Locals` (`uint8*`)

```cpp
// Pour void Function(float A, double B) :
// Locals[0..3]  → float A  (4 octets)
// Locals[4..11] → double B (8 octets)
```

C'est ce bloc que les macros comme `PARAM_PASSED_BY_VAL` traversent, octet par octet.

## Les opcodes principaux

Le bytecode Blueprint est une suite de bytes définis dans `EExprToken` (fichier `Script.h`).

| Opcode                | Rôle                                                     | Valeur |
| --------------------- | -------------------------------------------------------- | ------ |
| `EX_CallMath`         | Appel d'une fonction statique (ex. `UKismetMathLibrary`) | `0x68` |
| `EX_FinalFunction`    | Appel d'une fonction non-virtuelle                       | `0x1C` |
| `EX_VirtualFunction`  | Appel d'une fonction virtuelle (dispatch par nom)        | `0x1B` |
| `EX_LocalVariable`    | Lit une variable locale dans les Locals                  | `0x00` |
| `EX_InstanceVariable` | Lit une variable membre de l'objet courant               | `0x01` |
| `EX_Return`           | Fin d'exécution de la fonction Blueprint                 | `0x04` |
| `EX_Jump`             | Saut inconditionnel (branchement dans le graphe)         | `0x06` |
| `EX_JumpIfNot`        | Saut conditionnel (nœud Branch)                          | `0x07` |
| `EX_EndOfScript`      | Marqueur de fin du bytecode                              | `0x53` |

## ProcessInternal

`UObject::ProcessInternal` est la boucle principale du BPVM. Elle est appelée par `UObject::CallFunction` dès qu'une fonction Blueprint est invoquée.

```cpp
// Simplifié depuis Engine/Source/Runtime/CoreUObject/Private/UObject/ScriptCore.cpp
void UObject::ProcessInternal(FFrame& Stack, void* RESULT_PARAM)
{
    while (*Stack.Code != EX_Return)
    {
        // Lit l'opcode courant et avance Code
        uint8 Opcode = *Stack.Code++;

        // Appelle la fonction qui gère cet opcode
        (this->*GNatives[Opcode])(Stack, RESULT_PARAM);
    }
}
```

## Où le retrouver dans le moteur

`GNatives` et tous les handlers d'**opcodes** y sont définis :
```
Engine/Source/Runtime/CoreUObject/Private/UObject/ScriptCore.cpp
```

Les **opcodes** eux-mêmes sont dans :
```
Engine/Source/Runtime/CoreUObject/Public/UObject/Script.h
```

## Source

Code Source de Unreal
[intaxwashere Custom Thunk](https://gist.github.com/intaxwashere/e9b1f798427686b46beab2521d7efbcf)