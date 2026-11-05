# 12 Saving and Loading Profiles

Saving and loading user data can be handled in many ways. For example, you might just store everything in a static class and dump it out to a JSON file whenever you need to. Perhaps you want to use .xml format files, or even a database? In this chapter, we will look at a method for saving and loading user data that uses a ScriptableObject combined with JSON for its format. The ScriptableObject contains an array of instances of a data class named ProfileData. The ProfileData class holds everything we want to save and load to Profiles. By using an array of ProfileData in the ScriptableObject, we can easily load, and save to more than one save profile.

The system in this chapter works with save slots, although there is no example user interface to choose a different slot. The example games simply use the first profile, but if you decide to take this further and build out an interface for multiple slots, you can call ChooseProfile(<slot number>) to select whichever slot ties up with your user interface.

# 12.1 The Save Profile ScriptableObject

We use a ScriptableObject for two reasons. One is so that the data is easily accessible from anywhere in our games – a reference to the ScriptableObject gives you a reference to the data. You can modify data on the ScriptableObject instance and wherever it is accessed from, the data will be up-to-date with the latest modifications. The second reason for a ScriptableObject is that we can instantly see it update inside the Unity editor, making it easier to debug storage. The ScriptableObject is an excellent way to store data and access it from anywhere.

You can find this ProfileScriptableObject.cs file in the folder Assets/GPC_Framework/Scripts/COMMON/SCRIPTABLEOBJECTS.