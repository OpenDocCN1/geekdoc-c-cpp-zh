```
var ldr = new LevelDataRepresentation();
var levelItems = new List<LevelItemRepresentation>();
```

Here's the breakdown of that block of code:

+   1. Grabs a handle on the Level component and sets the Level GameObject position and rotation to 0, ensuring everything is positioned from the origin point in the scene.
2. Establishes LevelRoot as a reference to the Level GameObject, which is the parent of all level items.
3. Creates new instances of LevelDataRepresentation and LevelItemRepresentation.

Add the following just below List<LevelItemRepresentation>(); in the last bit of code:

```
foreach (Transform t in levelRoot.transform)
  // 4
  var sr = t.GetComponent<SpriteRenderer>();
  var li = new LevelItemRepresentation()
  {
    position = t.position
```

Here's what you're doing in there:

+   4. Loops through every child Transform object of levelRoot. Then it takes a reference to any potential SpriteRenderer component and assigns it to the sr variable. Then it creates a new LevelItemRepresentation to hold the position, rotation and scale of each item.