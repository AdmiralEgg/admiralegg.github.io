---
title: Goons Closedown Report
tags:
    - Design
    - Systems
    - Closedown Report
excerpt: Closedown Report for Goons
categories:
    - Goons

toc: True
toc_sticky: True
---
*Written in February 2024, and published in August 2024*

Goons is a character comedy rhythm game, set in a Victorian era cardboard box theatre. [Play It Here!](https://admiralegg.itch.io/goons)

Goons was made to learn and demonstrate the following areas,
- **Game Feel** - audio, animation and lighting feedback on user interaction and game progress. 
- **World & Art Style** - muted colour palette, a mechanical feel to all game components, and diegetic UI.
- **Rhythm Elements** - Music synchronised with lighting and animation. 
- **Optimising for Android**
- **AI Asset Generation**

The input system is limited to touch only, to align with mobile and allow focus on other areas of the game.

Facial motion capture was explored, but did not make the final product. This document will review the motion capture process.

# Design
Goons is a linear, level based game, where the player is given freedom to make sounds to a beat with the goal of entertaining the crowd. Each level the player is given more tools to make sounds, or more control of the sounds created by their Goon. The final level is a 'Sandbox' where players can access all the tools without restriction.

A fixed points value is required to complete a level. Points are awarded for actions while the music is playing. The crowd grows in intensity the closer you get to the required points total. 

Being on-beat is not accounted for in points (but there is some code to implement this). There is no fail state for the game, but the incentive for triggering sounds on the beat should be natural for players. 

# Optimisation
This project was intended for mobile, and optimisation work was done at the end of the project. 

In hindsight, the learnings from optimisation would have changed some of the design decisions at the start of the project. The focus on lighting and dynamic scene elements was core to the game, but not suited for a mobile game.

## Optimise Meshes & Materials
For audience cosmetics, assets were AI-generated (see [AI Asset Generation](#ai-asset-generation)).

On review, these AI-generated meshes were *extremely* complex (50k faces!), so sculpting and decimation was used in Blender to reduce the poly count. Lower poly count meshes were still usable with their generated textures, so results were positive after clean-up.  

<a href="/assets/images/goons-closedownRef2.png"><img src="/assets/images/goons-closedownRef2.png"></a>
*Before: 1.6M Tris, 1.1M Verts*

<a href="/assets/images/goons-closedownRef3.png"><img src="/assets/images/goons-closedownRef3.png"></a>
*After: 126k Tris, 99k Verts*

The time taken to produce and clean-up assets was far lower than producing my own from scratch, given my current skills.

## Culling
If extra performance was required, then occlusion culling could be applied. Goons that aren't on stage stand off-stage behind a curtain, so the curtain would be set as an occluder, with Goons set as occludees. Goons should also be disabled when not used in a level.

## Optimise Lighting
During the build phase, all lighting was done in Realtime. This seems the fastest way to iterate early in a project, as there's no waiting for baking. To balance load between compute and memory for mobile, lighting was switched to mixed.

### Mixed lighting
Most elements in the scene are dynamic (shown in yellow), the backdrop is static (blue) and the crowd contribute to the GI bake, but are not static.

<a href="/assets/images/goons-closedownRef4.png"><img src="/assets/images/goons-closedownRef4.png"></a>

Crowd cosmetics are dynamic, and they initialise randomly at the start of each level.

<a href="/assets/images/goons-closedownRef5.png"><img src="/assets/images/goons-closedownRef5.png"></a>

### Emissive materials
Half of the active lights in the scene are point lights used to highlight clickable buttons. Buttons are always presented on top of a box, with the button light shining on the box (see below).  

There was an experiment in switching these to Emissive materials, which could help with performance on mobile devices. However, the result was missing the self shadowing to make the button stand out (see below),

<a href="/assets/images/goons-closedownRef6.png"><img src="/assets/images/goons-closedownRef6.png"></a>

In Unity, Emissive materials won't cast light on non-static objects, and all buttons in the scene are dynamic (see [Mixed lighting](#mixed-lighting)). 

There are workarounds for this; the button prefab could be marked as static, and the baked lightmaps preserved and manually switched on when the emissive light turns on. However, there was not enough time to experiment with this.

### Lighting Ranges
On review of the lights, it was clear that lights intended for a single purpose (e.g. lighting the audience) were interacting with unintended objects in the scene.

To combat this, lighting ranges and spotlight cone sizes were reduced so the objects they effected were targeted.

## Optimise Audio
Audio was compressed to reduce size, and some long-running sound clips (e.g. audience murmuring) were clipped and looped.

# Game Feel
Attention was paid to Game Feel for this prototype.

## Interaction Feedback - Animation & Audio
Animation and audio cues are used to give the player direct feedback on an action. 

### Goon Speak
Core interaction. Click a goon, and the goon rocks backwards as well as playing a sound. Goon cannot be spam clicked (there's a ~400ms delay before another speak is allowed), and the animation helps indicate that a speak action is in progress. A similar animation is used when clicking a scrap, as the outcome of clicking is the same (clicking a goon or a scrap make the goon speak).

### Music Play
Core interaction, when the music plays there are are two animations which indicate the beat of the music,
- The speaker scales up and back on the beat.
- The 'Off' switch for the music flashes to the beat.
- The majority of the crowd jump to the beat, although some members of the crowd rush or drag from the beat.

Similar to other rhythm games, visual feedback on the beat should lead the player to trigger sounds in time to the music. 

### Interaction Barks
Audio was recorded for clicks on various interactions with the scene, or actions,
- Catching a scrap, "Nice Catch!"
- Tapping the audience, "Get your fingers out of the audience!"
- Tapping the speaker, "Oy, we've only got that on rent!"

These interactions either give positive reinforcement to play actions (e.g. clicking the scrap), or reward player curiosity with in-world feedback.

## 'Feel' by MoreMountains
Feel is a Unity asset pack which provides game 'juice', 
[Feel, the best way to add game feel to your Unity game, by More Mountains](https://feel.moremountains.com/)

The MMWiggle tool, 
[Corgi Engine: MoreMountains.Feedbacks.MMWiggle Class Reference](https://corgi-engine-docs.moremountains.com/API/class_more_mountains_1_1_feedbacks_1_1_m_m_wiggle.html) was used extensively in the project for random GameObject animations. Such as audience and speaker animations.

## Unity Audio Tools and Fmod
All audio was integrated using Unity audio functions, and scripting where necessary. Balancing the audio elements across the project was a challenge, as the options in Unity are quite basic.  

For the next project, all audio will be integrated using Fmod. Fmod Studio allows audio editing alongside staging and triggering audio. 

Fmod is an industry standard tool, and the costs are minimal for games with a small budget.

# AI Asset Generation
4 hats and 3 items were produced with AI for this project, meshes and textures. These assets required clean-up, but the time spent creating the assets end-to-end was very quick. As the assets aren't core parts of the game, the quality can be lower.

While there are plenty of moral questions around using AI assets, I feel that engaging with these tools to get an understanding of them is really important, and for prototyping the tools can be invaluable in accelerating development time.

Tool used,
[Luma AI - Genie (lumalabs.ai)](https://lumalabs.ai/genie?view=create)

# World & Art Style
Goons is a parody of British stereotypes, set in a hand-made Victorian box theatre. Scenery and objects in the game are rough, rugged, and have simple shapes.

Visually, the core of the game has a muted colour palette of browns, oranges and reds, with strong shadows accenting elements of the scene on a lighter background.

The game world is hand crafted, so elements in the scene are textured to be familiar arts-and-crafts materials; cardboard, wood, paper, clay.

## Diegetic UI
UI is in-world (diegetic), and animated like props in a Victorian theatre style. UI elements move in and out of the scene with the feel of hinges, motors and gears controlling them. Activation times of UI elements are sometimes randomised to give them a more organic, human controlled, feel.

Issues with the UI are as follows,
- The UI does not scale to different mobile screen sizes, and functionality for this is not in place. The UI would require bespoke functionality to scale, whereas scaling of a traditional UI would be handled by Unity.
- Most UI has physics, lighting, animation and audio components, which are likely to be less performant than a 2D UI.

## Characters
The initial idea for the characters (Goons) would be rough, pencil drawn, British stereotypes; Hag, Yorky (from Yorkshire), and Toff. Face capture was done while recording the dialogue, so core facial animation could be mapped onto the 'cut out' elements of the face; eyebrows, mouth, chin. Eye animation would not be captured.

Example of Yorky and Toff, before being scanned,

<a href="/assets/images/goons-closedownRef7.jpg"><img src="/assets/images/goons-closedownRef7.jpg"></a>

The Hag character, scanned and imported into the game,

<a href="/assets/images/goons-closedownRef1.jpg"><img src="/assets/images/goons-closedownRef1.jpg"></a>

Terrifying!

On review, the simplistic 'eyes on a stick' characters; when voices, eye animation, eye colour and character scales were applied, felt more closely aligned to the game world than the hand drawn characters. This loosely ties in with the [Law of Prägnanz](https://lawsofux.com/law-of-pr%C3%A4gnanz/), and aligns with low complexity art rules.

Additionally, the 'blank canvas' design of the characters would benefit the 'Goon Customisation' feature; a core part of progression for a full game. With fewer base details on their character, players have more scope for customisation; hats, monocles, moustaches, wigs, glasses, etc.

# Facial Animation & Motion Capture
The intention was to have basic facial motion capture applied all Goons, with eyebrow, chin, mouth movements captured. Character voices were all video captured, and work was done track dots in Blender.

This was de-scoped due to the time required to create the animation. If this were required in the future the workflow would be prototyped using Apple hardware. Recent Apple hardware includes depth tracking, and iOS integration is included with Unity, which is likely to simplify the process and improve the result.

Given more time (and technology), a motion captured mouth may have been a good addition to the character.

# Programming
Programming work on this project was similar to the previous. All the 'mechanisms' in the game (i.e. dynamic objects and UI elements) used two Abstract classes to 'Enable' (move in and out of the scene) and to 'Run'. 

Larger classes were split down, Goon.cs and GoonMove.cs being a good example, but more refactoring was required here, i.e. Goon could have been split into GoonSpeak.

## Intervals / Beats
A core concept in the game was beats syncing to actions in the game world. Code was largely taken from this YouTube video,
[SYNC YOUR UNITY GAME TO THE BEAT (youtube.com)](https://www.youtube.com/watch?v=gIjajeyjRfE&ab_channel=b3agz)

## Object Pooling
Audience members would be randomly assigned a hat or an object to throw at the end of a level. This was a good opportunity to use the Object Pooling feature in Unity. On Awake, objects would be initialised in the pool, and at the end of the level would be returned to the pool after 5 seconds.

It isn't clear whether there was much performance benefit here, but it's a good habit to start using these patterns.

## Input Manager
An InputManager class was used to filter through any screen clicks, firing raycasts at the clicked position, and using the SendMessage function to trigger a generic OnClicked method in the GameObject that was collided with. The layers the raycasts interact with change with the game state.

## Asynchronous action with Coroutines
Coroutines were used throughout the project to apply delays to components switching on / off. This added to the mechanical, hand controlled, cardboard theatre theme. Pauses and waits applied to aesthetic components (e.g. lighting), were often given random wait ranges.   

For larger blocks of code that required waits, async functions were used. This allowed code to be chunked into smaller functions which could wait for each other to finish. 

# Laws Of UX
Applying a few of the Laws of UX to this game,

[Fitts’s Law | Laws of UX](https://lawsofux.com/fittss-law/)
As this game was touch based, colliders in the game were expanded beyond the mesh size of most objects to allow players room to mis-click but still active the desired effect. Goons and Buttons are adequality spaced.

Two issues are the overlap between the Scrap and Play buttons (although clicking one will hide the other), and the proximity of scraps in the Scrap Inventory, which could lead to mis-clicks.

[Law of Proximity | Laws of UX](https://lawsofux.com/law-of-proximity/)
Applies to the Melody buttons and Scrap Inventory, but has not been applied to the Play button and Speaker.

[Jakob’s Law | Laws of UX](https://lawsofux.com/jakobs-law/)
The green 'Play' triangle is good example of a well known symbol being used as a player would understand it; to start music. This is enforced, as the button rotates to a red 'Stop' button after clicking.

[Goal-Gradient Effect | Laws of UX](https://lawsofux.com/goal-gradient-effect/)
The closer the player is to the end of the level, the louder the crowd will cheer, and the more intensely the crowd will move.

[Law of Prägnanz | Laws of UX](https://lawsofux.com/law-of-pr%C3%A4gnanz/)
Simple shapes, relying on animation and sound to convey action.