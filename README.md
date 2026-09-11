# Anthony Mattera - Game Developer / Technical Designer
I am a Game Developer specializing in Unity, focusing on technical complex projects such as VR/AR. I enjoy creating projects that stand out as unique compared to current market offerings. I’m passionate about collaborating with others and pushing the boundaries of game development into innovative and captivating experiences.
----

If you would like to see jump straight to some of the problems and solutions I've encountered during projects you can check **[here](#problems-solved-during-projects)**. or conversely you can just scroll down 

# Current Showcased Projects
## AR Puzzle Game: GEARS
<table>
<tr>
    <td valign="top" width="60%">
      <p>       A mobile + AR hybrid game partially inspired by Tetris, where the goal is to rotate gears into a "stuck gear" on the board to break it.

**Role in Development**: Designer and Developer-
Gameplay, UI, AR Foundation, 3D Modeling, Shaders

**Note:** Solo project

**In-Depth Description of role**
Developed from start to finish, this mobile AR hybrid game includes a 
- save/load system 
- custom Shaders 
- Ability to swap between AR/flat mobile mid gameplay


**Tools Used**
Unity, C#, Blender (for gear modeling), Shader Graph, AR Foundation

Play the Game: [Download GEARS APK](https://github.com/MatteraAnthonyJP/Anthony-Mattera-Portfolio/releases/tag/Gears)


</p>
    </td>
    <td align="center" valign="top" width="40%">
      <p><b>**Demo Video**</b></p>
      <a href="https://www.youtube.com/watch?v=sFGd83fBjbc">
        <img src="https://img.youtube.com/vi/sFGd83fBjbc/hqdefault.jpg" alt="Video Thumbnail" width="100%">
      </a>
    </td>
  </tr>
</table>



## Virtual Reality Blacksmithing Tech Demo

<table>
<tr>
    <td valign="top" width="60%">
      <p>       A VR tech Demo made to showcase designing meshes in real-time. 

**Role in Development**: Designer and Developer-
Gameplay, UI, XR Interaction toolkit, 

**Note:** Solo project.

**In-Depth Description of role**
Developed a VR tech demo
* data powered runtime mesh generation.
* An axis restricted multi-hand grab system
* A custom abstraction layer for physical controller button interactions for held object-dependent controls.
* A custom Shop system for a full gameplay loop
* As well as basic VR interactions including holsters, grabs, dials, levers, and locomotion mechanics.

**Tools Used**
Unity, C#, XR Interaction Toolkit, Shader Graph

**Demo:** For right now demo has to be individually requested

</p>
    </td>
    <td align="center" valign="top" width="40%">
      <p><b>**Demo Video**</b></p>
      <a href="https://www.youtube.com/watch?v=7_O5xNfPPn0">
        <img src="https://img.youtube.com/vi/7_O5xNfPPn0/hqdefault.jpg" alt="Video Thumbnail" width="100%">
      </a>
    </td>
  </tr>
</table>



## Educational Project - Drawing The Night Sky


<table>
<tr>
    <td valign="top" width="60%">
      <p>      An educational game created as a capstone project for a museum in Carter Lake, GA. The game helps children learn to identify constellations by connecting stars in the night sky using real star data from the Yale Bright Star Catalogue.

**Role in Development**: Data Validation, Gameplay logic.

**In-Depth Description of role**
- loading star data from a publicly available binary file
- implementing the gameplay functionality for connecting stars
- validating all connections to accurately form constellations. 

**Tools Used**
Unity, C#, json reading


Play the Game: [Download Drawing The Night Sky EXE](https://github.com/MatteraAnthonyJP/Anthony-Mattera-Portfolio/releases/tag/Drawing_The_Night_Sky)

</p>
    </td>
    <td align="center" valign="top" width="40%">
      <p><b>**Demo Video**</b></p>
      <a href="https://www.youtube.com/watch?v=GGBUJkl4HzU">
        <img src="https://img.youtube.com/vi/GGBUJkl4HzU/hqdefault.jpg" alt="Video Thumbnail" width="100%">
      </a>
    </td>
  </tr>
</table>
 


# Problems Solved During Projects:

## Gears AR/Mobile Game:

<img src="Images/OldGears.jpg" alt="Image of the original Design of the Game" align="left" width="250" />

### Further context regarding project
This version of the project actually started as a recreation of a college project i made that was rebuilt from the ground up to improve the gameplay, Latency, and Overall Visuals.

### Problem 1) Translation from Flat/AR
One of the main features was the ability to take the entire game board and toss it directly into AR space.

The basic setup was straightforward. Placement was handled by dropping the board onto whatever surface AR Foundation detected, and scaling was just a simple multiplier during the mode transition. The real challenge was actually controlling the game once it was there. 

### Solution 1)
One of the first things I did was have the actual Object rotate Towards the player when in AR Space. This allows you to always interact with the game 
To make touch placement feel natural relative to the user, I kept a grid oriented towards the player camera using Object.RotateTowards with a slight visual offset. It was a simple trick, but it made interacting in physical space easier and more responsive. On top of that in order to interact at all. I placed an invisible object placed directly behind the grid and stretching out far past the view of the screen in order to make placing the object less tedious.


<br clear="left" />

---

### Problem 2) The Rewrite
This problem is a bit more complicated on face value so I'm going to explain it here
At some point you are going to encounter a situation that would be physically impossible. Mainly a gear rotating and touching another gear that is turning the same direction. Now this may sound confusing at first, but there are exceptions built into the base game already. Mainly pieces that are physically connected using the black belt type connection shown in the demo. In the original version this would have all sorts of issues and in fact only checked its adjacent neighbors. It turned the game into more of a brick breaker type of game than the puzzle game it is now. 


### Solution 2)

<img src="Images/gears.gif" alt="Short GIF of the game running the BFS Algo" align="right" width="350" />

When it came time to deal with impossible scenarios. I didn't have very many options. I originally decided to only break pieces that broke logic, but that would cause the tile board to fill up way too fast eventually  breaking the game loop. Eventually I settled on designing a Breadth First Search Algorithm that queued up each individual piece of a gear set. While also keeping track of a alternating pattern among the Gears in order to determine which piece would be breaking logic. 

This actually became the main point of the game unlike the original which was to just make the randomly spawning gear turn in the appropriate direction. Eventually I even added a tracker into the BFS that kept track of the path back to the original starting gear.  Which allowed for me to create massive chains of breaking gears in a satisfying pattern tracing back all the way to the main spinning gear, and also a potential consequence if you make a wrong move. In a sense I turned my biggest problem into the main feature of the game.

<br clear="right" />

Another Link to the Full video of the demo: https://www.youtube.com/watch?v=sFGd83fBjbc

---

## VR Blacksmithing Game

Before jumping into the massive amount of things I want to talk about I just want to say this is the project I'm most proud of. There's a lot of complex work that went into it.

---
### Problem 1) Mesh Deformation Strategies

So This Project was actually something I have had planned out and just didn't find the time till recently to make, but one of the first issues I encountered was with the idea. I want to make a blacksmithing, but how can I do that without having massive calculations that tank performance?

### Solution 1)
<img src="Images/swordplay.gif" alt="Short GIF of the game running the BFS Algo" align="right" width="45%" />
In existing VR systems, dynamic deformation usually comes with heavy tradeoffs that ruin either performance or player agency. Here’s what I chose not to do and why:

1) High-Poly Mesh Deformation: Wastes vertex data, tanks VR performance, and makes physics calculations far too expensive.
2) Purely Visual Bump Mapping: Keeps performance high, but provides zero actual physical geometry for collision or physics simulations.
3) Pre-Determined / "Fake" Deformation: Sacrifices player input and agency by forcing a predetermined visual output.

