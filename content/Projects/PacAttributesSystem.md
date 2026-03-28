---
title: PacAttributeSystem
description: describes the project in a few words.
engine: Unity
language: C#
role:
team:
duration:
year: 2026
github: https://github.com/Stanpac/StanpacPackages.git?path=Packages/com.stanpac.pacattributessystem
itch: ""
build: ""
trailer: ""
---

## Overview

**PacAttributeSystem** is a generic Unity package for managing entity attributes such as MaxHealth, speed, damage, or any custom stat through a clean and extensible API.

At its core, the system revolves around three components:

- **`PacAttributeProfile<T>`** : A `ScriptableObject` that stores the base values of each attribute, defined by a custom enum `T`. Profiles can be set up directly in the Inspector.
- **`PacAttributesController<T>`** : A `MonoBehaviour` that loads a profile at runtime and manages the live state of all attributes. It supports reading base and final values, subscribing to change callbacks, and handles all recomputation automatically.
- **`PacAttributeModifier<T>`** : Represents a modifier applied to an attribute. Supports two stacking modes: **Additive** (flat bonus) and **Multiplicative** (percentage bonus, summed before application). Modifiers are tracked by source.

**Key features:**

- Fully generic, works with any `enum` you define
- Cached final values recomputed only when needed, with dirty-checking to avoid unnecessary callbacks
- Optional rounding to integer values
- Subscribe/unsubscribe callbacks per attribute `(oldValue, newValue)`

## Technical Details

- **Moteur** :Unity
- **Langage** : C#
- **Version Control** : git
- **Years** : 2026

## Links

You can add the package to your project using the Git URL below.

- [GitHub](https://github.com/Stanpac/StanpacPackages/tree/main/Packages/com.stanpac.pacattributessystem)
