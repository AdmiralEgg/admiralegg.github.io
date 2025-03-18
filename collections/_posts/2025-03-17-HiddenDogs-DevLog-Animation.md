---
title: "Devlog: Animating on a Budget" 
tags:
    - Devlog
    - Design
categories:
    - Hidden Dogs
---
Hellooooo dog fans! It's lovely to meet you all!

I'm Chris, Designer and Programmer on Hidden Dogs: In the Dog House. 

Along our Hidden Dogs (HD) development journey I'll be writing a few devlogs, about whatever topic takes my fancy. Today, it's...

## Animation!
Back int' day, when I was a lad, t' family would gather 'round TV and pick a channel. *Four*, we 'ad. 

Ahh, simpler times.

One of these channels had *Catchphrase*. I'd watch Catchphrase. I'd watch Catchphrase *a lot*.

[Catchphrase! I'm not sure it has aged well...](https://youtu.be/ttcL6Dc5qkc?si=H-LELfGSRox3__VU&t=281)

Catchphrase had an animation style which I only know as '[Flipbook Animation](https://youtu.be/J2xrN5WQuxw?si=MlXoMr5Lml5cs4Ig)'.

If you look at our 
[trailer](https://store.steampowered.com/app/3363850/Hidden_Dogs_In_the_Dog_House_Demo/), you'll notice the flipbook style, and if you're very observant you'll notice that we're animating to the beat! 

## Animating to a Beat!

**Animation to music** is the secret sauce of Hidden Dogs.

While music is playing, our music engine sends a signal to the game on every beat. Those signals are used to trigger; animations, sounds, movement... a whole bunch of things!

I first tried this in a prototypes; Goons. In Goons, lights would flash, the crowd would jump, and the Goon would dance all in time to the music. 

<img src="/assets/gifs/goons-dance-animation-blog.gif" width=250>

## Why do it this way?
It's cheap, and it's effective!

It's *cheap*, because we don't need an animator! We can take an image (say, a cloud), and move it, or rotate it, squash it, or stretch it using tools already available in our game engine. Simply rotating an image back and forth can give the feel of it dancing to the music.

It's *effective*, because it's our job to keep you (the player) immersed in the world, and linking the music and movement is something players aren't likely to notice this, but they'll *feel* it.

Ideas which are cheap and effective go a long way in Indie game development.

## Animation in a Level
Here's an example of it in action,

<img src="/assets/gifs/stinky-animation-blog.gif" width=250>

This animation is used for an indicator for our mutt, Stinky. 

Stinky will appear in lots of levels, taking his flies and stink with him!

## Animations on the Map
Here's another example, of a tractor ploughing a field on our world map. 

<img src="/assets/gifs/tractor-animation-blog.gif" width=250>

The tractor moves in a flipbook style, and will move when it gets a beat trigger from our music track.

## Rules of Animation
So, here are our core rules for animation,
- Anything *in-world* will animate on the beat, using a flipbook style.

*However*, not everything will be animated this way. Our user interface (UI) is the exception. We've breaking the rules for the UI, to make it a little smoother and cleaner, which ties into the look of our UI.

## The Downside
If the player turns the music off, the animation can feel erratic and random. 

This is a problem when streamers with their own background tracks play the game.

## Finally
So that's the trick to our animation! 

Thanks for reading, I've got plenty more of Hidden Dogs to show in the future, so make sure you keep an eye on this devlog!