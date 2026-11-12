**Step 21:** Save and return to Unity. Fix any syntax errors that pop up in the console.

**Step 22:** Attach this script to Trigger-FindDoorHint (the big cube acting as a trigger).

**Step 23:** Play the game. The cube is probably big and dark in your scene, but will be easy to see. As you walk through it, the text "find the secure entrance to the base" will appear at the bottom of the screen and disappear after 3 seconds. If this doesn't happen, double-check all the names called for in the scripts.

# Tips and Tricks

The approach we've used here of nesting all the variables in private variables and using the GameObject.Find and GetComponent methodologies keeps the Unity editor clean. We don't need to connect a bunch of objects manually to any scripts; we are taking care of it in script. The benefit of this is if for some reason an object is deleted and we recreate it, we don't have to remember the places where it had to be plugged in. The drawback is that the connections of objects to scripts can only be seen in the scripts and not directly in the Editor. There are trade offs either way.

**Step 24:** Create additional cubes (converted to triggers) for the Trigger-WaterHint (around the water areas) and Trigger-EMPHint (as the player approaches the door) triggers. Be sure that these triggers also include the EntryWayTextTriggerScript. Remember this can also be done by copying/pasting the Trigger-FindDoorHint GameObject and moving/scaling/rotating/renaming the copy. Notice that in Figure 13.6 there are two large triggers covering the canal part. As long as both of these triggers have the same name, our mechanism will work.

![](bbox=[0.14, 0.64, 0.65, 0.88])

**Step 25:** Test the triggers. Play the game and see if indeed the text appears and changes at the appropriate places.