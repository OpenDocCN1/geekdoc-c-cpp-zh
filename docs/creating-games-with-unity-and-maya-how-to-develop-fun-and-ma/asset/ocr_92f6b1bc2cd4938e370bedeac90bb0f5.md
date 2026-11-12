In reality, if the object that is being raycast against is named Hallway_Key, we need to highlight it, and then if the user clicks the mouse we need to fire a new function called PickUpKey.

**Step 7:** Rework this section to read as follows:

```
```
if (hitObj.name == "Hallway_Key") {
    AddHighlight(hitObj);
    if (Input.GetMouseButtonDown(0)) {
        PickUpKey();
    }
}
```
```

> > **Why?**
> >
> > So what we're saying here is “if the object raycast against is named Hallway_Key, then highlight it, and then (if the object being raycast against is still Hallway_Key) if the user clicks the mouse button, fire the function PickUpKey.”

# Fleshing Out PickUpKey

Now we can do all the action involved in actually picking up the key.

**Step 8:** Scroll and create a new function called PickUpKey. Flesh the function out like this:

```
```
function PickUpKey(){
    var keyIcon : GameObject=GameObject.Find("KeyIcon");
    iTween.MoveTo (keyIcon, Vector3 (1.1,0), 1);
    var keyGeometry : GameObject = GameObject.Find
    ("Hallway_Key");
    keyGeometry.active = false;
    keyAcquired = true;
}
```
```

> > **Why?**
> >
> > This does some interesting things. First, notice that there are two local variables declared (keyIcon and keyGeometry). We will use these only once (the character picks up the key only once), so rather than cluttering up an already crowded block of variable declarations, we'll declare these new variables as we need them.
> >
> > Immediately after declaring each, and even in the same line, we tell Unity to go out and populate them by finding objects by a particular name. Generally, using GameObject.Find in a function can be dangerous,