BaseSoundController derives from MonoBehavior so that it can use the Awake() andnStart() functions called by the Unity engine:

```
public class BaseSoundController : MonoBehaviour
{
    public static BaseSoundController Instance;

    public AudioClip[] GameSounds;

    private int totalSounds;
    private ArrayList soundObjectList;
    private SoundObject tempSoundObj;

    public float volume = 1;
    public string gamePrefsName = "DefaultGame"; // DO NOT FORGET TO SET
                                                                // THIS IN THE EDITOR!!
```

The variable name Instance is static, accessible from anywhere, which makes
playing sound possible from any other script in the game. When the script's Awake()
function is called, Instance is set to the instance of the script. The assumption is that each
scene requiring sound effects will contain one instance of this script in a scene, attached
to an empty GameObject or similar. Since this script does not check for multiple instances,
care must be taken to ensure there is only one instance in a scene:

```
public void Awake()
{
    Instance = this;
}
void Start()
{}
```

PlayerPrefs saves a file to the user's hard drive, which can be accessed at any time for
saving trivial data. The Unity documentation has the following information on where
PlayerPrefs files are stored:

Editor/Standalone

On Mac OS X PlayerPrefs are stored in ~Library/Preferences folder, in a file named unity.
[company name][product name].plist, where company and product names are the names
up in Project Settings. The same .plist file is used for both Projects in the Editor
and standalone players.

On Windows, PlayerPrefs are stored in the registry under HKCU\Software\{company
name}[product name] key, where company and product names are the names set up in
Project Settings.

On Linux, PlayerPrefs can be found in ~/.config3d/[CompanyName]/[ProductName],
config33d again when using the company and product names specified in the Project Settings.

# WebPlayer

On Web players, PlayerPrefs are stored in binary files in the following locations:
Mac OS X: ~Library/PreferencesUnityWebPrefs
Windows: %APPDATA%\Unity\WebPlayerPrefs