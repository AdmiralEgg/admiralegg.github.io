---
title: Cosy Builder
categories:
    - Cosy Builder
project-page-sort-id: 100
excerpt: "A relaxing game about decorating a room."
header:
    overlay_image: "/assets/images/cbGameplay1.png"
    teaser: "/assets/images/cbGameplay1.png"
---

<figure class="third">
    <a href="/assets/images/cbTitle.png"><img src="/assets/images/cbTitle.png"></a>
    <a href="/assets/images/cbGameplay1.png"><img src="/assets/images/cbGameplay1.png"></a>
    <a href="/assets/images/cbGameplay2.jpg"><img src="/assets/images/cbGameplay2.jpg"></a>
</figure>

# Summary
> Cosy Builder is a relaxing game about decorating a room.
[Play It Here](https://admiralegg.itch.io/cosybuilder)

Cosy Builder was my first prototype after taking a career break and deciding to invest my time into making games.

The idea was sparked by a friend, who described a cosy game where you furnish a room then take photographs. Using this idea as a baseline, I looked at The Sims and aimed to simplify the design by,
1. Removing the requirement for items to be placed on a grid.
2. Reducing the amount of options presented to the player.

To reach these goals, some experimental features were added,
- Items in the game have physics, making the act of decorating feel more organic and chaotic.
- Players can 'focus' their view onto placed fittings, e.g. shelves, bookcases, tables, to perform small adjustments to items.
- Items are made available only when needed. For example, books are available only when 'focused' in on a bookshelf. This is an example of [Progressive Disclosure](https://en.wikipedia.org/wiki/Progressive_disclosure).

In the most recent version of Cosy Builder, the first-person camera and photo mode have been removed, with more time spent on refining the mechanics used to furnish the room.

# Design & Programming
For a long writeup on Cosy Builder, please read the article below.

[Cosy Builder Closedown Report](https://admiralegg.github.io/cosy%20builder/CosyBuilder-ClosedownReport/)

# Key Learnings
- Working with physics and lighting in Unity.
- Object state was controlled by state machines, and efficient spawning of objects was managed by object pooling.
- Player UX improvements made using object outlining and the [Shapes](https://acegikmo.com/shapes/) package.

# From Prototype to Release
Cosy Builder was a prototype, so a full game loop was not designed. A release of Cosy Builder would require, at a minimum;
- An opening tutorial.
- Content; more items, more rooms.
- An item unlocking system.

# Conclusion
The Cosy Builder prototype took two months to reach a playable state, and following player feedback, an additional six weeks to refactor and refine a number of mechanics to make the game playable.

The initial prototype was not playable, as the controls were not intuitive to players. The refactor was done with [Jakob's Law](https://lawsofux.com/jakobs-law/) in mind, adapting the control scheme from The Sims.

Cosy Builder was shown at Interactive Futures 2024, and was well received by younger players, who found plenty of creativity in the chaos of the item physics.