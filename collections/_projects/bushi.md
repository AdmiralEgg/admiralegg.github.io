---
title: Bushi
categories:
    - Bushi
excerpt: "Battle waves of enemies in feudal Japan, using only the power of typing!"
header:
    overlay_image: "/assets/images/bushi-gameplay3.png"
    teaser: "/assets/images/bushi-gameplay3.png"
---

<figure class="half">
    <a href="/assets/images/bushi-gameplay3.png"><img src="/assets/images/bushi-gameplay3.png"></a>
    <a href="/assets/images/bushi-gameplay2.png"><img src="/assets/images/bushi-gameplay2.png"></a>
</figure>

*Bushi was worked on through 2023 and closed down in March 2024.*

*This post was written August 2024.*

# Summary
Bushi was an ambitious personal project, worked on early in my career, that reached a rough prototype state through sheer determination and copious amounts of caffeine.

Here's the elevator pitch, written back in 2023.

> Bushi is arcade-action game about a Samurai, driven by revenge, chasing a ruthless clan leader across Japan.
>
> Battle waves of enemies and bosses across varied locations, growing your powers of ninjitsu, magic, and the blade, and fight using only your keyboard! Master the forgotten art of speed typing in this unique, Clack n' Slash experience.

Bushi was a brilliant learning experience, with a scope only a naive, novice game developer would dare take on!

# Design
Bushi was designed as a replayable, arcade experience, with the keyboard as the primary controller. 

The game was 'on rails', i.e. the player had no direct control over the character. Instead they would move between locations, then asked to fight with keyboard commands.

## Game Loop
Following a narrative through levels, players would alternate between Battles and Transitions, ultimately reaching a boss battle.

<a href="/assets/images/bushi-gameLoop.png"><img src="/assets/images/bushi-gameLoop.png"></a>

In Battle, players fight waves of enemies, typing words displayed on screen to attack, block, use items, and cast magic spells.

In Transitions, their character would run through the level to the next Battle, giving the player a break and the opportunity for light narrative to move the story along.

At the end of the level the player would go to a tavern to spend their Battle XP on upgrades.

## Battles
Battles are similar to the Final Fantasy 7, with the player having a set of actions to trigger, then waiting for the action to be performed.

Players had the option of 3 stances; Attack, Defence and Magic. These stances served random words to the 'BattleText' UI at the top of the screen.

<a href="/assets/images/bushi-gameplay2.png"><img src="/assets/images/bushi-gameplay2.png"></a>

Outside of stances, players had access to Items. These were static words that could be typed at any time, but had a cooldown period after use.

Taking cues from arcade games; if you run out of health, you die and lose all your progress. Bushi aimed for a ~30 minute playthrough from start to finish.

## Upgrades
### Battle Arts
Upgrade your core attacking and defensive abilities, unlocking; longer words for more powerful attacks, lower cooldown times for quicker attacks, and defensive actions such as Parry and Riposte.

### Ninjitsu
Unlock powerful items to crowd control the enemy, and the ability to see hidden secrets within the environment that give you the edge over your opponent.

### Magic
Unlock higher tiers of magic, powerful spells, faster casting and faster magic meter build up.

# Design References
Typing of the Dead and the Final Fantasy 7 battle system were the main design references for Bushi.

## Typing of the Dead | Keyboard Actions
Typing of the Dead is a keyboard controlled offshoot of House of the Dead.

<figure class="third">
    <a href="/assets/images/bushi-reference1.jpg"><img src="/assets/images/bushi-reference1.jpg"></a>
    <a href="/assets/images/bushi-reference2.jpeg"><img src="/assets/images/bushi-reference2.jpeg"></a>
    <a href="/assets/images/bushi-reference3.jpg"><img src="/assets/images/bushi-reference3.jpg"></a>
</figure>

The keyboard takes the tactile feeling of a light gun trigger, and moves it to the home. It's great edutainment for players wanting to improve their typing.

Given the cult following of mechanical keyboards, this control scheme seems ripe for a revival.

## Final Fantasy 7 | Active Time Battle (ATB) system
The semi-turn based ATB system of Final Fantasy 7 was an inspiration for the Bushi battle system.

[ATB Write Up](https://finalfantasy.fandom.com/wiki/Battle_system#Active_Time_Battle)

In Bushi, rather than waiting for a bar to fill for a turn, the player would wait for a cooldown after an attack until the next random word was available to be typed.

## Golden Axe | Magic System
The Magic stance would allow players to build up their Magic meter. The higher your meter, the more powerful the spells you could cast. Similar to the Golden Axe magic system.

<a href="/assets/images/bushi-reference4.jpg"><img src="/assets/images/bushi-reference4.jpg"></a>

# Programming
Most Bushi code was written from scratch in C#. Following this project, I standardised my code and project structure.

Below is a breakdown of a few core systems in the game.

*Note: All Bushi code is on GitHub, please contact me if you're interested in having access.*

## Dictionary Manager
- The **Dictionary Manager** singleton class would read a JSON file of 10,000 most popular English words, then order each word by size.
- On request, Dictionary Manager would return a random word as a **Word** object. Requests could come from multiple different places.
- **Word** objects tracked the completion state of a word.

## Scriptable Objects
Unity's Scriptable Objects (SOs) were used where needed. **Static** SOs were read in on start. **Dynamic** SOs were read then used as a decoupled data containers for multiple systems to read and write to. Examples below.

### Static Data

**Enemy**
- Enemy Type
- Enemy Health
- Enemy Abilities

**Enemy Wave**
- Number of Waves
- Enemies in Wave
- Spawn Point Positions

**Equipment**
- Equipment Name
- Equipment Damage
- Equipment Cooldown

### Dynamic Data
**Player & Enemy**
- Health
- Magic
- Items

## Dialogue with YarnSpinner
[YarnSpinner](https://www.yarnspinner.dev/) was used for the dialogue system. It's a simple tool allowing writers to type script-like code. Below is an example of a YarnSpinner testing script.

- `->` values were parsed by YarnSpinner to display multiple actions a player could pick from. 
- Brackets `<< >>` would trigger events in the game, the example below shows triggering of cameras, animations, and updating the main directional light.

```
title: Opening
tags:
---
Wow! My first ever Yarn script in Unity!

Lets switch the camera eh...
<<SetCamera Cutscene PlayerFocus>> // Switching the camera to camera named PlayerFocus

-> Gosh!
-> Incredible!
-> I'm amazed!

Switch the camera again...
<<SetCamera Cutscene PlayerFocus2>>

Back to our normal camera
<<SetCamera Cutscene FullScene>>

How about some pathetic fallacy?
<<SetLighting Cutscene Dark>>

Back to standard lights then...
<<SetLighting Cutscene Light>>

Let's trigger an animation...
<<TriggerAnimation Cutscene gesture>>

Huzzah! Finished!
```

## Player & Enemy
The Player and Enemies shared the same **State Machine**, with states such as; Idle, Attack, Throw. These used an abstract BaseState, which required EnterState and UpdateState functions.

The State Machine was also responsible for triggering animations, including the player moving to an enemy and back, attacking, or throwing items.

This was the first State Machine I'd implemented, and I'd go through multiple iterations of State Machine structures before setting on the one currently used for Cosy Builder object states.

# Conclusion
Bushi taught me about scope and burnout. It taught me which parts of games are complex, and how focused effort and execution can be more important than ideas. It taught me how clear design at the start of the project can save you many, many cycles of iteration.

It's a project I'd like to revisit in the future, when I have more experience, as the battle system combined with the input system make something quite unique.