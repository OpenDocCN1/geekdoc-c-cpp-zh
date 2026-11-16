template, as it’s the state of `TargetActor` when it’s originally spawned. Then, for each `TargetActor` to save in the level, compare its JSON object to the template one and write only the properties and components that are different.

You can then use this process for all the different types of actors. To assist with this, RapidJSON provides overloaded comparison operators. Two `rapidjson::Value`s are equal only if they have the same type and contents. This way, you can eliminate setting at least most of the components (because they won’t change). It will require a bit more work to do this on a granular (per-property) level.

# Exercise 14.2

Applying the same binary file techniques you used for the mesh files, create a binary file format for the animation files. Because all the tracks of bone transforms are the same size, you can use a format where, after writing the header, you write the ID for each track followed by the entire track information. For a refresher on the animation file format, refer to Chapter 12, “Skeletal Animation.”