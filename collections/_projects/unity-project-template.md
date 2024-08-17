---
title: Unity Project Template
categories:
    - Unity Project Template
project-page-sort-id: 103
excerpt: "Rapidly configure default Unity packages and rendering with a template."
header:
    overlay_image: "/assets/images/code.jpg"
    teaser: "/assets/images/code.jpg"
---

*This project was worked on between March & April in 2024.*

*This article was written in August 2024.*

# Summary
Since starting working in Unity, I've wanted accelerate the setup of new projects.

I've written a few helper scripts that do this, and made them available on GitHub. These scripts are bundled into a Unity Template, and run from the Unity Editor.

[GitHub Repo: Unity 3D URP Project Template](https://github.com/AdmiralEgg/Unity3DURPProjectTemplate)

[GitHub Repo: Project Template Creator](https://github.com/AdmiralEgg/UnityStandardConfigCreator.u)

Included in the Template are some GitHub Action files, which set up builds of Unity on GitHub via GitHub Actions.

# Project Template Features
- Instantly deploy a new Packages manifest, which automatically installs a number of key packages: URP, VFX Graph, Shader Graph, the new Input System, and more.
- Add new default scene, with a standardised GameObject hierarchy.
- Add a standard directory hierarchy to the Assets directory.
- Setup basic URP rendering and, and configure lighting to realtime by default.
- Add a basic spinning cube to check your build works.

# GitHub Build Actions
- Trigger a 'Build Unity Project' action to build your project for multiple different platforms.
- Overnight scheduling which runs builds overnight if there are changes in your repo.
- Trigger a 'Publish to Itch' action to use Butler to push your builds to an Itch page.
- Trigger a 'Notify Discord' action to notify a Discord channel that a new Itch build is available.

# Conclusion
This project has helped me lock down my standard development process for new prototypes. It enables me to get started quickly, without losing focus on what I want to achieve. 

The Spinning Cube project (built in a day) is a great example of the template in action.

The GitHub Actions are used for all my project builds, and connect to my Discord for notifications.