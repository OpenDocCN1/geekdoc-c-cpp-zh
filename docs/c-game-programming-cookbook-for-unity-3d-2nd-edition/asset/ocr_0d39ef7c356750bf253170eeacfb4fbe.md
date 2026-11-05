Profiles, too. This is to make accessing the data easier, as the path to the data can sometimes be a little long to be repeatedly typing out in other functions. We save a bunch of repetition by providing the functions to return data right from inside the BaseProfileManager class. As you grow and expand your own save Profiles, you should bear that in mind and consider adding functions to this class to make it easy to get or set save profile data from your other scripts.

```
```csharp
using UnityEngine;
using System;
namespace GPC
{
    public class BaseProfileManager : MonoBehaviour
    {
        [System.NonSerialized]
        public bool didInit;
        public ProfileScriptableObject profileObject;
        public static ProfileData loadedProfile;
        public string profileSaveName = "Game_ProfileData";

        private int numberOfProfileSlots = 3; // you can
        change this to whatever you want, but for this example we'll only
        need 3 slots
    }
```
```

BaseProfileManager derives from MonoBehaviour, so that we can easily change and set values in the Inspector as needed.

We use the regular didInit, just as a safeguard we can look to whenever we need to make sure that the script has run its Init() function.

Next above, we declare the variable profileObject – this is typed as a ProfileScriptableObject (yes, the same one we made in Section 12.1 earlier!) and it will hold a reference to the ScriptableObject we use for storing user Profiles in. Below that, you can see the variable loadedProfile, a ProfileData typed variable that will be used to store the currently loaded profile data whenever we need it. Note that the actual profile data is still stored in the ScriptableObject but we use this to hold the individual profile we are accessing (during the game or whenever we need to get data from a profile).

Whenever we save and load data, it needs a filename. We hold a filename in profileSaveName and it is publicly declared so it can be edited in the Inspector. Just be sure that the filename is the name if you use BaseProfileManager in multiple Scenes.

The last variable above is numberOfProfileSlots. In effect, this just defines the length of the array used to store data in the ScriptableObject (then, in turn, the save files). You can have as many Profiles as you like, but it will be up to you to provide an easy way to display them to the user.

Note that this book does not include an interface for selecting a save profile. We just save to the first profile – if you need to add additional save profile functionality, that is left up to you.

The Init() function is up next:

```
```csharp
public void Init()
{
    // grab the ScriptableObject from Resources/
    ScriptableObjects folder
    if(profileObject==null)
        profileObject = Resources.Load
        ("ScriptableObjects/ProfileData") as ProfileScriptableObject;
}
```
```

The variable profileObject should contain a reference to the ScriptableObject used for profile data storage. When profileObject is null, we know that it has