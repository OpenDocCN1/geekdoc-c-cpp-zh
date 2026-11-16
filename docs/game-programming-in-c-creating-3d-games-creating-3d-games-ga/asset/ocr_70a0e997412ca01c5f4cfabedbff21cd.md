array of actors, and each actor has property information for that actor. However, you need some way to specify which type of `Actor` you need (because there are subclasses). In addition, you want to avoid having a long set of conditional checks in the level loading code to determine which `Actor` subclass to allocate.

As before, it helps to first visualize what the data might look like. Listing 14.5 shows one method to specify the actors in the JSON file. This example only shows actors of type `TargetActor`, but the type can easily specify any other `Actor` subclass. Note that in addition to the type are any other properties to specify for that actor. Here, the only properties set are position and rotation, but these could conceivably be any property the actor has.

# Listing 14.5 Level with Actors (Level1.gplevel)

Click here to view code image

```
{
    // Version and global properties
    // ...
    "actors": [
    {
        "type": "TargetActor",
```