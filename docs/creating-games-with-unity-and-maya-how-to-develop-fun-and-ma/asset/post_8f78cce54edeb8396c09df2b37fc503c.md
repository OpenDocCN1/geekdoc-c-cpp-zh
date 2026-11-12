
## Tutorial 16.2: Keys

Hopefully, this will be a fun tutorial. In the process of this tutorial, we'll make use of the techniques we've covered in the past tutorials. By assembling these skills in a new way, we'll have a new mechanism in the game.

The process will go like this: First we'll need to create a trigger that checks to see if the player has the key when the player enters it. If the player does indeed have the key, the door will open; if the player does not, a text prompt will pop up to alert the player that he needs the key. We'll create a PickUpKey function that fires when the player's ray is cast upon the key and the player clicks it. When the player clicks the key, we'll make the key disappear from the scene, but create a GUI element to indicate that the key is on the player's person. It's going to be fun!

- **Step 1:** Create a new GUITexture to show the key. Create a new GUITexture (`GameObject>Create Other>GUITexture`) and name it `KeyIcon`. Use the texture `Icon-Key` from the 2D Assets folder to define its texture.

- **Step 2:** Place the key in the top-right corner of the screen. Select `KeyIcon` in the Hierarchy and in the Inspector change the Transform X and Y values to 1. Change the Pixel inset values to X = -70, Y = -70, Width = 64, Height = 64 (Figure 16.6).

![](img/0285f88bc840f313779e011725b623a5_485_0.png)

### Why?

The image is 64x64. With the GUITexture at 1,1,0, the bottom-left corner of the image is at the top-left corner of the screen, meaning that the image is off the screen. By offsetting the pixels by -70 in both X and Y, we slide the image back onto the screen with a 6-pixel buffer above and to the right.

- **Step 3:** Now that you can see what it will look like when visible, move it off the screen. Select `KeyIcon` in the Hierarchy and in the Inspector, change the Transform X = 1, Y = 1.

> **Why?**
>
> We're just sliding it off the screen, so that when the key is actually acquired, it can slide back on.

- **Step 4:** Make KeyIcon a child of GUIElements. Go ahead and break the prefab. Then once the KeyIcon is a child of GUIElements, be sure to press the Prefab Apply button.

### Accessing the State Engine

- **Step 5:** Open AC_ToolFunctionalityScript.

**Why?**

Our state engine exists in the AC_ToolFunctionalityScript. Remember this is where we're keeping track of flashlightActive, pistolActive, empActive, and empGhostActive. We need to add a new state (a new Boolean): keyAcquired.

- **Step 6:** Make the state engine aware of a new potential state: keyAcquired. Add the following lineup among the variable declarations:

```javascript
private var flashlightActive : boolean;
private var pistolActive : boolean;
private var empActive : boolean;
private var empGhostActive : boolean;
private var keyAcquired : boolean;
```

**Why?**

We could technically store this Boolean in other places, but keeping all the Booleans in one place really helps when it comes time for bug squashing. If all the states are being stored in one place, we know exactly what place to look if the state isn't working as desired.

### Building upon the Raycasting Mechanism

Remember that earlier we set up this AC_ToolFunctionalityScript with a raycasting mechanism. Look up in the function Update section and see that the following block of code exists:

```javascript
if (hitObj.name == "Hallway_Key"){
    AddHighlight(hitObj);
}
```

This exists within the raycasting mechanism and says, "if the object we raycast against is named 'Hallway_Key,' fire the AddHighlight function." This really is just a placeholder for what's really going to happen here.

In reality, if the object that is being raycast against is named Hallway_Key, we need to highlight it, and then if the user clicks the mouse we need to fire a new function called PickUpKey.

- **Step 7:** Rework this section to read as follows:

```javascript
if (hitObj.name == "Hallway_Key") {
    AddHighlight(hitObj);
    if (Input.GetMouseButtonDown(0)) {
        PickUpKey();
    }
}
```

