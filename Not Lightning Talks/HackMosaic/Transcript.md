## What is Unity?
Unity is a cross platform game engine that enables you to make 2D or 3D games for multiple systems (mobile, pc, consoles). Pokemon Go is one! A game engine is basically a framework that takes care
of the of the heavy lifting of game development, saving you time. It'll handle things like graphics, so you don't have to handle lighting all the time, handling of input types (mouse? keyboard? joystick?),
and physics (give a thing gravity). Unity gives you an editor to make your game, and has simple capabilities in terms of graphic creation and modeling. If you want to make a sprite (2d graphical component) or some elaborate component, you'll probably
want another tool to do this (like Maya).

For scripting, Unity gives you the option of either 
 - C#: Unity is bundled with Mono (Open source cross platform .NET) and uses their C# compiler. However, it's using an older runtime, which is roughly equivalent to .NET 2.0 (runtime that C# uses, made in 2005), which means
 not all of C#'s features are available. You can use up to C# 3.5.
 - or JavaScript (sometimes called UnityScript) which is vastly different from ECMAScript/what you use for the web.

 You have two options for working on scripts: MonoDevelop or Visual Studio


## Unity Editor
The editor can be split up into sections:
- The toolbar is for playing your scene, and has tools for altering the position and size of your game objects. 
- The hierarchy window is where game components are placed
- The scene view is a static visual representation of your developing game
- The inspector is used for adding and altering components on your game objects
- The project window contains all assets (scripts, music, art)

## Making the Platformer

[Project already exists and we'll be putting bit by bit in there]

## 0 - Setup

We'll put the hero in our scene hierarchy since this will be the thing we control. Consider resetting your transform so the position is at 0 for your x/y/z coordinates and
everything is in the center, can make things more manageable.

## 1 - Center player on camera

First thing we do is center the camera on the player. You do this by simply putting the camera
in the scene hierarchy UNDER the player so that the camera is following the player when you set the camera's x/y coordinates to 0. 

## 2 - Make the hero move

Then we'll add our first script: SimplePlatformController. There's a few key things here to note. We have the HideInInspector attribute that hides variables that are unnecessary. Second let's talk about this 2D rigidbody, which will be our hero. How does Unity know? Well when we add this script to thehero, the GetComponent() function looks for the specific type of the game object that the script will be added to. So it's looking for that rigid body, and it's the only rigid body here, and you can't add more than one here. Unity knows this and nicely links this up for you. Like I mentioned before, rigid bodies act under the law of physics, so you'll see in FixedUpdate() we're adjusting the hero's speed/velocity and forces acting on it in this physics loop. We're grabbing the horizontal axis, setting the speed, setting the force in both direction, make sure the rigidbody doesn't go too fast, and make sure we're not facing one way and moving the opposite way. Last thing here is in Update(), where we are taking that Transform variable and doing a thing here called linecasting. Linecasting connects two points, start and end. Here we're casting our line against 
just the ground layer. We need it to tell us if we're on the ground so we can know if we can jump (no double jumping here).

Scripting is done, so when we add this script to the hero, and add a horizontally stretched a 2d cube to the ground layer, which will be under the hero, the hero now falls on the
"ground" and can jump with the space bar.


## 3 - Spawn the ground with SpawnManager Script

So now we want the hero to be able to jump from platform to platform, so we'll spawn these stretched cubes. First we'll make it into a prefab, which is just a template game object that can be reused. I dragged it into my prefabs folder to do this. All its components and properties will remain the same, so no need to alter each one. If you change something in one game object that is a prefab,
it will change all the other game objects (you can override this for one specific prefab if you wish). So now we'll write a script to spawn.So we'll spawn the max number of platforms, spawn platforms in within the bounds that the player can jump vertically and horizontally. Next we'll set an origin position which will be the last platform that was spawned, the first platform will be the one that's already there. The spawn loop just makes a platform to the right of the next platform.

In the editor, set the ground to be the platform, and now the hero can jump from platform to platform.


## 4 - Add a coin

Next, we'll add some coins. Essentially we're expecting the coins to disappear when the hero touches it. So we'll set that up by adding the coin sprite to our scene, add a 2D circle collider component and check the trigger box so that we do something when the hero comes into contact with the coin's collider radius. The collider radius is customizable. In a script we'll basically tell the coin to
destroy itself if the hero touches it.

## 5 - Spawn coins

Just one coin is boring, so let's add more. Just like the ground we'll want to spawn these coins. We'll need to make a coin prefab, and then give the coin some spawn locations relative to the platforms. We want to avoid spawning coins in a spot where the player can't reach it. To do this, we'll make some transform game objects to be children of the ground in our scene hierarchy. Next, a script to
spawn our coins randomly by taking those 4 transforms, putting them in an array, and randomly choosing an index which will determine where the next coin will spawn. 
