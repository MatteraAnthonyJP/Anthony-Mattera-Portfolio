# Anthony Mattera - Game Developer / Technical Designer
I am a Game Developer specializing in Unity, focusing on technical complex projects such as VR/AR. I enjoy creating projects that stand out as unique compared to current market offerings. I’m passionate about collaborating with others and pushing the boundaries of game development into innovative and captivating experiences.
---

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
Developed from start to finish, this mobile AR hybrid game includes a save/load system, custom Shaders, and an experience that can adapt between augmented reality and traditional flat-screen modes during gameplay


**Tools Used**
Unity, C#, Blender (for gear modeling), Shader Graph, AR Foundation

Play the Game: [Download GEARS](https://github.com/MatteraAnthonyJP/Anthony-Mattera-Portfolio/releases/tag/Gears)

***File is an APK***

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

**Demo:** For right now demo has to be individually requested

**Tools Used**

Unity, C#, XR Interaction Toolkit, Shader Graph

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
Responsible for loading star data from a publicly available binary file, implementing the gameplay functionality for connecting stars, and manually validating all connections to accurately form constellations. 

**Demo Video**


***File is zipped .exe***


**Tools Used**
Unity, C#, json reading


Unity, C#, XR Interaction Toolkit, Shader Graph

Play the Game: [Download Drawing The Night Sky](https://github.com/MatteraAnthonyJP/Anthony-Mattera-Portfolio/releases/tag/Drawing_The_Night_Sky)

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

### Problem 1) Translation from Flat/AR
One of the main features was the ability to take the entire game board and toss it directly into AR space.

The basic setup was straightforward. Placement was handled by dropping the board onto whatever surface AR Foundation detected, and scaling was just a simple multiplier during the mode transition. The real challenge was actually controlling the game once it was there. 

### Solution 1)
One of the first things I did was have the actual Object rotate Towards the player when in AR Space. This allows you to always interact with the game 
To make touch placement feel natural relative to the user, I kept a grid oriented towards the player camera using Object.RotateTowards with a slight visual offset. It was a simple trick, but it made interacting in physical space easier and more responsive. On top of that in order to interact at all. I placed an invisible object placed directly behind the grid and strechting out far past the view of the screen in order to make placing the object less tedious.


### Further context regarding project
This version of the project actually started as a recreation of a college project i made that was rebuilt from the ground up to improve the gameplay, Latency, and Overall Visuals.
<img src="Images/oldGears.png" alt="Image of the original Design of the Game" width="300" />


### Problem 2) The Rewrite
This problem is a bit more complicated on face value so I'm going to explain it here
At some point you are going to encounter a situation that would be physically impossible. Mainly a gear rotating and touching another gear that is turning the same direction. Now this may sound confusing at first, but there are exceptions built into the base game already. Mainly pieces that are physically connected using the black belt type connection shown in the demo. In the original version this would have all sorts of issues and in fact only checked its adjacent neighbors. It turned the game into more of a brick breaker type of game than the puzzle game it is now. 

### Solution 2)
When it came time to deal with impossible scenarios. I didn't have very many options. I originally decided to only break pieces that broke logic, but that would cause the tile board to fill up way too fast eventually  breaking the game loop. Eventually I settled on designing a Breadth First Search Algorithm that queued up each individual piece of a gear set. While also keeping track of a alternating pattern among the Gears in order to determine which piece would be breaking logic. This actually became the main point of the game unlike the original which was to just make the randomly spawning gear turn in the appropriate direction. Eventually I even added a tracker into the BFS that kept track of the path back to the original starting gear.  Which allowed for me to create massive chains of breaking gears in a satisfying pattern tracing back all the way to the main spinning gear, and also a potential consequence if you make a wrong move. In a sense I turned my biggest problem into the main feature of the game.

<img src="Images/gears.gif" alt="Short GIF of the game running the BFS Algo" width="300" />

Another Link to the Full video to the demo: https://www.youtube.com/watch?v=sFGd83fBjbc


## VR Blacksmithing Game

Before jumping into the massive amount of things I want to talk about I just want to say this is the project I'm most proud of. There's a lot of complex work that went into it.

### Problem 1) Mesh Deformation Strategies
So This Project was actually something I have had planned out and just didn't find the time till recently to make, but one of the first issues I encountered was with the idea. I want to make a blacksmithing, but how can I do that without having massive calculations that tank performance?

### Solution 1) 
What Ive seen in the field is a large amount of designs that have tradeoffs and honestly they usually hurt the end user and the capabilities of the final product more than they are worth. So lets talk first about what I **didn't do**. 
1) I didn't deform a mesh with a large amount of pre-made extra vertices. This would tank performance make it very difficult to do physics calculations, and guess what it would make most of the mesh data go to waste. Not to mention in VR this is very difficult to Make fun and its too complex for most people to enjoy.
2) I didn't make the deform purely visual using bump maps. This would be better for the performance, but if the ultimate goal was to have the output be usable in physics simulations this would be terrible
3) I didn't fake it. I didn't want the output to be per-determined meaning the user is just a passenger and doesn't have much input in the outcome

So what I Actually Did is Build a mesh using a flat surface acting as a cast for the weapon. allowing the user to point to and specify mid points,Edge Points, height, weight, width, and materials. 
Advantages of this approach
1) The User Gets to choose the shape
2) Performance issues build up instead of down. You aren't forced to have 10,000 vertices. You start with 5 and work up towards that 10,000 ( not that you'd ever reach it)
3) Beginner friendly. All it takes is moving some points and changing some dials and even a child could design something of their dreams.
4) Its Lightweight meshes meaning physics calculations can be super efficient compared to others.
5) This also allows me to save and do changes mid gameplay. Allowing for a future system I'd like to implement. That is both highly compatible and built on top of my current work.

   
### Problem 2) VR Controller Buttons
<img src="Images/vr con.png" alt="photo of a quest 3 controller" width="300" align="right" />

So this problem stems from how The XR toolkit (Unity's VR Solution) Is built. Its most likely easiest to explain after showing a picture of what a VR controller usually looks like button wise 



I want you to mainly focus on the X/Y buttons. So heres what is actually a problem. When you make something for VR opposed to other mediums you tend to need alot more interactions entirely dependent on the object you have held in your hand. The easiest example of such is a gun. First of all if you aren't directly holding a gun you wouldn't want to have control over a gun, but at the same time when you are holding it  You might have a trigger, but you could also have buttons like a safety or a magazine release. Unity's XR toolkit doesn't have a native way to give interactions to those Extra buttons IE X/Y built into it. So in a sense out of box theirs no way to make object dependent controls for these non Trigger based buttons

<br clear="right" />

### Solution 2)

This solution was highly straight forward actually. I created an event manager for each hand that was controlled based off predetermined buttons and button configurations(Hold down multiple buttons at once for a different interaction). I then created an inherited interactor (What gives you the ability to grab objects in VR) and setup the ability to hook directly into the hands events. This has multiple benefits
1) You only control the object you have grabbed
2) You can have multiple functions running on the same object without being hard coded
3) This is practically a developer tool and is plug and play which drastically speeds up development
4) Can be imported into other people's projects with minimal setup

Some images showcasing the plug and play nature of it in unity
<p align="left" style="display: flex; justify-content: center; gap: 10px;">
<img src="Images/vr2.png" alt="photo of a quest 3 controller" width="25%" />
 <img src="Images/VR 1.png" alt="photo of a quest 3 controller" width="40%" />
</p>





