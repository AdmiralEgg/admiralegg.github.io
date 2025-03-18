---
title: "Devlog: Animating on a Budget" 
tags:
    - Devlog
    - Design
categories:
    - Hidden Dogs
---
Hellooooo dog fans! I'm Chris, Designer and Programmer on Hidden Dogs: In the Dog House. 

Along our Hidden Dogs (HD) development journey I'll be writing a few devlogs, about whatever topic takes my fancy. Today, it's Animation!

## Animation!
Back int' day, when I was a lad, t' family would gather 'round TV 'n pick channel. *Four*, we 'ad. 

Ahh, simpler times.

One channel had *Catchphrase*. I'd watch Catchphrase. I'd watch Catchphrase *a lot*.

[Catchphrase! Doubt this has aged well...](https://youtu.be/ttcL6Dc5qkc?si=H-LELfGSRox3__VU&t=281)

Catchphrase had an animation style which I only know as '[Flipbook Animation](https://youtu.be/J2xrN5WQuxw?si=MlXoMr5Lml5cs4Ig)'.

If you look at our 
[trailer](https://store.steampowered.com/app/3363850/Hidden_Dogs_In_the_Dog_House_Demo/), you'll notice the flipbook style. If you're very observant you'll notice that we're animating to the beat!

## Animating to the Beat!

**Animating in time with the music** is the secret sauce of Hidden Dogs.

As music plays, a signal is sent to the game on every beat. Those signals are used to trigger; animations, sounds, movement, and more!

My first time trying this was in the prototype, Goons. In Goons, lights would flash, the crowd would jump, and the Goon would dance, all in time to the music.

<img src="/assets/gifs/goons-dance-animation-blog.gif" width=250>

## Why do it this way?
It's cheap and effective!

It's *cheap*, because we don't need an animator! We can take an image (say, a cloud), then; move it, rotate it, squash it, or stretch it using tools already available in our game engine. Simply rotating a cloud back and forth to the music can bring it to life.

It's *effective*, because it's our job to keep you (the player) immersed in the world. Linking music and movement is something players aren't likely to notice, but they should *feel* it.

Cheap and effective design goes a long way in Indie game development.

## Animation in a Level
Here's an example of it in action. This is one of our *character mutts*, Stinky!

<img src="/assets/gifs/stinky-animation-blog.gif" width=250>

Stinky will appear in lots of levels, his flies and stink following him!

## Animations on the Map
Here's an example from the map, with a tractor ploughing a field and a dancing cloud.

<img src="/assets/gifs/tractor-animation-blog.gif" width=250>

The tractor moves in a flipbook style, and will move when it gets a beat trigger from our music track.

## Rules of Animation
The simple rules for animation - anything *in-world* will animate on the beat, using a flipbook style.

Our user interface (UI) doesn't animate this way, as we don't consider the UI to be *in-world* for Hidden Dogs.

## The Downside
If the player turns the music off, the animation can feel erratic and random.

This is a problem with streamers, as they use their own background music while playing the game!

## Finally
So that's the trick to our animation.

Thanks for reading, I've got plenty more of Hidden Dogs to show in the future, so make sure you keep an eye on this devlog!