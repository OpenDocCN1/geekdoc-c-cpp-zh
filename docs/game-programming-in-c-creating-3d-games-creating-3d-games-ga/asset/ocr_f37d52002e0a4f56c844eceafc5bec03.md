# sComponentFactoryMap:

# Click here to view code image

```
std::unordered_map<std::string, std::pair<int, Compon
LevelLoader::sComponentFactoryMap
{
    { "AudioComponent",
        { Component::TAudioComponent, &Component::Create
    },
    { "BallMove",
        { Component::TBallMove, &Component::Create<BallW
    },
    // Other components omitted
    // ...
};
```

You then implement a LoadComponents helper
function in LevelLoader, as shown in Listing 14.10. As
with LoadActors, it takes in an array of the
components to load and loops through this array. You
then use the sComponentFactoryMap to find the
component type. If it is found, you then check if the actor
already has a component of the type. The iter->
second.first accesses the first element of the value