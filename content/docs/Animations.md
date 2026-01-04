---
tags:
  - docs
weight: "40"
title: Animations
date: 2025-07-17T18:33:15.054Z
lastmod: 2026-01-04T15:41:27.277Z
---
Animations are a little tricker in Unreal than other commercial engines. This page is for animating skeletal meshes; to animate static meshes, use a level sequence. This guide centers **Mixamo** animations. If you are using animations from other sources and get lost with these steps, talk to a TA for help.

### Quick Start

If your animation only plays once when called, i.e. attacks or getting hit, use \[animation montages]\(#Animation Montages). If your animation loops until something changes, i.e. running or dying, use \[ABP state machines]\(#State Machines).

## Sequences

An animation sequence is just an animation clip. It stores the data for singular animations.

You can get these clips from Mixamo. Hit the download button, and download **without skin.** This means it's just downloading the poses, not the full mesh.\
![](/ob/Images/Anim/Tutorial_Anim_1.png)\
Then, go to Unreal. Import the FBX with the **Import button** in the Content Browser. It should bring up the following pop-up. You **must**: (a) select a **compatible skeleton** (if it's from Mixamo, use `SKEL_Xbot`); (b) **import it with a Z rotation of -90** (otherwise it will be sideways).\
![](/ob/Images/Anim/Tutorial_Anim_2.png)\
Finally, rename the asset. The standard used in this project is `A_AssetName` (the prefix A\_ is used for all animation sequences).

<div class="page-break" style="page-break-before: always;"></div>

## Animation Blueprints

Animation blueprints, or ABPs, are the brains of Unreal blends animations. The idea is that you have a base pose, which plugs into nodes that modify or blend it, which plugs into the output.

> For animations that change based on a variable (i.e. `bIsRunning`), use a state machine. For animations that play once when an action happens, use an animation montage.

First, create an ABP from your Content Browser. It will ask you which skeleton to use; **use the same skeleton as your animation sequences.** In Mixamo's case, that is `SKEL_Xbot`. You should now see something similar to this.\
![](/ob/Images/Anim/Tutorial_Anim_3.png)\
**Output pose** tells the engine what to actually show in-game. To give it a pose, we need to add an animation to it. The simple way to do this is to **drag an sequence into the graph, and connect it.** When the preview on the left tells you to, recompile the animation and it should show up now.\
![](/ob/Images/Anim/Tutorial_Anim_4.png)

## State Machines

This is how you connect animations that **play based on variables**. An example of this is switching between an idle and running animation.

Start by making a state machine. Right click the background and look up "state machine." Connect the pin to the output pose.\
![](/ob/Images/Anim/Tutorial_Anim_5.png)\
You can double click to enter the state machine. You will see only an **entry** node; that will connect to your starting state. **Add states by dragging sequences from Asset Browser or Content Browser windows.** Your cursor will have a bad symbol on it; don't worry -- that just happens for some reason.\
![](/ob/Images/Anim/Tutorial_Anim_6.png)\
Think of each state as one animation you want. We need to connect between them to switch between. If you drag from the light gray border of each state, you can make **transitions.** They only go one way -- if you want to go back and forth, you need two transitions.\
![](/ob/Images/Anim/Tutorial_Anim_7.png)\
Now, we need to tell it when to switch. If you double click on the transition, you can add a **rule.** When you plug "true" into the result, the transition will start. **You can make variables for this in the variables tab on the left in "My Blueprint".**

> \[!warning] Troubleshooting\
> **The rule has to evaluate to true to happen**. This means if you want the transition to happen if a variable is false, you should hook it up as GET VARIABLE -> NOT -> RESULT.

![](/ob/Images/Anim/Tutorial_Anim_8.png)\
Once you've added both rules, you can test your state machine. Compile the blueprint; the preview window should automatically start. By default, my character begins in idle. I can then use the "Animation Preview Editor" tab to click the boolean on and off. **If your animation isn't looping, double click your animation state and make sure Loop is turned on.**\
![](/ob/Images/Anim/Tutorial_Anim_9.png)

<div class="page-break" style="page-break-before: always;"></div>

## Animation Montages

This is how you connect animations that **play when an event happens.** These are a little tricky, so try to pay attention to the examples in the project.

First, we need to add an **animation slot**. They aren't intuitive, but it lets us override parts of the source motion (the usual pose for your character). *You can use a state machine as a source motion*.\* Go to **Window** at the top of the editor, find "Anim Slot Manager."![](/ob/Images/Anim/Tutorial_Anim_10.png)\
In the slot manager, **add a new slot.** I called mine "CharacterAction". Note that slots appear for any asset using the same skeleton, so you can reuse them.\
Then, **add a slot node between the source motion and the output.** Right-click the background and type in "slot"; you will see a Default Slot node. Add that, then look at details on the right. Swap the slot to the one you just made. All together, it should look like this.\
![](/ob/Images/Anim/Tutorial_Anim_11.png)\
Now, we need to create an **Animation Montage** asset. Go to your content browser and search "Animation Montage." It'll ask you for a skeleton to use; **use the same skeleton as your animation sequence**. Make sure you name the new asset (`AM_Name` is the standard recommended for this project).\
![](/ob/Images/Anim/Tutorial_Anim_12.png)\
In the new window that spawns, you need to **make sure that you are using the right slot**. On the timeline (seen below), there is a dropdown on your slot field. Click it, go to "Slot Name," and **choose the slot you created**.\
![](/ob/Images/Anim/Tutorial_Anim_13.png)\
Then, **drag your animation sequence** from the Asset Browser or Content Browser to **add it to the timeline**.\
![](/ob/Images/Anim/Tutorial_Anim_14.png)

<div class="page-break" style="page-break-before: always;"></div>

## Animation Notifies

Montages aren't just for animating; they have gameplay purposes as well. **Notifies** are a blueprint class that can be called from the "notifies" track in montages and other animation assets.

Unintuitively, the workflow for notifies is: broadcast notify from montage -> notify asset calls event on mesh owner -> mesh owner executes event.

\#docs \${docs}
