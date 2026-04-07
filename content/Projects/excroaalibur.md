---
title: Excroaalibur
description: Fast-paced turn-based tactical game
engine: Unity 
language: C#
role: Lead Programmer
team: 10 people
duration: 5 month
year: 2025-2026
github: "https://github.com/pacistan/Excroaalibur"
itch: "https://sneakysunset.itch.io/araka"
build: ""
trailer: ""
---

## Overview

Excroalibur is a tactical turn-based game where you play as a team of three frogs trying to survive against infinite waves of enemies. After getting their hands on a legendary sword guarded by equally foolish knights, the frogs must defend themselves and escape by using the weapon in the most questionable way possible: throwing it. By passing the sword between teammates, players can power it up and use it to deal with stronger and stronger enemies, creating a combat system built around strategy, teamwork, and absurdity.

## Technical Details

- **Moteur** : Unity
- **Langage** : C#
- **Version Control** : git
- **Rôle** : Lead Programmer
- **Team** :10 people
- **Years** : 2025-2026
- **Duration** : 5 months

## Links

- [play on Steam](https://store.steampowered.com/app/4392470/Excroaalibur)
- [GitHub](https://github.com/pacistan/Excroaalibur)

## Screenshots

<Carousel>
<img src="/Projects/Assets/Excroaalibur/Excroaalibur_Screenshoot_1.png" alt="Screenshot 1">
</Carousel>

## My Role

I was the lead programmer on a team of three programmers. My role included structuring the team’s workload, writing and assigning tasks, and making sure development progressed smoothly and efficiently. I also worked closely with the other departments to understand their technical needs and translate them into clear programming objectives.  
In addition to this coordination work, I remained actively involved in development by implementing gameplay mechanics, designing system architecture, and contributing to the project’s core technical systems.

## Challenges

One of the main challenges in this project was building a system able to preview the result of certain actions before they were actually executed in-game. This required us to split the action logic into two separate parts: a pre-calculation phase that simulated the result and stored the necessary data, and an execution phase that used this stored data to play the action while updating the UI, meshes, and other visual elements at the right time. Making these two systems work together cleanly and reliably was one of the most demanding technical aspects of the project.

Another important challenge for me was designing the visualization system that showed where actions could or could not be performed. To achieve this, each tile used a canvas on a dedicated layer that was updated according to movement or action availability. A camera rendered only this layer to a texture, and I then used a shader to project it as a decal onto the environment so the player could clearly read the available zones. This was a very interesting system to work on because it involved both gameplay logic and rendering techniques.
## Conclusion

I really enjoyed working on this project, as it was both highly rewarding and genuinely interesting from start to finish. It was the first time I had such an important role as a lead programmer, and it gave me a much clearer understanding of how demanding this position can be, but also how essential it is to a project’s overall success.  
Beyond the technical work itself, this experience taught me a lot about responsibility, communication, and team organization, and it made this project especially valuable for my growth as a developer.
