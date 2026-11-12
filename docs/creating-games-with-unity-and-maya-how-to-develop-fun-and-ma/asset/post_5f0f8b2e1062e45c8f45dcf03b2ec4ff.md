
We already know how to turn objects on and off (GameObject.active = true/false); we just need to declare the variables and then have them turned on and off in the right places.

### Step 32: Declare three new private variables at the top of the script:

```csharp
private var aegisFlashlight : GameObject;
private var aegisFlashlightLight : GameObject;
private var aegisPistol : GameObject;
```

**Why?**

We're declaring a variable to house the geometry of the flashlight (aegisFlashlight), the light (created way back when working in the hallway), and the pistol geometry (aegisPistol). We'll populate these here in our Awake function in a bit.

### Step 33: Populate these new private variables in the Awake function. So it should read like this:

```csharp
function Awake(){
    mainCamera = GameObject.Find("Main Camera");
    toolFunctionality = mainCamera.GetComponent("AC_ToolFunctionalityScript");
    aegisArms = GameObject.Find("AegisChung_Arms_Prefab");
    aegisFlashlight = GameObject.Find("AC_Flashlight");
    aegisFlashlightLight = GameObject.Find("Flashlight");
    aegisPistol = GameObject.Find("AC_Pistol");
}
```

**Why?**

Again, the assumption at this point is that we won't be renaming things, and that we go out and find only one of the objects. Again, the benefit of this is that we needn't populate them within Unity's editor—the drawback is that if we rename something, this script will break.

### Step 34: Activate these and deactivate them in the appropriate places within the ReadyPistol, StorePistol, ReadyFlashlight, and StoreFlashlight functions:

```csharp
function ReadyPistol(){
    aegisPistol.active = true;
    aegisArms.animation["PistolReady"].speed = 1;
    aegisArms.animation.Play("PistolReady");
    yield WaitForSeconds(aegisArms.animation.clip.length);
    toolFunctionality.pistolActive = true;
}

function StorePistol(){
    aegisArms.animation["PistolReady"].speed = -1;
    aegisArms.animation["PistolReady"].time = aegisArms.animation["PistolReady"].length;
    aegisArms.animation.Play("PistolReady");
    yield WaitForSeconds(aegisArms.animation.clip.length);
    aegisPistol.active = false;
    toolFunctionality.pistolActive = false;
}

function ReadyFlashlight(){
    aegisArms.animation["FlashlightReady"].speed = 1;
    aegisArms.animation.Play("FlashlightReady");
    aegisFlashlight.active = true;
    yield WaitForSeconds(aegisArms.animation.clip.length);
    aegisFlashlightLight.active = true;
    toolFunctionality.flashlightActive = true;
}

function StoreFlashLight(){
    aegisFlashlightLight.active = false;
    aegisArms.animation["FlashlightReady"].speed = -1;
    aegisArms.animation["FlashlightReady"].time = aegisArms.animation["FlashlightReady"].length;
    aegisArms.animation.Play("FlashlightReady");
    yield WaitForSeconds(aegisArms.animation.clip.length);
    aegisFlashlight.active = false;
    toolFunctionality.flashlightActive = false;
}
```

**Why?**

Most of that is pretty straightforward (i.e., turn on the aegisPistol right before running the animation that shows it and turn it off after the animation that stores it). The strange one is where the flashlight is. This is placed so that the light doesn’t turn on until after the FlashlightReady animation has been run, and turns off right before the flashlight is put away.

### Step 35: Make sure both pistol and flashlight are turned off when the game begins. Do this within a Start function (if you don’t have one). Usually this is done toward the top of the script after the variable declarations and any Awake functions but before any other functions:

```csharp
function Start(){
    aegisFlashlight.active = false;
    aegisFlashlightLight.active = false;
    aegisPistol.active = false;
}
```

**Why?**

This makes sure that the pistol and flashlight are turned on only when they are called (i.e., in the ReadyFlashlight or ReadyPistol functions). If we carefully turned them off in the editor before running the game, this wouldn’t be a problem, but including this little code snippet helps protect us against future carelessness.

### Step 36: Save and return to Unity. Fix any syntax problems.

### Step 37: Turn on Flashlight, AC_Flashlight, and AC_Pistol in the Hierarchy, select each of these objects and make sure they are active in the Inspector.

**Why?**

One of the potential drawbacks to populating variables in Awake (or Start) functions with a GameObject.Find command is that if an object is inactive, Unity can't find it. If the variable is a public variable that is populated by dragging the item from the Hierarchy, this isn't an issue. But with the method we're using here (private variables that are populated with Find), we need to make sure that when the game starts the objects are active to find. Remember that up in step 33, we immediately turn them all off again, but Unity now has an understanding of what they are and can reactivate them when told.

### Step 38: Select AegisChung_Arms_Prefab and in the Animation component, turn off Play Automatically.

**Why?**

Now we are carefully calling up when to play the animations of bringing up the pistol and flashlight. Without turning off Play Automatically, the pistol would always come up at the beginning of the game rather than when the player tells it to.

### Step 39: Open AC_ToolFunctionalityScript.

### Step 40: Turn off all the Booleans. Add the following lines to make sure that Unity knows on start up that there are no tools active.

```csharp
function Start()
{
    pistolActive = false;
    empathic = false;
    empGhostActive = false;
    flashlightActive = false;
}
```

### Step 41: Save and return to Unity. Fix any syntax errors or typos.

### Step 42: Play and test. There is still the pesky problem of the character looking up and to the left as the player attempts to select a piece of inventory (which we’ll fix in a minute); but at this point, the player should be able to activate any of the tools and they should work.

### Step 43: Apply these changes to the prefab. With FPC_AegisChung selected in the Hierarchy, in the Inspector click the Apply button on the Prefab line.

**Why?**

We want to make sure that all this work on the inventory system is functional in the Hallway too (and any other levels we create). By applying the changes to the prefab, we know that these new functionalities will work later as well.

## Bulking up the GUI System

We need to solve a couple of problems with our inventory system. First we don’t want it visible all the time; with it always there, it detracts from the immersive experience and the player assumes he can reach up and select a tool. The second problem is that we don’t want the mouse visible usually. It’d be necessary to have it visible when selecting tools, but it needs to go away when the game is running in noninventory mode. We’ll solve both of these problems by authoring a couple of new functions to show and hide the inventory.

But before we go too far, let’s clean up, expand, and make a prefab of all our GUIElements to clean up our Hierarchy, and make the elements more easily accessible and reusable.

### Step 44: Create a new GUITexture (GameObject > Create Other > GUI Texture). Name it InventoryPrompt. Use ButtonInventory-Tab-Horizontal (from the Project panel’s 2D Assets) for the Texture. Change the Transform X = 0 and Transform Y = 1. Change the Pixel Inset to X = 0, Y = -32, Width = 256, Height = 32.

**Why?**

This GUITexture will serve as the prompt to remind the player how to access the inventory.

### Step 45: Make InventoryButton_EMP, InventoryButton_Flashlight, and Inventory_Button_Pistol children of InventoryButton_Tab (in the Hierarchy, select these three GUITextures and drag them atop InventoryButton_Tab).

**Why?**

We are going to use iTween’s MoveTo to move all the buttons on and off the map. By making the button all of one element (the InventoryButton_Tab), we can animate just the tab, and all the buttons will go with it.
