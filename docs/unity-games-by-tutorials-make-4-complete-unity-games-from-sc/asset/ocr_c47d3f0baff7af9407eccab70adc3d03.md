It's also static, which means that — as you may remember — it can be called from any class without having to have a reference to beforehand.

+   2. This check makes sure that the method stops executing the origin point and destination are the same, which would create a zero-length vector. The LookRotation() method doesn't float like that so it's in place.

+   3. This blocks the current rotation and creates the target rotation for the Transform by using the LookRotation() method.

+   4. This is the actual method that makes the rotation interpolate, Lerp(). It might sound like some sort of frozen beverage. But in reality it's a handy way of getting a value between two other values (also called tweening) with a distinct beginning and end.

The SmoothlyLook() method can be used to replace the popping rotation of the enemies with a nice turn.

Save this script, open up the Enemy script and remove this line from the UpdateMovement() method:

```
transform.LookAt(targetPosition);
```

Put this in its place:

```
transform.localRotation = UtilityMethods.
SmoothlyLook(transform, targetPosition);
```

Now save the Enemy script and return to the editor. Make sure you have at least one enemy in the scene and press the Play button. You should now see the enemy turning smoothly at turns and edges. Finally, delete any enemies left in the Hierarchy.

That's it! Three handy utilities for Runstrife — and for your own games if you like.

# # Waves of enemies

In the current state of the game, there isn't anything happening without you dragging an Enemy prefab to the scene. You want waves of enemies to spawn onto the map in intervals.