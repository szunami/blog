---
layout: post
title:  Jump Emblem
tag: unity, gamejam, gamedev, c#
---

This past week I participated in the [Newbies Game Jam](https://itch.io/jam/newbies2) and built a game (a demo really) called [Jump Emblem](https://itch.io/jam/newbies2).

### Game Design Notes

I love tactics games (Into the Breach, Fire Emblem, Advance Wars) and wanted to explore the design space. Early in the day, I was thinking about making a 2D platformer with tactics-style movement; I was stunned when I discovered that this jam had a suggested genre of `Tabletop Platformer`. I knew this coincidence was too cosmic to ignore, so I decided to go for it.

This jam convinced me that this design space is wide open and there are some fun ideas to explore. Unfortunately, due to time constraints, I didn't get a chance to explore the space fully.

A couple (unimplemented) mechanics to jump off from this demo:
1. What if there is an enemy that is trying to block you from reaching the goal?
2. What if you have multiple units that have different movement constraints?
3. What if different platforms move differently?

This demo also left some other key questions unanswered:
1. What is the player's goal? Why?
2. Are there enough interesting challenges to keep the game fun and interesting? Would the mechanics lead to puzzles that are overly rigid and tedious?


### Implementation Notes

I wanted to build this demo using Unity and have the game be playable on mobile web browswers. I am fairly new to Unity and C#, so some of my bigger pain points might be due to my unfamiliarity with the available options.

I wanted this game to be playable on mobile, so I decided to rely on button presses rather than keyboard inputs. This meant that my entire game was essentially a bunch of buttons with related state.

During this jam, I struggled to develop a pattern of how this state should be updated. I ultimately stored some state within each button and some state living in a global GameState game object. For the scope of this demo, this was fine; I can imagine that in a larger project this would quickly get out of hand.

In some of my scripts, I added callbacks to buttons using C# `delegates`. This worked okay, but I quickly ran into some bugs where variables in my delegates were getting modified in the scope that they were created in. I am more used to working in React, where there is a more formal way to express data dependencies via state, props, and hooks.

I also struggled to have buttons affect other buttons; for example if you move to location `(0, 1)`, the other movable location buttons should disappear. To achieve this, I had each button check if they should be destroyed in their `Update` method. This felt dirty but it got the job done.