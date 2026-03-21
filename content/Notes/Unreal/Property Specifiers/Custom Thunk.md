---
title: Custom Thunk
tags:
  - Unreal
  - PropertySpecifiers
draft: false
---
Quand tu veux contrôler manuellement comment le [[BPVM]] appelle une fonction native, au lieu de laisser l'[[UHT]] générer le pont automatiquement.
## C'est quoi un thunk ?

Un thunk est un pointeur de fonction que le [[BPVM]] peut sauvegarder et appeler plus tard. Chaque nœud du graphe Blueprint correspond à un thunk lié à une fonction native.

Par exemple, le nœud `+` float dans le graphe est lié à `UKismetMathLibrary::AddAdd_Float`. Le BP compiler sérialise un `UFunction*` vide dans le bytecode, et au chargement le moteur le linke vers la bonne fonction native.

## UFUNCTION normal vs CustomThunk

Par défaut, l'[[UHT]] génère automatiquement le thunk pour toute `UFUNCTION(BlueprintCallable)`, tu peux le voir dans les fichiers `.gen.cpp` via le macro `DEFINE_FUNCTION`.

Avec `CustomThunk`, tu dis au moteur de ne pas générer de thunk automatiquement. Tu fournis toi-même le `DEFINE_FUNCTION`, et le moteur se contente de le linker au nœud dans le graphe.

## La mémoire des paramètres

Avant chaque appel de fonction, le [[BPVM]] :

1. Lit le `UFunction*` linké au nœud
2. Alloue un bloc mémoire (`parms memory`) = somme des `sizeof` de chaque paramètre
3. Copie les variables du graphe dans ce bloc
4. Expose ce bloc via `FFrame::Locals` (`uint8*`)

C'est ce bloc que les macros comme `PARAM_PASSED_BY_VAL` traversent, octet par octet.

```cpp
// Pour void Function(float A, double B) :
// Locals[0..3]  → float A  (4 octets)
// Locals[4..11] → double B (8 octets)
```

---

## Structure d'un custom thunk

La fonction déclarée dans le `.h` ne doit **jamais** s'exécuter,  elle sert juste à exposer la signature à l'[[UHT]] .

```cpp
UFUNCTION(BlueprintCallable, CustomThunk)
float Sum(float A, double B) { check(0); return 0; }
```

L'implémentation réelle se fait avec `DEFINE_FUNCTION` :

```cpp
DEFINE_FUNCTION(UYourClass::execSum)
{
    // Lit 4 octets de Locals et avance l'instruction pointer
    PARAM_PASSED_BY_VAL(A, FFloatProperty, float);

    // Lit 8 octets suivants
    PARAM_PASSED_BY_VAL(B, FDoubleProperty, double);

    // Marque la fin du parcours des paramètres
    P_FINISH;

    // Indique au profiler qu'on entre dans du code natif
    P_NATIVE_BEGIN;

    *reinterpret_cast<float*>(RESULT_PARAM) = A + B;

    P_NATIVE_END;
}
```

### Les macros clés

|Macro|Rôle|
|---|---|
|`PARAM_PASSED_BY_VAL(Name, FProp, Type)`|Lit un paramètre depuis `FFrame::Locals`|
|`P_FINISH`|Signale la fin du parcours de la stack|
|`P_NATIVE_BEGIN` / `P_NATIVE_END`|Scope pour le profiler (Insights)|
|`RESULT_PARAM`|`void*` pointant sur la zone de retour|

### Retourner une valeur

cpp

```cpp
// Équivaut à `return MyValue`, mais via la parms memory
*reinterpret_cast<float*>(RESULT_PARAM) = MyValue;
```

Si la fonction ne retourne rien, on n'interagit pas avec `RESULT_PARAM`.

## Où le retrouver dans le moteur

Le plugin **Mover** avec `K2_GetDataFromCollection` en est un bon exemple. La fonction expose un pin sortant dont le type est inconnu à la compilation et est dépendant du type du pin entrant.

Résultat dans le graphe Blueprint : le pin de sortie se met automatiquement à jour en fonction du type branché en entrée.

Un thunk auto-généré ne peut pas faire ça, il reçoit uniquement des copies des paramètres, sans accès à l'adresse mémoire des pins ni à leur type runtime.

## Source 

[intaxwashere Custom Thunk](https://gist.github.com/intaxwashere/e9b1f798427686b46beab2521d7efbcf)