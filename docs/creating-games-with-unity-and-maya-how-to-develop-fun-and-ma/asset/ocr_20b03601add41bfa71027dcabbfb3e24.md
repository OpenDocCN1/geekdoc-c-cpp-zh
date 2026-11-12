```
```javascript
        yield WaitForSeconds (5);
        guiText.enabled = false;
    }
```
```

> > **Why?**
> >
> > These are literally copied and pasted with the specifics of what the text says and how long to display it altered. Again, what we have here are a lot of instructions waiting for the nod to fire. Note that we also haven't created the triggers for the StayOutOfWaterHint and TryEMPHint. That will come.

+   - **Step 15:** Save, return to Unity, and check for syntax errors in the Console. Fix if needed.
+   - **Step 16:** Attach this script to the GUITextHints GameObject. Remember this is done by just dragging the script from the Project panel to the GameObject in the Hierarchy.

# ## Scripting Triggers

It's all fairly anticlimactic at this point. This script is attached to the object it needs to be and is all set to start displaying and changing text, but nobody's told it to do so yet. With this next script we will add real functionality to the trigger created earlier and instruct it to start firing functions created in the first script.

+   - **Step 17:** In your Project panel, select the Scripts folder. Create a new JavaScript and name it EntryWayTextTriggerScript. Open it by double-clicking it.
+   - **Step 18:** Delete the default code and enter the following:

```
```javascript
private var guiTextObject : GameObject;
```
```

> > **Why?**
> >
> > This script we are writing here will be attached to the triggers. But this script needs to talk to another script attached to another GameObject. The other GameObject is GUITextHints, which we're going to call guiTextObject here.

+   - **Step 19:** Add the following to define the new variable:

```
```javascript
private var guiTextObject : GameObject;

function Awake () {
    guiTextObject = GameObject.Find("GUITextHints");
}
```
```

> > **Why?**
> >
> > Similar to the last chapter, this function Awake runs at the start of the game and goes out and finds the object GUITextHints and defines that as guiTextObject within this code.