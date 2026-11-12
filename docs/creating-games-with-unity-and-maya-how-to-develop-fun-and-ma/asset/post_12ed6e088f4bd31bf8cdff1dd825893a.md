
**FIGURE 15.28** Problem with triggers; the raycasting is “seeing” the triggers, and triggering our EMP on them as well.

![](img/0285f88bc840f313779e011725b623a5_457_0.png)

### Layers

This is an annoying, but fixable, predicament. The triggers need to have a collider on them or they won’t work as colliders. But the colliders are what cause the raycasting to see them, and then the ghosted EMP to crawl up the sides of these imaginary objects.

Luckily, the fine folks at Unity have foreseen such troubles and created a method of allowing objects to live on layers. These layers aren’t like Photoshop layers—they don’t actually (by default) live in a particular order over the top of each other. But they are very handy for Unity mechanisms that “see” things.

For instance, cameras and lights can be told to only “see” certain layers. For lights this means that a light might illuminate certain objects (that are on certain layers) and not illuminate adjacent objects (that are assigned to different layers). It means that a camera could be told to ignore certain layers and thus not to draw some objects that exist in the scene. This can be a handy way to handle things like X-rays or night-vision goggles.

In the case of raycasting this can be very important. Via script, a raycasting mechanism can be told to ignore certain layers, or, lucky for us, there is already an Ignore Raycast layer that does some of this for us.

If an object, like a trigger, is assigned to this Ignore Raycast layer, all raycasting functions see right through the object (they don’t stop the ray).

Which layer a GameObject is assigned to is seen in the Inspector and is right next to the Tag drop-down menu. Creating new layers is actually within the same mechanism as creating new tags (use the Layer drop-down menu to select Create New Layer). We aren’t going to be doing much with layers for this project, but be aware that it’s there.

- **Step 21:** Assign each of the triggers to the layer Ignore Raycast. Do this by selecting each trigger in the Hierarchy and then using the Layer drop-down menu (Figure 15.29).

![](img/0285f88bc840f313779e011725b623a5_458_0.png)

FIGURE 15.29 Adjusting the trigger's layer so they won't be seen by the raycasting mechanism.

### Make the EMP Effective

So now we can place the EMP. This visually explodes, but we need to make it actually do something. The first thing we need to do is check if the EMP has been placed within a certain distance of the keypad. If it has, it needs to short the keypad out. We'll indicate that by changing the color of the texture on the keypad, turning on some smoke, and then opening the doors.

We can nest all of this within the ExplodeEMP function. But first we need to create some variables to hold everything.

- **Step 22:** Create public variables for keypadLock, keypadSmoke, entryWayLeftDoor, and entryWayRightDoor. Place them all at the beginning block of the script:

```
var keypadLock : GameObject;
var keypadSmoke : GameObject;
var entryWayLeftDoor : GameObject;
var entryWayRightDoor : GameObject;
```

- **Step 23:** Down in the ExplodeEMP function, add the following code:

```
function ExplodeEMP(placedEMP:GameObject) {
    yield WaitForSeconds (2);
    placedEMP.audio.enabled = true;
    placedEMP.GetComponent("Detonator").enabled = true;
    placedEMP.renderer.material.color = Color (0,0,0);
    if (Vector3.Distance(placedEMP.transform.position,
    keypadLock.transform.position) <= 1) {
        keypadLock.renderer.material.color = Color (.5,.5,.5);
        keypadSmoke.active = true;
        iTween.RotateTo (entryWayLeftDoor, Vector3 (0,45,0), .8);
        iTween.RotateTo (entryWayRightDoor, Vector3 (0,-45,0), .8);
    }
}
```

### Why?

Measuring distance is actually pretty straightforward and is presented reasonably clearly in the documentation (just do a search for "distance"). There are several ways to measure distance: Vector3.Distance just means to measure distance in all dimensions. What this code is doing is saying, "If the Vector3.Distance between the position of placedEMP and keypadLock is less than or equal to 1, then do the following things. The next four lines should be familiar to you by now—they change the color of keypadLock, activate keypadSmoke, and then use iTween to rotate open both doors to 45 and -45 degrees, respectively, over 0.8 seconds."

Now this has some limitations. It assumes we are only using the EMP to break open the keypadLock (which we are). But if in an expanded version of the game the EMPs were going to be used for other objects, we'd need to include some other mechanism (perhaps additional Booleans) to do this. But for now, this is going to work out great.

- **Step 24:** Save and return to Unity. Fix syntax problems.

- **Step 25:** Populate the new public variables (Figure 15.30). These should be populated from objects in the Hierarchy (not the Project panel). If you're using the Unity packages, the names will largely match. But feel free to use your own.

