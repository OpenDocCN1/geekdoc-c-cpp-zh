```
rapidjson::Value& inObject, const char* name, int
{
    rapidjson::Value v(value);
    inObject.AddMember(rapidjson::StringRef(name), v,
}
```

The last three parameters are identical to the parameters of the GetInt function, except the Value is now not const. The first parameter is an allocator that RapidJSON uses when needing to allocate memory. Every call to AddMember requires an allocator, so you must pass one in. You can get the default allocator just from a Document object, but you could conceivably use a different allocator if desired. You then create a Value object to encapsulate the integer and use the AddMember function to add a value with the specified name to inObject.

The rest of the Add functions are similar, except for AddVector3 and AddQuaternion, for which you must first create an array and then add float values to that array. (You'll see this array syntax when looking at the global properties.)

You then create a skeleton for the LevelLoader::SaveLevel function, as shown in Listing 14.11. First, you create the RapidJSON document and make an object for its root via SetObject. Next,