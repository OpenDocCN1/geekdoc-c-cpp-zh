BlasterGameManager derives from BaseGameController, which in turn derives from MonoBehaviour so that it can tap into some of Unity's built in calls to functions like Update(), Awake() and Start() etc:

```
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;
using GPC;

public class BlasterGameManager : BaseGameManager
{
    public Transform _playerPrefab;
    public Transform _playerSpawnpoint;
    public BaseCameraController _cameraManager;
    public Transform _thePlayer;
    public BlasterPlayer _thePlayerScript;
    public List<BlasterPlayer> _playerScripts;
    public BlasterUI_Manager ui_Manager;
    public ScreenAndAudioFader _fader;
    public int enemyCounter;
    public BaseUserManager _baseUserManager;
    public BaseSoundManager _soundComponent;
}
```

Above, we require System.Collections.Generic for using Lists. UnityEngine.SceneManagement for returning to the main menu at the end of the game and GPC for the framework.

The class declaration above shows we derive from BaseGameManager. Next, we skip past all but one of the variable declarations and get to the constructor:

```
set; }
public static BlasterGameManager instance { get; private

public Awake()
{
    instance = this;
}
```

As with any other Singleton style classes we produce in this book, above we declare a variable named instance that gets set to this instance in its Awake() function.

```
private void Start()
{
    // start with audio muted and fade covering the screen
    _fader.SetFadedOut();
    // schedule a fade in after a little time
    Invoke("StartFadeIn", 1f);
    SetTargetState(Game.State.Loaded);
}
```

When the Start() function runs, automatically called by Unity, the first thing we need to do is make sure that the screen starts blacked out so that we can have a nice fade in. To pull this off, we call out to the ScreenAndAudioFader class reference in _fader and run its SetFadedOut() function. This will set the state of the fader to black right away.

The next line is an Invoke statement that will call the StartFadeIn() function in one second. We delay this to make it work nicely – it appears better to a user if