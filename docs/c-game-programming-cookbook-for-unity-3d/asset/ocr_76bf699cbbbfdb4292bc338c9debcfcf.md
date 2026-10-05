```
private bool isStopped;

[System.Serialized]
public static GameController_IP Instance;

public float gameSpeed=8;

public bool BossWinToNextLevel= true;

// there should always be one player
public int totalPlayers= 1;

public SceneManager;

public float CameraStartPositionZ= -11;

public GameController_IP()
{
    Instance=this;
}

public void Start()
{
    // we want to keep the game controller alive right through
    // the game, so we use DontDestroyOnLoad to keep it alive
    DontDestroyOnLoad(this.gameObject);
}

public void LevelLoadingComplete()
{
    Init();
    UIControl.Init();
}

public void Init()
{
    // tell the player that it can move, in 4 seconds
    Invoke("StartPlayer",4);

    // in case we need to change the time scale, it gets set here
    Time.timeScale=gameSpeed;

    // we store the game's number of players in a pref
    // so it may be set elsewhere (the main menu for example) and
    // carried into every level of the game.
    if(PlayerPrefs.HasKey("totalPlayers")) // does this pref exist?
    {
        totalPlayers=PlayerPrefs.GetInt("totalPlayers");
        // then use the value it holds
    } else {
        totalPlayers=1; // default to single player
    }

    // find player parent transform
    playerParent=GameObject.Find("Player_Parent_Object").transform;
Vector3[] playerStarts=new Vector3[totalPlayers];
Quaternion[] playerRotations=new Quaternion[totalPlayers];
```