---
title: Echoes of the Past
categories:
    - Echoes of the Past
project-page-sort-id: 99
excerpt: "A story driven puzzle game set in a medieval environment. <i>Playable on Itch.io!</i>"
header:
    overlay_image: /assets/images/echoesGameplay.jpeg
    teaser: /assets/images/echoesTeaser.jpeg
---

<figure class="third">
    <a href="/assets/images/echoesGameplay.jpeg"><img src="/assets/images/echoesGameplay.jpeg"></a>
    <a href="/assets/images/echoesGameplay2.jpeg"><img src="/assets/images/echoesGameplay2.jpeg"></a>
    <a href="/assets/images/echoesGameplay3.jpeg"><img src="/assets/images/echoesGameplay3.jpeg"></a>
</figure>

# Summary
> Echoes of the Past is a story driven puzzle game set in a medieval environment. [Play It Here](https://lukecarter.itch.io/echoes-of-the-past)

Echoes was a team project for the [Game Dev Group](https://www.linkedin.com/company/the-game-dev-group/) Bootcamp. This 5 person team included; a programmer, two 3d artists, a sound designer, and me. A writer was brought in during development to flesh out the backstory and write the narrative lines. My role was designer, and I programmed a few systems.

Echoes takes inspiration from [The Crystal Maze](https://en.wikipedia.org/wiki/The_Crystal_Maze). The player is placed in a hub world with many closed doors, behind the doors are puzzles. In Echoes, rather than being driven by crystals, the player is driven by an unfolding story.

The player is introduced to the story in a Hub room, then asked to complete a set of puzzles. After each puzzle, the player is rewarded with new story details. When the puzzle set is completed, players are asked to choose the outcome of the story. The story is delivered by a 'narrator' voiceover, with accompying text.

The finished product represents a vertical slice of the game; one story and set of puzzles was presented, whereas a full story arc would tell three stories, with three sets of increasingly challenging puzzles.

# Design
My key deliverable was a design document for the game. Core part of the design included,
- The overarching story, and impacts of player choices.
- Puzzles mechanics, and puzzle level design.
- Movement mechanic requirements.
- Tonal consistency, through story, sound and animation.
- Player navigation and goal setting using scene lights.

## Story
Below is the full narrative flow for the game. The vertical slice delivered the first story of three, with the ending adjusting based on the choices the player made along the way.

<a href="/assets/images/echoes-ref1.png"><img src="/assets/images/echoes-ref1.png"></a>

## Puzzle Design
There are 3 puzzles types in Echoes,

**Light Puzzles** - Players are asked to direct a beam of light between mirrors to an end goal.

**Dark Puzzles** - Players are dropped into a circular, dark maze, with a torch. From the centre of the maze, they can see areas of light. The player searches through the maze to reach the lights.

**Story Puzzles** - Players are dropped in a scene which links into the story being told. They are encouraged to explore their environment with a 'symbol find' style puzzle.

In the Hub level, verticality is used to split the puzzle categories, i.e. Light puzzles are all up stairs!

## Tonal Consistency
The design aimed for an immersion and a magic-realism tone, with the magical elements of the game becoming more recognisable more as the game went on. What Remains of Edith Finch was a touchpoint for the slow burn approach to showing the magical elements of the game.

Elements of tonal consistency,
- UI elements were kept to a minimum, and if needed they were [diegetic](https://en.wikipedia.org/wiki/Diegesis). For example, UI fonts are a handwritten style.
- Sound and animation were designed to be organic, old world, ancient mechanisms, inspired by Indiana Jones and Tomb Raider.

## Player Navigation & UX
With the requirement of an immersive experience and limited UI elements, player were shown their goals with torch lights in the scene. 

Torches could change colour and intensity through a Dynamic Light System. This was used to guide players to available doors.

# Systems
I wrote a number of systems for the game, below are the major systems.

## Narrative System
The narrative system uses the following Unreal Engine features; Data Tables, Enum Objects, an Actor Blueprint and an Interface Blueprint.

Audio was recorded in 'chunks', each chunk being between 2 and 8 lines of dialogue. Each chunk was linked to many subtitle strings in a Data Table, and each subtitle had a delay value. This allowed manual syncing of when the subtitles appeared, to match the dialogue in the audio chunk. 

It is a discrete system designed to be triggered by anything, with the requirement of the Enum value of the audio chunk to be passed. This allowed maximum flexbility for our programmer trigger narrative from other systems.

Manually coding delays between subtitle lines is not the optimal way of designing this system, but for a vertical slice it was a quick, effective, and easily configurable.

## Dynamic Light System
The dynamic light system uses similar Unreal features to the narrative system. It is required for players to navigate around the hub, and show remaining puzzles doors that need to be completed.

The Dynamic Light System could trigger single lights, or groups of lights, and switch colour or intensity. This was used extensively for torches in the game.

A 'Manager' actor would relay messages between any blueprint in the game wanting to update a 'dynamic' light, and the light itself. Dynamic Lights had to be part of a blueprint, and inherit a 'Dynamic Light' blueprint, to allow it to receive events.

This system was designed and built in a couple of days at the end of the project, and as such it required some system knowledge to configure. It was not friendly to non-engineers. 

If I were to redesign, I'd focus on making the system easier to understand and tweak for artists and level designers. I'd expose more parameters on the lights themselves, e.g. 'Target Intensity' and 'Target Colour', I'd implement more debugging options, to allow the target state to be changed to in-editor. Finally, I'd allow artists to author their own named target states. 

## Mirror Staff Puzzle Mechanic
This mechanic took a blueprint our programmer had worked on, and refined it to meet the design requirements.

In the design, the player would push a 'rod', perpendicular to the vertical staff, to rotate it. The staff could rotate 360 degrees, but had a set list of degree values it would 'lock' into.

The following was implemented,
- Rotating clockwise or anti-clockwise depending on where the player is standing.
- Handling wrap around rotation. 
- Drawing debug lines for; initial staff rotation, available staff rotations, and the light beam itself.

Finally, when the staff begins rotating, the player could not  rotating again until the staff came to a stop. To indicate the stop, a 'clunk' sound was added.

## Visual Scripting in Unreal
All systems in the game were built using Blueprints. This was a choice by our programmer, and sensible given the time constraints and number of small systems required to be built.

Using Blueprints, I learnt the following,
- Make systems small and modular. As blueprints compile to binaries, they are difficult to compare, so large systems that get touched by many developers often lead to conflicts.
- Use Functions and Modules to break up Blueprints. 
- Use Interfaces to de-couple systems, and trigger descreet systems by passing events. This was used in the Narrative and Dynamic Light systems.

## Use the tools the Engine provides
As a programmer, often your first instinct is to code a solution to a problem. However, most problems aren't unique to your game, and taking the time to research in-engine solutions before rolling your own can saves a lot of time.

# Puzzles and Player Challenge
The discussion of challenge in relation to the puzzles was regularly had during development. I would push for simplicity, having seen a gradual build up of puzzle mechanics in games like The Witness and Portal, and the team would push for complexity, remembering the 'AHA!' moments of excitement that solving a complex puzzle brings.

During development I was reading [A Theory of Fun for Game Design](https://theoryoffun.com/index.shtml), and after development, I was introduced to the [Structure of Observed Learning Outcomes (SOLO) taxonomy](https://helpfulprofessor.com/solo-taxonomy/)

A Theory of Fun describes how learning, understanding and mastering patterns leads to fun in games, and the SOLO taxonomy defines the stages in the process of learning.

Rigorously sticking to the SOLO taxonomy when introducing new mechanics gives the designer the opportunity create the 'AHA!' moments for the player. These moments are generated when multiple mechanics and dynamics ([See the MAD framework](https://en.wikipedia.org/wiki/MDA_framework)) combine in interesting ways.

However, I could never articulate these ideas to my team. I knew *what* needed to be done, but I didn't know *why*. As a designer, I need to be clear on *why* decisions are being made.

# Conclusion
Echoes of the Past is a mish-mash of ideas, some executed well, and some not so well. I'm proud of the design of this game, at a high level the game fits together cohesively, but where it falls down is the execution of the puzzle rooms themselves.

There was plenty to learn from this project, expecially on the soft skills side. I think, given the many challenges of the project, what we produced has the raw ingredients of a good game.