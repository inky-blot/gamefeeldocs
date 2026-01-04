---
tags:
  - docs
weight: "10"
title: Unreal Basics
date: 2025-08-02T01:07:10.505Z
lastmod: 2026-01-04T15:40:33.579Z
---
> \[!note]\
> You can skip this page if you already know Unreal.

Unreal is a steep learning curve. Unlike Unity or Godot where you largely build your own project architecture, **Unreal already has a system for everything.** Having that functionality out-of-the-box lets you get something on-screen and looking great very quickly. **However, you then need specialized knowledge about how to use each sub-system.** This is less of an issue on a team, where the burden of expertise is shared; when working solo, all that burden falls back on you.

Be aware of the workload; this course doesn't allocate many hours to learning the technical side of this. If you are brand-new to commercial engines, or otherwise don't feel confident you'll make Unreal work, make the decision now to use a more comfortable engine.

Additionally, this project does not expect you to use any C++. It is heavily recommended that you stick to blueprints, as co-integrating the two will require you to know more of the engine.

## Object Architecture

Unreal heavily uses **inheritance**, the idea that a more generic class can be inherited from to make a more specific class. **Everything inherits from something.**

**Levels**, also called Maps, are exactly what they sound like.

**Blueprints** (`BP_`) are the building block of functionality. They exist as their own assets, and then can be instanced (placed in) the world. You'll use these for everything: prefabs, coding, combining objects, or handling events.

* **Actors** are a type of blueprint that represent anything that can be placed in the level.
  * **Pawns** are a type of actor that can be "possessed" by a player or AI.
  * **Characters** are a type of pawn that can also walk, run, or do things like a human or animal.
* **Components** are a type of BP that attach to an actor. There's two types:
  * **Scene Components** have a transform, which means they exist in space. If your component cares about where it is or what it looks like, it's a scene component.
  * **Actor Components** don't have a transform, meaning they don't physically exist in a level. If your component is meant to handle data or processing, it's an actor component.

Some common advanced blueprints you'll see are:

* **Interfaces, Macro Libraries, and Function Libraries** are optional ways to add to other blueprints.
* **Game Modes** are a blueprint that tells the game how to load each part of the game. DO NOT mess with this if you don't know what you are doing.
* **Controllers** are a blueprint that tells characters what to do. We use these to either bind player input to the player character or to control enemies. DO NOT mess with this if you don't know what you are doing.

## Blueprint Architecture

Blueprints inheriting from different parents might have different UIs or uses. At the very least, almost every blueprint can store **variables.**

### Placing

The **Viewport** window appears in any blueprint with a **transform.** This includes actors, characters, and scene components. In the viewport, you can move items around to tweak where they appear in space. You can also use the "Add" button in the Components window to add child blueprints, allowing you to attach things to your main blueprint.\
![](/ob/Images/Tutorial_Basics_1.png)

### Execution

Then there's **event graphs,** which appear in any blueprint that can do stuff. Here, you can add events, which are the majority of your gameplay programming. You can have as many event graphs as you want, so use them to organize your code.

**Nodes** are each their own "line of code" that does something. The white line stretching between nodes is called the **execution flow**, which tells the engine what order the code should be called. The other colored lines are called **data connections**, which send information from one node to the next.

**Events** are their own callable sections of code. First, the red event node is where you implement the event, meaning you tell the engine what you want to happen. Then, you can call the event by searching its name in the "Actions" context menu (right clicking the background, or dragging a connection off its pin), which should be a blue node. Note that each event can only be implemented once in each blueprint.

Additionally, there are special events called **callbacks.** Callbacks fire at predictable times, and you shouldn't fire them manually unless instructed to do so.

* **Event Begin Play** happens when the game begins.
* **Event Tick** happens each frame. Some frames take longer than others, so don't attach time-sensitive code to this event.
* **Event Async Physics Tick** happens each physics frame. Unlike standard ticks, the physics tick occurs at a stable speed, meaning time-sensitive code will run consistently.

You can **collapse** sections of code into subsections, letting you hide or reuse it. There's three main ways to do this:

* **Subgraphs**, sometimes called a collapsed graph, is like a little event graph inside your main event graph. Collapsed graphs turn a bunch of nodes into one node. However, they cannot be reused later.
* **Functions** are like subgraphs; when you call a function, the engine executes the code inside the function before moving on. They can be reused later, and can be called in blueprints that inherit from it.
* **Macros** are similar to functions, but instead of moving flow into the function, it literally replaces the macro node with whatever is inside. They are reusable, but cannot be called or overwritten in inheriting blueprints.

Finally, there's **dispatchers.** Think of a dispatcher as a mailing list full of events. When you call the dispatcher, it goes through the list, telling each one to fire. The mailing list starts out empty, but you can add or remove events from it through a process called **binding.** Because a dispatcher is just a mailing list, it doesn't care what events it's actually calling; you can change the list later and it'll still work. If this blueprint is attached to another one, the other can actually listen for the dispatcher too.
