

```
{
    return false;
}

// Get the value type, and check it's an integer
auto& property = itr->value;
if (!property.IsInt())
{
    return false;
}

// We have the property
outInt = property.GetInt();
return true;
}
```

You can then use the `GetInt` function in `LoadLevel` to validate that the loaded file's version matches the expected version:

Click here to view code image

```
int version = 0;
```

```
if (!JsonHelper::GetInt(doc, "version", version) ||
    version != LevelVersion)
{
    SDL_Log("Incorrect level file version for %s", file);
    return false;
}
```

Here, the JSON object in question is the overall document (the root JSON object). You first make sure that GetInt returns a value and, if it does, you check that its value matches the expected value (a const called LevelVersion).

You also add similar functions to JsonHelper to extract other basic types: GetFloat, GetBool, and GetString. However, where this paradigm really becomes powerful is for non-basic types. Specifically, many properties in this game are of type Vector3 (such as ambientLight), so having a GetVector3 function is very useful. The overall construction of the function is still the same, except you need to validate that the property is an array with three members that are floats. You can similarly declare a GetQuaternion function.

## Ambient and Directional Lights

With the helper functions in place, you can create a function to load in the global properties. Because the global properties are varied and may not necessarily need the same class types, you must manually query the specific properties you need. The LoadGlobalProperties function in Listing 14.4 demonstrates how to load the ambient light and directional light properties. Notice that for the most part, you call the helper functions you've created for these properties.

Note that you can access a property as a rapidjson::Value& directly through operator[]. The dirObj["directionalLight"] call gets the value with the directionalLight key name, and then the IsObject() call validates that the type of the value is a JSON object.

Another interesting pattern for the directional light is to have direct access to variables you want to set. In this case, you do not need to add any conditional checks on the GetVector3 calls. This is because if the property requested does not exist, the Get functions guarantee not to change the variable. If you have direct access to a variable and don't care if the property is unset, then this reduces the amount of code.

## Listing 14.4

LevelLoader::LoadGlobalProperties Implementation

Click here to view code image

```
void LevelLoader::LoadGlobalProperties(Game* game,
const rapidjson::Value& inObject)
{
    // Get ambient light
    Vector3 ambient;
    if (JsonHelper::GetVector3(inObject, "ambientLight", ambient))
    {
        game->GetRenderer()->SetAmbientLight(ambient);
    }

    // Get directional light
    const rapidjson::Value& dirObj = inObject["directionalLight"];
    if (dirObj.IsObject())
    {
        DirectionalLight& light = game->GetRenderer()->GetDirectionalLight();
        // Set direction/color, if they exist
        JsonHelper::GetVector3(dirObj, "direction", light.direction);
        JsonHelper::GetVector3(dirObj, "color", light.color);
    }
}
```

You then add a call to `LoadGlobalProperties` in `LoadLevel`, immediately after the validation code for the level file version:

**Click here to view code image**

```
// Handle any global properties
const rapidjson::Value& globals = doc["globalProperties"];
if (globals.IsObject())
{
    LoadGlobalProperties(game, globals);
}
```

You can then add a call to `LoadLevel` in `Game::LoadData`, which loads in the `Level0.gplevel` file:

**Click here to view code image**

```
LevelLoader::LoadLevel(this, "Assets/Level0.gplevel")
```

Because you're now loading in the light properties from the level file, you can also remove the code in `LoadData` that hard-coded the ambient light and directional light.

## Loading Actors

Loading in the actors means the JSON file needs an array of actors, and each actor has property information for that actor. However, you need some way to specify which type of `Actor` you need (because there are subclasses). In addition, you want to avoid having a long set of conditional checks in the level loading code to determine which `Actor` subclass to allocate.

As before, it helps to first visualize what the data might look like. Listing 14.5 shows one method to specify the actors in the JSON file. This example only shows actors of type `TargetActor`, but the type can easily specify any other `Actor` subclass. Note that in addition to the type are any other properties to specify for that actor. Here, the only properties set are position and rotation, but these could conceivably be any property the actor has.

## Listing 14.5 Level with Actors (Level1.gplevel)

Click here to view code image

```
{
    // Version and global properties
    // ...
    "actors": [
    {
        "type": "TargetActor",
        "properties": {
          "position": [1450.0, 0.0, 100.0]
        }
    },
    {
        "type": "TargetActor",
        "properties": {
          "position": [0.0, -1450.0, 200.0],
          "rotation": [0.0, 0.0, 0.7071, 0.7071]
        }
    },
    {
        "type": "TargetActor",
        "properties": {
          "position": [0.0, 1450.0, 200.0],
          "rotation": [0.0, 0.0, -0.7071, 0.7071]
        }
    }
    ]
}
```

Assuming for a moment that you have a method to construct an actor of a specific type, you also need to be able to load properties for the actor. The simplest approach is to create a virtual LoadProperties function in the base Actor class, shown in Listing 14.6.

## Listing 14.6 Actor::LoadProperties Function

Click here to view code image

```
void Actor::LoadProperties(const rapidjson::Value& inObj)
{
    // Use strings for different states
    std::string state;
    if (JsonHelper::GetString(inObj, "state", state))
    {
        if (state == "active")
        {
            SetState(EAActive);
        }
        else if (state == "paused")
        {
            SetState(EPaused);
        }
        else if (state == "dead")
        {
            SetState(EDead);
        }
    }

    // Load position, rotation, and scale, and compute
    JsonHelper::GetVector3(inObj, "position", mPosition);
    JsonHelper::GetQuaternion(inObj, "rotation", mRotation);
    JsonHelper::GetFloat(inObj, "scale", mScale);
    ComputeWorldTransform();
}
```

Then, for some subclass of Actor, you can override the LoadProperties function to load any additional properties, as needed:

Click here to view code image

```
void SomeActor::LoadProperties(const rapidjson::Value& inObj)
{
    // Load base actor properties
    Actor::LoadProperties(inObj);

    // Load any of my custom properties

    // ...

}
```

Now that you have a way to load properties, the next step is to solve the issue of constructing an actor of the correct type. One approach is to create a map where the key is the string name of the actor type, and the value is a function that can dynamically allocate an actor of that type. The key is straightforward because it's just a string. For the value, you can make a static function that dynamically allocates an actor of a specific type. To avoid having to declare a separate function in each subclass of `Actor`, you can instead create a template function like this in the base `Actor` class:

Click here to view code image

```
template <typename T>

static Actor* Create(class Game* game, const rapidjson::Value& inObj)
{

    // Dynamically allocate actor of type T

    T* t = new T(game);

    // Call LoadProperties on new actor

    t->LoadProperties(inObj);

    return t;
}
```

Because it's templated on a type, it can dynamically allocate an object of the specified type and then call LoadProperties to set any parameters of the actor type, as needed.

Then, back in LevelLoader, you need to create the map. The key type is std::string, but for the value, you need a function that matches the signature of the Actor::Create function. For this, you can once again use the std::function helper class to define the signature.

First, you use an alias declaration (which is like a typedef) to create an ActorFunc type specifier:

Click here to view code image

```
using ActorFunc = std::function<
    class Actor*(class Game*, const rapidjson::Value&)
>;
```

The template parameters to std::function specify that the function returns an Actor* and takes in two parameters: Game* and rapidjson::Value&.

Next, you declare the map as a static variable in

