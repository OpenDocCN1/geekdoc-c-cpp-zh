```
JsonHelper::AddString(alloc, inObj, "state", state
JsonHelper::AddVector3(alloc, inObj, "position", n
JsonHelper::AddQuaternion(alloc, inObj, "rotation'
JsonHelper::AddFloat(alloc, inObj, "scale", mScale
}
```

With all these pieces in place, you can then add SaveActors and SaveComponents functions to LevelLoader. Listing 14.13 shows the SaveActors function. First, you get the vector of actors from the game by const reference. Then, you loop through every actor and create a new JSON object for it. You then add the string for the type by using the TypeID and TypeNames functionality. Next, you create a JSON object for the properties and call the actor's SaveProperties function. You then create an array for the components before calling SaveComponents. Finally, you add the actor's JSON object into the JSON array of actors.

# Listing 14.13 LevelLoader::SaveActors Implementation

Click here to view code image

```
void LevelLoader::SaveActors(rapidjson::Document::Alloc
Game* game, rapidjson::Value& inArray)
```