> **Why?**
>
> So what we're saying here is “if the object raycast against is named Hallway_Key, then highlight it, and then (if the object being raycast against is still Hallway_Key) if the user clicks the mouse button, fire the function PickUpKey.”

### Fleshing Out PickUpKey

Now we can do all the action involved in actually picking up the key.

- **Step 8:** Scroll and create a new function called PickUpKey. Flesh the function out like this:

```javascript
function PickUpKey(){
    var keyIcon : GameObject = GameObject.Find("KeyIcon");
    iTween.MoveTo (keyIcon, Vector3 (1.1,0), 1);
    var keyGeometry : GameObject = GameObject.Find("Hallway_Key");
    keyGeometry.active = false;
    keyAcquired = true;
}
```

> **Why?**
>
> This does some interesting things. First, notice that there are two local variables declared (keyIcon and keyGeometry). We will use these only once (the character picks up the key only once), so rather than cluttering up an already crowded block of variable declarations, we'll declare these new variables as we need them.
>
> Immediately after declaring each, and even in the same line, we tell Unity to go out and populate them by finding objects by a particular name. Generally, using GameObject.Find in a function can be dangerous,

![](img/0285f88bc840f313779e011725b623a5_489_0.png)

FIGURE 16.7 The door that will be locked.

- Step 14: Rotate the group so that the door is shut. The Rotation XYZ should all be 0.

- Step 15: Make sure the group (and its children) is set to non-Static. Do this in the Inspector by checking off the Static option.

**Why?**

The group was probably originally set to Static since it needs to be to be included in the bake. However, if it remains marked as Static we can't animate it with iTween (or any other script-driven method for that matter).

- Step 16: Create a trigger called Trigger-LockedDoor. As a refresher, remember this can be done by creating a Cube (GameObject>Create Other Cube). Click off its Mesh Renderer in the Inspector. Turn on its Is Trigger option within the Box Collider and resize and place it as seen in Figure 16.8.

![](img/0285f88bc840f313779e011725b623a5_489_1.png)

FIGURE 16.8 Trigger-LockedDoor.

- Step 17: Create an AudioSource that contains the sound of a squeaky door opening. Make sure Play on Awake is turned off. Place the AudioSource right by the door and name it Sound-DoorLocked.

- **Step 18:** Create a new JavaScript. Name it HallwayDoorsLockedTriggerScript. Open the script in your script editor.

### Why?

I can hear you hard-core scripters screaming from here, "Just use the HallwayDoorsTriggerScript and alter it to be able to check for a Boolean state." And you'd be absolutely right. A much more efficient method would be to create one door-opening script that is useful in almost all situations; however, we're going to build another to review how triggers function, and to keep the script easy to read within the book.

- **Step 19:** Define variables for the door, the bulkheadHandle, a doorOpenSound, the mainCamera, and the guiTextHints:

```javascript
var door : GameObject;
var bulkheadHandle : GameObject;
var doorOpenSound : GameObject;
private var mainCamera : GameObject;
private var guiTextHints : GameObject;
```

### Why?

The door is the object that opens. The bulkheadHandle is the wheel that turns. The doorOpenSound is a sound that plays when this big ol' door opens. The next two private variables allow us to track down where our state engine lives (attached to Main Camera), and drive a screen hint if the player has not gotten the key yet.

- **Step 20:** On Start, have the script populate mainCamera and guiTextHints:

```javascript
function Start() {
    mainCamera = GameObject.Find("Main Camera");
    guiTextHints = GameObject.Find("GUITextHints");
}
```

### Why?

So why make mainCamera and guiTextHints private variables and populate them in script and not do this for the others? Good question; the answer is that this will make the script applicable in other locked-door situations. In most all situations where the door is locked (and we want to be able to open it), the state engine will be accessed, and the screen hints will be shown. Since these two objects won't change, hard coding them saves populating in Unity. But since the door may indeed change if this script is used elsewhere, keeping it a public variable (along with the door handle and sound the door plays) will allow this script more uses.
