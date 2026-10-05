# Building & nesting data classes for game components

Each level file uses a base LevelDataRepresentation object to store the following items in JSON:

+   - playerStartPosition: The position from where Super Soy Boy spawns.

+   - cameraSettings: An object that contains information about how to configure the smooth follow camera, including follow speed and boundaries.

+   - levelItems: An array of level item. For every object created under the root level GameObject in the level scene, an item in this array describes what the item is, its location, rotation, sprite color, etc.

By default, Unity's Json can't serialize camera settings or level objects because they're not simple types. Hence, they're represented as nested fields in the main LevelDataRepresentation.cs class.

In turn, these objects are represented by classes that have simple type fields. Unity's JSONUtility will be able to understand them!

For example, look at the LevelDataRepresentation.cs class. An instance of the LevelItemRepresentation.cs class represents each item stored in the levelItems array. The script has these simple type fields:

```
public Vector3 rotation;
public Vector3 scale;
public Vector2 position;
public string prefabName;
public int spriteOrder;
public string spriteLayer;
public Color spriteColor;
```

This nesting of [Serializable] classes is exactly how you make complex objects serialize or deserialize and nice with JSON.

# Parsing a level in the editor and saving it to disk

Open LevelEditor.cs. Add the following code below (GUILayout.Button("Save level")) above the using curly bracket:

```
// 1
Level level = (Level)target;
level.transform.position = Vector3.zero;
level.transform.rotation = Quaternion.identity;
// 2
var levelRoot = GameObject.Find("Level");
// 3
```