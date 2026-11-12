**Step 1:** Open the script AC_ToolFunctionalityScript.

**Step 2:** Make the script know whether or not the pistol is out and ready to be fired. Declare the following variable at the beginning of the script (since the script is getting long, the needed added snippet will be called out by itself):

```
```
...
var pistolActive : boolean = true;
...
```
```

# Why?

We're actually doing several things here. We're declaring the variable `pistolActive` and telling Unity it's going to be a type Boolean (on/off switch), and in the same line we're telling Unity its value is true (on). Later, we're going to adjust this so we can determine if the pistol is active via our inventory system, but for now, we just want to turn it on and leave it on.

**Step 3:** Have the script check to see if the pistolActive is true, and if it is, instantiate something that we'll call gunSpark (which will be a particle system). Add the following code:

```
```
...
    if (hit.collider.gameObject.name == "Hallway_Key")
        AddHighlight(hit.collider.gameObject);
    }
    if (pistolActive){
        if (Input.GetMouseButtonDown(0))
            var hitDirection = Quaternion
.LookRotation (hit.normal);
            Instantiate(gunSpark, hit.point,
hitDirection);
        }
    }
...
```
```

# Why?

So this new snippet checks to see if pistolActive is true; if it is, it listens for the player to press the left mouse button (if `Input.GetMouseButton(0)`); when the player does this Unity creates a temporary variable (called hitDirection) and has it look at the normal of where the ray is striking the surface. Remember that the normal of a surface is the front of the surface, or the direction the surface is facing. This is laying the groundwork so that when the gunSpark fires, it will fire out from the direction of the surface it hits.

The last line there is the important one for our purposes. It's instantiating or creating while the game runs an object called gunSpark, at the location of hit.point facing the hitDirection that we defined in the line before. So the syntax of Instantiate is Instantiate (an object, at this spot, rotated like this).