I built a system where a flat surface acts as a dynamic cast for the weapon. The player directly defines midpoints, edge points, height, width, and material parameters to generate the mesh in real time.

Why this works:

1) Full Player Agency: Players get total control over designing the weapon's physical shape.

2) Scalable Performance: Geometry starts at 5 vertices and scales up procedural-style only as needed, keeping physics lightweight and framerates stable.

3) Runtime Flexibility: The lightweight mesh structure allows data to be modified or saved on the fly during gameplay.

---
### Problem 2) VR Controller Buttons
<img src="Images/vr con.png" alt="photo of a quest 3 controller" width="300" align="left" />

So this problem stems from how The XR toolkit (Unity's VR Solution) Is built. Its most likely easiest to explain after showing a picture of what a VR controller usually looks like button wise 



I want you to mainly focus on the X/Y buttons. So here's what is actually a problem. When you make something for VR opposed to other mediums you tend to need alot more interactions entirely dependent on the object you have held in your hand. The easiest example of such is a gun. First of all if you aren't directly holding a gun you wouldn't want to have control over a gun, but at the same time when you are holding it  You might have a trigger, but you could also have buttons like a safety or a magazine release. Unity's XR toolkit doesn't have a native way to give interactions to those Extra buttons IE X/Y built into it. So in a sense out of box theirs no way to make object dependent controls for these non Trigger based buttons

<br clear="right" />

### Solution 2)

This solution was highly straight forward actually. I created an event manager for each hand that was controlled based off predetermined buttons and button configurations(Hold down multiple buttons at once for a different interaction). I then created an inherited interactor (What gives you the ability to grab objects in VR) and setup the ability to hook directly into the hands events. This has multiple benefits
1) You only control the object you have grabbed
2) You can have multiple functions running on the same object without being hard coded
3) This is practically a developer tool and is plug and play which drastically speeds up development
4) Can be imported into other people's projects with minimal setup

Some images showcasing the plug and play nature of it in unity
<p align="center" style="display: flex; justify-content: center; gap: 10px;">
<img src="Images/vr2.png" alt="photo of plug and play nature" width="25%" />
 <img src="Images/VR 1.png" alt="photo of plug and play nature" width="40%" />

</p>

**Another Link to the Full video of the tech demo: https://www.youtube.com/watch?v=7_O5xNfPPn0**

---

## Drawing the Night Sky

My main role in this project was the backed initial work that went into actually making the game "function" My role regarding the visuals was extremely limited

---
### Problem 1) Showcasing Constellations

For this project the group was given nearly free reign of what we were allowed to do. We had only 2 requirements. It must allow you to draw real constellations, and it must be within a level of accuracy. So it should line up decently well with the actual night sky

### Solution 1) 
<img src="Images/night Sky.gif" alt="gif of the game" width="500" align="right" />

There were a few attempts to make this project. originally we came up with a map of the constellations projected onto a sphere that envelops the player. This had obvious downsides being that the scale looked off, and interactions were a nightmare. So I eventually went back and looked into something called the Yale Bright Star Catalogue which is a collection of visible stars. This is perfect since all constellation stars are considered bright stars So I took a binary file from Yale's own website and plugged in that data in to give a basic location, name, and vector position from the location. This allowed up to make a full visible map. I then cross referenced every star from the constellations we had picked in order to piece together the gameplay for accuracy