![](img/0285f88bc840f313779e011725b623a5_459_0.png)

### Tips and Tricks

As a side note, the EntryWay_KeyPadSmoke (Figure 15.31) is actually just a slightly modified smoke particle emitter from Unity's built-in Particles (accessible in the Standard Assets/Particles folder if you've already imported the Particles Unity Package). Pick one and then put it into the scene next to the keypad. Make any changes you want to the smoke. Then use that smoke to populate the Keypad Smoke entry field.

- **Step 26:** Test and play.

![](img/0285f88bc840f313779e011725b623a5_460_0.png)

**FIGURE 15.31** EntryWay KeypadSmoke. Just a modified version of Unity's built-in smoke.

### Conclusion

If all is working right, after the EMP is placed next to the keypad, it should explode, turn itself black, turn the keypad black, start the smoke coming from the keypad, and open the doors. If you've been following all the tutorials, there should also be a trigger set within those open doors that will move us to Scene-Hallway.

There's some important things left to do. Right now, we have no inventory system, so it's clumsy (we have to manually activate or deactivate the tool before running the game). We need to build in a system so that the player can determine which tool or weapon to use. We also need to build in mechanisms that kill the player if he falls in the water, and that make the player lose if the alarms in the building go off for too long. Lastly, we need to build in some way for the player to win.

In the next chapter we'll build in this endgame sort of mechanics. At that point we'll have a functioning game that's ready to be built and distributed.

![](img/0285f88bc840f313779e011725b623a5_462_0.png)

## Unity: Creating Inventory Systems

Thus far we have created several weapons and tools (our flashlight, EMP, and pistol). However right now, in order to use any of the three, they have to be activated in the script manually before running the game. This, of course, is a useless method to the player. What we need to do is create an inventory system that allows the player to choose which tool he wants to use and when. This inventory system will also do the work behind the scenes of turning various tool functionality on and off in the scripts.

Right now, the gun is active even when placing an EMP. The flashlight is shining even when the flashlight isn't visible. We need to get these tools so we use them one at a time. Before we get to the nitty-gritty, though, there are a few core ideas to cover.

### State Engine and How Many Scripts?

A state engine is a mechanism that (for our purposes) will keep track of what state the game is in. Or more directly, what state the player is in. Or more specifically, what weapon/tool the character is using. It turns out we've actually been creating one as we've been building the AC_ToolFunctionalityScript. So far this script's main chunk of code is a big Update function that checks if a list of Booleans are true or false. Depending on which Boolean is true, the script fires a block of code, or calls on another function within the script. Currently, the only way to define which Boolean is true is via the public variables accessible in the Inspector.

But this state engine can be much more robust. We can build in functionality that allows other scripts to call back to AC_ToolFunctionalityScript and tell it that a certain state (Boolean) is now active, or deactivate a Boolean. With this new information, AC_ToolFunctionality can fire new blocks of script at the appropriate times.

Currently almost all these blocks of script are housed within AC_ToolFunctionalityScript. And this script is getting a bit unwieldy to show in this book since it's getting long. In fact, large chunks of this script could indeed be broken out into other distinct and discrete scripts and this AC_ToolFunctionalityScript could simply call out to these particular scripts when needed. There are some real benefits to working this way: the gun functionality can be included in a GunFunctionality script. Someone coming into the project can look at a script folder and see quickly what things are happening and what's doing it without having to read through too much script. The drawback to a whole lot of scripts is the temptation to start letting multiple scripts control the same thing, like locking and hiding the mouse.

I've been involved and have authored projects (to my shame) that have multiple scripts hanging around the project that have access to things like hiding the cursor. The problem is that as the game development progresses and there's a bug that the mouse isn't becoming visible when needed, it is a nightmare tracking down which script is turning it off, and which script should be turning it on when multiple scripts have that capability.

Using a centralized script to house things like the mouse turning off and on, and what the state of the game is in means there is only one place to go when searching out and squashing bugs. This centralized script houses the state engine and coordinates what's happening with other scripts. Other scripts can call out to it, but it keeps track of the central state of the game. One script to rule them all.

My colleague here at Los Alamos National Laboratory who is the central programmer for our team has had to develop sophisticated state engines. The training modules he authors are a thing of beauty since the prefabs are hardly ever broken, and all of his scripts sit in an empty GameObject in the game called ScriptContainer. All the functionality is contained in that one little package. Of further interest is how few scripts actually sit in there—oftentimes a complex game will have only three or four scripts (he also is constructing custom classes similar to iTween that reside in the Project panel that he can call on within the few scripts he hangs in the Hierarchy panel).
