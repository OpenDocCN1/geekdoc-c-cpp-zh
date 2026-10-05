```
piece.transform.position = li.position;
piece.transform.rotation = Quaternion.Euler(
  li.rotation.x, li.rotation.y, li.rotation.z);
piece.transform.localScale = li.scale;
```

Here's what you cooked up in:

+   1. Reads the JSON file content of the selected level — selectedLevel is the path where the level resides after the player clicks the corresponding button. JsonUtility is a class that deserializes the JSON content to an instance of LevelDataRepresentation. It also sets all the nested fields, so this object contains all the level hierarchy deserialized in this one object.
2. Makes levelData. levelItems into a fully populated array of LevelItemRepresentation instances.
3. For every item that is looped through the array, the script locates correct prefab and loads it from the Resources/Prefabs folder by the prefName value.
4. Instantiates a clone of this prefab. When the prefab has a sprite, it's configured based on sprite data from the JSON file for that item.
5. Makes the object of the Level GameObjectthen sets its position, rotation and scale based on the data for that in the level file.

piece.transform.localScale = li.scale; at the bottom of the foreach loop. Add the following code which needs the closing curly for each of the following:

```
var SoyBoy = GameObject.Find("SoyBoy");
SoyBoy.transform.position = levelData.playerStartPosition;
Camera.main.transform.position = new Vector3(
SoyBoy.transform.position.x, SoyBoy.transform.position.y,
Camera.main.transform.position.z);
```

The scene always has a SoyBoy GameObject in the Hierarchy. However, when it loads, possible that Super SoyBoy is in a different starting location — that could be a real problem.

This code locates SoyBoy and places him at the playerStartPosition location saved in the JSON file. Next, it positions the camera in line with SoyBoy, so the level loads with the view squarely on that little chunk of tofu.

Now, you just need some code to set up the camera's Smooth Follow script settings in accordance with how the level was designed and saved.