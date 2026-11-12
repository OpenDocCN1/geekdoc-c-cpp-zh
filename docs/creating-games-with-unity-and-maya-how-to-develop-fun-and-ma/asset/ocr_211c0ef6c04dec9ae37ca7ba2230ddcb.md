**Why?**

We're just sliding it off the screen, so that when the key is actually acquired, it can slide back on.

**Step 4:** Make KeyIcon a child of GUIElements. Go ahead and break the prefab. Then once the KeyIcon is a child of GUIElements, be sure to press the Prefab Apply button.

# Accessing the State Engine

**Step 5:** Open AC_ToolFunctionalityScript.

**Why?**

Our state engine exists in the AC_ToolFunctionalityScript. Remember this is where we're keeping track of flashlightActive, pistolActive, empActive, and empGhostActive. We need to add a new state (a new Boolean): keyAcquired.

**Step 6:** Make the state engine is aware of a new potential state: keyAcquired. Add the following lineup among the variable declarations:

```
private var flashlightActive : boolean;
private var pistolActive : boolean;
private var empActive : boolean;
private var empGhostActive : boolean;
private var keyAcquired : boolean;
```

**Why?**

We could technically store this Boolean in other places, but keeping all the Booleans in one place really helps when it comes time for bug squashing. If all the states are being stored in one place, we know exactly what place to look if the state isn't working as desired.

# Building upon the Raycasting Mechanism

Remember that earlier we set up this AC_ToolFunctionalityScript with a raycasting mechanism. Look up in the function Update section and see that the following block of code exists:

```
if (hitObj.name == "Hallway_Key"){
    AddHighlight(hitObj);
}
```

This exists within the raycasting mechanism and says, "if the object we raycast against is named 'Hallway_Key,' fire the AddHighlight function." This really is just a placeholder for what's really going to happen here.