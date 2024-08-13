---
title: Player Navigation with the Dynamic Light System
tags:
    - Systems
categories:
    - Echoes
---
Work in Progress.

- System not extensible enough
- Colour, intensity, flicker, set default
- Light 'Groups' and individual lights
- Groups of lights triggered with same values.
- Lots of limitations to the system, but not inherantly a bad thing.

- System setup; DL Actor, DL Interface, DL System, EnumLights, EnumGroups. Interface attached to any actor that needs to trigger lights, sends events which are picked up by the system. System checks a table (DataTable) to lookup the actor based on an Enum.

- Problem: Adding new lights not designer friendly