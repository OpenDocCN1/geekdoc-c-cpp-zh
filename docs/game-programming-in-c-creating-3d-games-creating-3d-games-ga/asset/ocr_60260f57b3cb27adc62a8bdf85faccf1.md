later use.

With the map set up, you can now create a `LoadActors` function, as in Listing 14.7. Here, you loop over the `actors` array in the JSON file and get the type string for the actor. You use this type to then look up in `sActorFactoryMap`. If you find the type, you call the function stored in the map (`iter->second`), which in turn calls the correct version of `Actor::Create`. If you don't find the type, you have a helpful debug log message output.

# Listing 14.7 LevelLoader::LoadActors Implementation

Click here to view code image

```
void LevelLoader::LoadActors(Game* game, const rapidjson::Value& actorsArray)
{
    // Loop through array of actors
    for (rapidjson::SizeType i = 0; i < actorsArray.Size(); i++)
    {
        const rapidjson::Value& actorObj = actorsArray[i];

        if (actorObj.IsObject())
        {
            // Get the type
            std::string type;
        }
    }
}
```