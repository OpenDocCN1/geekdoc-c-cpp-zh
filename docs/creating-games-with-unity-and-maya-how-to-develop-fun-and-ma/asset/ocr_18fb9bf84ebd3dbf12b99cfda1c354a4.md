For instance, right now, the pistol is always out since the AegisChung_Arms prefab has the PistolReady animation running first thing. This was great when we were setting up the firing of the gun, but is a little awkward now since it's pretty unbelievable that the gun will make the EMP work or shine light like a flashlight.

So we need to create a couple of functions to bring the pistol out and put it away. We'll create these functions within the InventoryButtonScript (with the idea that this script handles all the defining when tools are used with their respective buttons), and call them up when the buttons are pressed to activate or deactivate a weapon/tool.

The way we'll put the pistol away (and the flashlight for that matter) is by playing the animation PistolReady (and FlashlightReady) forward (to bring it out) and backward (to put it away). The way animations are called on is like this: GameObject.animation.Play("Name of Animation");

Let's call up some animations.

**Step 21:** Still within InventoryButtonScript, at the top of the script, declare a new variable to hold the object that has the animations attached to it (Aegis's arms).

```
private var aegisArms : GameObject;
```

**Step 22:** Create a new function to ready the pistol. And when the pistol is ready set the pistolReady Boolean to active. Do this at the bottom of the script:

```
function ReadyPistol()
    aegisArms.animation["PistolReady"].speed = 1;
    aegisArms.animation.Play("PistolReady");
    yield WaitForSeconds (aegisArms.animation.clip.length);
    ToolFunctionality.pistolActive = true;
}
```

> **Warnings and Pitfalls**
> 
> Note that there is a subtle but important difference when working with attributes of an animation (like changing the speed)—namely that the name of the animation is contained in [ ] and not ( ) like it is when the clip is being played.

# Why?

The first line there simply says, "on the GameObject aegisArms, find the animation called "PistolReady" and set its speed to 1 (play at regular speed). There usually is little need to change the speed of an animation (if it's animated correctly); however, in a bit, we're going to play this animation backward by setting the speed to -1. If we don't make sure it's set to positive 1 here, we won't know if the animation is playing forward when it's called up in the next line.

Next we're telling Unity to wait for the animation to play—or more specifically wait for the amount of seconds it takes for the animation to play before going to the script contained in the ToolFunctionality variable (which we declared on Awake as the AC_ToolFunctionalityScript that is attached to Main Camera) and setting pistolActive to true.