---
title: Roadtrip
description: describes the project in a few words.
engine: Unity
language: C#
role: Programmer
team: 6 people
duration: 3 month
year: 2024
github: "https://github.com/Stanpac/RoadTrip"
itch: ""
build: "https://drive.google.com/drive/u/3/folders/1EV0YvUqoLWRcI7iRQCkH5dN-QU363dec"
trailer: ""
---

## Overview

RoadTrip is a mobile auto-runner where you play as a cheerful family heading out on a road trip. The trunk is full, so the only option is to strap all the luggage on the roof and hope for the best. As the car speeds through increasingly chaotic roads, bags start sliding, bouncing, and flying off. Your goal is simple : survive the journey and lose as little luggage as possible, all while collecting new memories along the way.

## Technical Details

- **Moteur** : Unity
- **Langage** : C#
- **Version Control** : git
- **Rôle** : Programmer
- **Team** : 6 people
- **Years** : 2024
- **Duration** : 3 months

## Links

- [Download build](https://drive.google.com/drive/u/3/folders/1EV0YvUqoLWRcI7iRQCkH5dN-QU363dec)
- [GitHub](https://github.com/Stanpac/RoadTrip)

## Screenshots

<Carousel>
<img src="/Projects/Assets/Roadtrip/Roadtrip_Screenshoot_1.png" alt="Screenshoot 1">
<img src="/Projects/Assets/Roadtrip/Roadtrip_Screenshoot_2.png" alt="Screenshoot 2">
</Carousel>

## My Role

As the sole programmer on the project, I was responsible for the entire codebase. My main technical contributions were the procedural level generation system, which scales in difficulty over time, and the car physics. I also supported the team on integration and helped shape some system designs to back up the game designers.

## Challenges

My biggest challenge was reproducing convincing car controls and wheel physics. Rather than using Unity's built-in Wheel Collider, which I found too rigid to tune and couldn't get to a satisfying feel with, I built my own wheel simulation from scratch using Raycasts. It required a lot of research and iteration to get right.

The procedural generation system was another significant challenge. I designed it around a credit-based approach inspired by Risk of Rain's enemy spawning system. Each level tile has a difficulty cost, and the generator accumulates a currency over time that it spends to place tiles. As time passes, the budget grows, allowing increasingly difficult tiles to appear and naturally ramping up the challenge for the player.

## Conclusion

Working on RoadTrip was a genuinely enjoyable experience. Being the only developer was challenging but deeply rewarding. I'm particularly proud of the car physics and the procedural generation system, both pushed me to research and build things I hadn't done before, and seeing them come together in a working game was very satisfying. The end result is something the whole team can be proud of, and working alongside such a great group of people made it all the more worthwhile.

