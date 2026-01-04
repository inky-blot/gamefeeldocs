---
tags:
  - docs
weight: "30"
title: Mesh Assets
date: 2025-07-17T18:21:22.021Z
lastmod: 2026-01-04T15:41:11.091Z
---
Mesh assets are the geometric information about a 3D object. Any 3D object visible in-game will require a mesh.

## Types of Mesh

There are two types of mesh.

* **Static meshes** don't bend or deform naturally, so you have limited options to animate them. These are the meshes you use for environments and such.
* **Skeletal meshes** have bones and a skeleton, meaning somebody took the time to make sure the model could bend and twist and all that. These are what are used for characters, usually.

> \[!note]\
> For this project, you are encouraged to use **skeletal meshes** for your weapons and characters whenever possible.

The skeleton your character uses is very important, as it determines which animations work with it.

* By default, this project uses **X Bot**, which is Mixamo's standard. It is compatible with most or all animations available on Mixamo. You can swap the model freely with any model on Mixamo.
* Included in the project is also **Manny**, which is Unreal's standard. It should be compatible with a lot of the animations available on Fab (the Unreal asset store). You can swap the model freely with some of the models on Fab or online.

One quirk of Unreal is that mesh blueprints must be either skeletal or static.\
By default, the template weapon blueprint is **based on skeletal meshes**.\
We can convert a static mesh to a skeletal mesh when **importing the FBX.**

### STS: Converting static to skeletal

First, hit the "Import" button. Find the FBX for your weapon (it is likely in your downloads folder, if you got it online).\
![](/ob/Images/Skeletons/Tutorial_Skeletons_1.png)In the subsequent modal, you need to **check "Skeletal Mesh."** This tells Unreal to convert it. If you do not give it a skeleton, Unreal will make a very simple one for it. Make sure you rename your new assets.\
![](/ob/Images/Skeletons/Tutorial_Skeletons_2.png)\
In your weapon's blueprint, find **Mesh in in the Class Defaults menu**. Set it to the skeletal mesh you just created.\
![](/ob/Images/Skeletons/Tutorial_Skeletons_3.png)

***

## Sockets

**Sockets** are a named "snap point" added to a skeleton. Using sockets, a weapon can be held or otherwise bound to different parts of the mesh.

### STS: Creating a socket

Open the skeleton asset. We need to **find a bone near** where we want to hold the item. I'm going to use the `RightHand` bone.\
![](/ob/Images/Skeletons/Tutorial_Skeletons_4.png)\
Right-click the bone and **add a socket**.\
![](/ob/Images/Skeletons/Tutorial_Skeletons_5.png)\
**Change the name** of the socket. Name it something easy to remember and copy! Try not to change this name later.\
![](/ob/Images/Skeletons/Tutorial_Skeletons_6.png)\
Jump back to your character blueprint (by default, `BP_FirstPerson`). On your weapon component, **find the socket field** in your details panel. Click the folder with a magnifying class icon, then choose the correct socket.\
![](/ob/Images/Skeletons/Tutorial_Skeletons_7.png)Finally, we can adjust the positioning. **You can either move the socket directly in the skeleton menu** (tricky to do because you can't preview the output, but super clean and reusable) or **add local transforms to your weapon component** (messier but easier to preview).

\#docs \${docs}
