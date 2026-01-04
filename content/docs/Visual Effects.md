---
tags:
  - docs
weight: "50"
title: Visual Effects
date: 2025-07-24T11:59:23.560Z
lastmod: 2026-01-04T15:41:39.773Z
---
**Niagara** is Unreal's visual effect system. Each Niagara system is its own asset, allowing it to be used like a prefab. Each system is comprised of one or more **emitters**, meaning you can have multiple particle styles or behaviors in the same system.

## Creating a Niagara System

Let's build a simple dust cloud when the character kicks. Add a new asset in your content drawer, and select Niagara.\
![](/ob/Images/VFX/Tutorials_VFX_1.png)\
In the following menu, choose a base for your system. I will use the **directional burst**.\
![](/ob/Images/VFX/Tutorials_VFX_2.png)\
Open the asset. On the graph, the blue node contains details about the whole system. The orange nodes are individual **emitters**. Each emitter spits particles out in a different way. We only want our system to play once, so select the blue node and find "Loop Behavior" in the details; set it to "once."\
![](/ob/Images/VFX/Tutorials_VFX_3.png)<span style="background:#ff4d4f">FINISH THIS. NEED ATTRIBUTION FREE CLOUD SPRITE.</span>

<div class="page-break" style="page-break-before: always;"></div>

## Playing VFX from Montages

To emphasize your animations, you can add VFX events to your montage files. This tutorial assumes you have (a) have made or acquired a Niagara asset and (b) you have made or acquired an animation montage.

First, we need a notify track. In your montage, **add a track** to your timeline.\
![](/ob/Images/VFX/Tutorials_VFX_4.png)\
If you right-click the track anywhere on the timeline, you can **add a notify**. In this case, we will use "Play Niagara Particle Effect."\
![](/ob/Images/VFX/Tutorials_VFX_5.png)\
You can move this notify left or right on the timeline to adjust its timing. I recommend pausing playback and scrubbing through the timeline. Find a good spot, and move the notify to the same time as your scrubber.\
![](/ob/Images/VFX/Tutorials_VFX_6.png)\
With the notify selected, set the "Niagara System" and "Socket Name" fields in the details window. The socket refers to where the effect should appear. Also consider whether you want your system attached (will move with the bone) or not (will appear at the bone, but won't move).\
![](/ob/Images/VFX/Tutorials_VFX_7.png)\
Finally, resume playback. You should now see your VFX appear.\
![](/ob/Images/VFX/Tutorials_VFX_8.gif)

\#docs \${docs}
