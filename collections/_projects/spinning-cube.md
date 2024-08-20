---
title: Spinning Cube
categories:
    - Spinning Cube
project-page-sort-id: 102
excerpt: "An AI NPC character applied to a point-and-click puzzle scenario. *A solo project for GDG Game Jam 1.*"
header:
    overlay_image: /assets/images/spinningCube1.png
    teaser: /assets/images/spinningCube1.png
---

# Summary
Spinning Cube was built in a day during GDG Game Jam 1.

The goal was to experiment with the combination of a modern AI NPC, and classic point-and-click gameplay.

Below is a video of the result,

[![Spinning Cube Demo](http://img.youtube.com/vi/wqqJ8Wv3Zmw/0.jpg)](https://youtu.be/wqqJ8Wv3Zmw "Spinning Cube Demo")

Spinning Cube was demonstrated at Interactive Futures 2024.

# InWorld
InWorld was used to power the character,
[InWorld](https://inworld.ai/)

InWorld asks you to create a character on their platform, then lets you chat with it with some REST API calls.

## AI NPC Personality
The character, 'Spinning Cube', was created on InWorld, where the personality can be configured.

![Setting the NPC Personality](/assets/images/spinningCube2.png)

These basic traits can result in some surprising emergent gameplay.

> Player: Do you like tomatoes?

> AI: I do not like tomatoes, because they are shaped like spheres, and I'm afraid of spheres.

## AI NPC Knowledge
AI NPCs can be given knowledge of the world, and knowledge only they hold. Knowledge can reference themselves and other characters in the game.

![Setting the NPC Knowledge](/assets/images/spinningCube3.png)

## AI NPC Goals
The core point-and-click gameplay was achieved through setting 'Goals'.

The script below was added to SpinningCube, and send and receive triggers from Unity, and can adjust the AI character profile.

There's flexibility in the system; you can curate the response of a character on a trigger, but also change the emotional state of a character. 

See 'actions' below...

```
goals:
  # On earthquake trigger, drop coins
  - name: 'drop_coins'
    repeatable: false
    activation:
      trigger: 'EarthquakeTrigger'
    actions:
      - say_verbatim: 'Yikes! What was that?! Oh no, my coins!'
        emotion_change: 'TENSION'
        send_trigger: 'dropped_some_coins'

  - name: 'drop_coins_justalook_persuade'
    repeatable: false
    activation:  
      intent: 'coin_justalook'
    actions:
      - say_verbatim: 'Oh, you want to see my gold? I am not sure...'
        emotion_change: 'TENSION'
        send_trigger: 'coin_justalook_started'
      - say_verbatim: 'Alright then, but just have a look...'
        emotion_change: 'TENSION'
        send_trigger: 'dropped_some_coins'

  - name: 'report_theft'
    repeatable: false
    activation:
      trigger: 'TheftTrigger'
    actions:
      - say_verbatim: 'Oy! Did you steal my coins?!'
        emotion_change: ANGER

intents:
  - name: 'coin_justalook'
    training_phrases:
      - 'Can you please show me the coins?'
      - 'What do gold coins actually look like?'
      - 'What do gold coins sound like when they are dropped?'
```

In this case, the SpinningCube character changed their emotional state to `ANGER` when the player stole their gold.

# Conclusion
Plenty of potential and plenty of challenges to build a full game around, but I was happy with the outcome!