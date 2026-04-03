---
title: QuantumShift
description: describes the project in a few words.
engine: Unreal Engine 5
language: C++, Blueprints
role: Lead Programmer
team: 5 people
duration: 3 month
year: 2024
github: "https://github.com/Stanpac/Quantum-Shift"
itch: ""
build: "https://drive.google.com/drive/u/3/folders/1j1ixOx_4NTgkA0UAwlOBRH8OcBhd4kVz"
trailer: ""
---

## Overview

QuantumShift is a first-person arena shooter where you face waves of drones and a final boss drone in a contained combat space. The core mechanic revolves around gravity inversion, letting you flip between the floor and the ceiling of the arena to reposition, dodge, and find new angles of attack.

## Technical Details

- **Moteur** : Unreal Engine 5
- **Langage** : C++, Blueprints
- **Version Control** : git
- **Rôle** : Lead Programmer
- **Team** : 5 people
- **Years** : 2024
- **Duration** : 3 months

## Links

- [Download build](https://drive.google.com/drive/u/3/folders/1j1ixOx_4NTgkA0UAwlOBRH8OcBhd4kVz)
- [GitHub](https://github.com/Stanpac/Quantum-Shift)

## Screenshots

<Carousel>
<img src="/Projects/Assets/QuantumShift/QuantumShift_Screenshoot_1.png" alt="Screenshot 1">
<img src="/Projects/Assets/QuantumShift/QuantumShift_Screenshoot_2.png" alt="Screenshot 2">
</Carousel>

## My Role

As one of two programmers on the project, I handled the player controls, the gravity inversion mechanic, UI and animation integration, and the boss drone AI.

## Challenges

The hardest challenge was the gravity system. Our original idea was to let the player move across all four walls of the arena and transition between them fluidly, but we ran into significant issues with camera rotation management and couldn't reach a satisfying result, which led us to scrap the idea and simplify it down to a straightforward gravity inversion between floor and ceiling.

The small drone AI was another interesting challenge. To make them feel more threatening and dynamic, we implemented a flocking behavior inspired by fish schooling, where drones maintain distance from each other while collectively pursuing the player, giving the impression of a coordinated swarm rather than individual enemies.
## Conclusion

A somewhat frustrating project given the challenges we ran into and not being able to fully realize our original core mechanic, but one I still learned a great deal from.

