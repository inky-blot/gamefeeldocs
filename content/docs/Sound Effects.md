---
tags:
  - docs
weight: "60"
title: Sound Effects
date: 2025-07-30T00:47:02.880Z
lastmod: 2026-01-04T15:41:47.866Z
---
This template uses the default sound engine in Unreal. We did not prebuild support for FMOD or WWISE, and we heavily discourage adding them yourself.

Spatialized audio means sounds that are literally emitted in space. Most sound effects are spatialized; audio without a physical representation, like UI sounds or background music, are not spatialized.

### Good to Knows

When you import a sound, such as a .WAV file, it begins as a **Sound Wave asset**. We suggest prefixing your waves with `A_`. Then, you can right-click the asset and select "Create Cue." A **Sound Cue asset** contains additional mixing information that can come in handy. We suggest also prefixing this as `A_` and suffixing as `_Cue`. \*\*Cues are optional.

Also, **Unreal caps out at 32 simultaneous sounds.** It's okay (albeit bad practice) to spawn ungodly numbers of sounds as long as they are super short (and thus don't occupy your sound limit very long).

## Background Music

Your **default** scene already has a `BackgroundMusic` object. To change it, just select **"Sound/Sound"** on your details panel. If it isn't already disabled, feel free to disable "Attenuation/Allow Spatialization". **If you need more control over the audio**, either remove the Sound Class Override or change the values within the Sound Class asset.\
![](/ob/Images/SFX/Tutorials_SFX_1.png)

<div class="page-break" style="page-break-before: always;"></div>

## Audio Components

Sound, spatialized or not, is created by adding audio components to an object. **Noise made by enemies, bullets, or other distant events should be spatialized,** when possible.

Each sound effect should be its own Audio component. You can add one to your blueprint via the **Add button on your Components window**.\
![](/ob/Images/SFX/Tutorials_SFX_2.png)\
You can move the audio asset in your viewport. It can also be useful to place the sounds in an empty scene component to keep you organized or let you move sounds en masse.

You need to change the sound settings!

* **Sound/Sound:** Changes the sound to play.
* **Sound/Pitch Multiplier:** Be aware: you need to randomize the pitch yourself through blueprints!
* **Attenuation/Allow Spatialization:** Failing to turn this on will de-spatialize the audio.
* **Activation/Auto-Activation:** Failing to turn this off will cause the sound to play undesirably when the game loads.

To play these sounds, drag the component into your event graph. Use the **Play node** to activate it.\
![](/ob/Images/SFX/Tutorials_SFX_4.png)

<div class="page-break" style="page-break-before: always;"></div>

## Animation Notifies

You can add **animation-specific sounds** to a montage using **animation notifies**. This is useful for timing sounds, such as grunts.

To do so, open your Montage asset. Hover over the "Notifies" track label and hit "Add Notify Track." Right click on the newly created track in the timeline and hit "Add Notify," and then "Play Sound." You can set a desired sound in the Details panel under "Anim Notify/Sound."\
![](/ob/Images/SFX/Tutorials_SFX_3.png)

If using animation notifies, **you must assign an attenuation profile to your sound cue.** If you don't, the audio will not spatialize at all. Open your Sound Cue asset; find **"Attenuation/Attenuation Settings"** in the Details panel and add an attenuation profile.

## Sound Attenuation Profiles

If you cannot find the default ATT that comes with your project, they are fortunately easy to make. **Create a Sound Attenuation asset** from your Content Drawer. The suggested prefix for this file is `ATT_`. The **default values are fine** for this project.

If your character is moving quickly or you want hyper-real sound mixing, set "Attenuation (Volume)/Attenuation Function" to Inverse. If your sounds rise or fall too quickly, set it to Linear.

\#docs \${docs}
