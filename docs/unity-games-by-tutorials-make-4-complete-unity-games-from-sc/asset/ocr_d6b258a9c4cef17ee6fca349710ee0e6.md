5. This is a bit of a hack to store the name of each level item in the prefabName field. When loading a level later on, your code will need to know which prefabs to use to construct the level based on the name stored in the JSON file.

When you design a level, you tend to duplicate or clone items, which adds spaces and numbers in brackets to each cloned item. This hack does its to trim away spaces and brackets with numbers from the items nested under the Level root. The resulting name will become the name of the prefabs to load later from the Resources/Prefabs folders.

6. Performs a check to ensure that a valid SpriteRenderer was found — because a level item might not have an attached sprite. If the sr variable is not null, then information about the sprite's sorting, order and color stores in the LevelItemItemRepresentation object.

7. Lastly, the item that has all the collected information is added to the levelItems list.

Just below the closing curly bracket of the for loop you added, add this code:

```
//
ldr.levelItems = levelItems.ToArray();
ldr.playerStartPosition = =
GameObject.Find("SoyBoy").transform.position;
// 9
var currentCameraSettings = FindOfType<CameraLerpToTransform>();
if (currentCameraSettings != null) {
  ldr.cameraSettings = new CameraSettingsRepresentation() {
    cameraTarget = currentCameraSettings.cameraTarget.name,
    cameraDepth = currentCameraSettings.cameraDepth,
    minX = currentCameraSettings.minX,
    minY = currentCameraSettings.minY,
    maxX = currentCameraSettings.maxX,
    maxY = currentCameraSettings.maxY,
    trackingSpeed = currentCameraSettings.trackingSpeed
  };
}
```

8. Converts the entire list of level items to an array of LevelItemRepresentation objects and stores them in the levelItems field on the LevelDataRepresentation object.

9. Locates the CameraLerpTransform script in the scene. Then it maps its settings against a new CameraSettingsRepresentation object and assigns that object to the LevelDataRepresentation object's cameraSettings fields.