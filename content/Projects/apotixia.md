---
title: Apotixia
description: 4-player simultaneous card-chess strategy gameactions simultaneously.
engine: Unreal Engine 5
language: C++, Blueprints
role: Programmer
team: 6 people
duration: 3 month
year: 2025
github: "https://github.com/pacistan/Apotixia"
itch: ""
build: "https://drive.google.com/drive/folders/1S9nqSuwySM8Z5R1so4QoAd6qVWw2122W?usp=drive_link"
trailer: "https://youtu.be/s9Bz4Xp0i4E"
---

## Overview

Apotixia is a 4-player free-for-all tactical game that blends chess-inspired movement with card-based unit summoning in a mythological Greek setting. Players draw cards, deploy unique units, and fight to control the center of the board, scoring points each round until one player reaches five. 
Everyone prepares actions at the same time, then watches them unfold together, creating a mix of strategy, prediction, and chaos.

## Technical Details

- **Moteur** : Unreal Engine 5
- **Langage** : C++,  Blueprints
- **Version Control** : git
- **Rôle** : Programmer
- **Team** : 6 people
- **Years** : 2025
- **Duration** : 3 months

## Links

- [Gameplay Video](https://youtu.be/s9Bz4Xp0i4E)
- [Download build](https://drive.google.com/drive/folders/1S9nqSuwySM8Z5R1so4QoAd6qVWw2122W?usp=drive_link)
- [GitHub](https://github.com/pacistan/Apotixia)

## Screenshots

<Carousel>
<img src="/Projects/Assets/Apotixia/Apotixia_Screenshoot_1.png" alt="Screenshot 1">
<img src="/Projects/Assets/Apotixia/Apotixia_Screenshoot_2.png" alt="Screenshot 2">
<img src="/Projects/Assets/Apotixia/Apotixia_Screenshoot_3.png" alt="Screenshot 3">
<img src="/Projects/Assets/Apotixia/Apotixia_Screenshoot_4.png" alt="Screenshot 4">
</Carousel>

## My Role

I was one of the two programmers on the project. We both worked on the core gameplay systems, and I also handled the lobby, multiplayer connection setup, and the UI layout. This gave me the opportunity to contribute both to the main gameplay experience and to the systems that support the player’s interaction with the game.

## Challenges

One of the biggest challenges on this project was that it was our first time developing a multiplayer game in Unreal Engine. We had to learn how multiplayer worked in general, from handling lobby connections to understanding replication properly and using multicast events correctly. It was a very practical learning process, and solving these networking issues was an important part of making the game work reliably.

Another challenge I worked on was making sure that only the chessboard itself was replicated in multiplayer, while the environment remained identical for every player. This was important because we did not want our artist to create four different versions of the environment for each point of view. As a result, each player shares the same environmental viewpoint, even though their actual position on the board is different.

## Conclusion

I really enjoyed working on this project, especially because it gave me the opportunity to discover multiplayer development in Unreal Engine. Learning how networking changes the way systems must be designed and programmed was both challenging and very interesting. It was a very different approach from the programming practices I was used to, and it made the project particularly rewarding for me.

