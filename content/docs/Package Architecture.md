---
tags:
  - docs
weight: "20"
title: Package Architecture
date: 2025-12-21T21:47:05.063Z
lastmod: 2026-01-04T15:40:39.424Z
---
> \[!important]\
> This section is the most important information in this documentation. It is recommended you at least skim this page before starting and/or asking for help.

All template related objects will be located in the top-level folder, \content\template.

* Top-level blueprints (i.e. `BP_Player` and `BP_Enemy`) should be used as containers -- a place to combine your components.
* Individual behaviors have been encapsulated to components (i.e. `BP_DamageableComponent`).
  * To pass information up (i.e. from a component to its container BP), use a **dispatcher**.
* Weapons inherit from `BP_Weapon`, which inherits from Skeletal Mesh Component.
  * To add a weapon to the player, attach it as a child of the first person mesh.
  * Switching between weapons is handled by the `BP_WeaponManagerComponent`.
  * To make your own weapons, you should make a **COPY OF** `BP_GenericWeapon`. Copying it will preserve all the code inside, which you can use as a template.
  * All weapons are given **lifetime events** and relevant dispatchers, which can be used for setup or for listening for .
* Lifetime events for **attacks** are included in each BP inheriting `BP_Weapon`.
  * Each attack has been given an event graph for organization.
  * Calling lifetime events occurs semi-automatically in the template.
  * One condition: somewhere you must call **Event Attack End** or you'll get stuck in the attack!
    * You can call the event through blueprints or use the existing animation notify, `BPN_AttackEnd`.
* Thrown weapons are unique. Any weapon that throws itself should be divided into a component (inheriting `BP_Weapon` and held by the player) and an artifact (inheriting `AActor` and spawned when thrown).
* By default, `BP_Player` and `BP_Enemy` implement interfaces that allow them to receive damage and knockback from certain attacks. If you add more enemies or physics actors, check if they need to implement any interfaces.

# Importing the Template

The UE5 template for Game Feel is distributed as a .zip file. Extract the archive to `[project_directory]\content`.

Windows includes a in-built extract function; it is found in the context menu if you right-click the archive in File Explorer. Alternatively, free archive tools like 7zip and WinRar can be found online. These tools are third-party and are not affiliated with DigiPen.\
https://www.7-zip.org/\
https://www.win-rar.com/

\#docs \${docs}
