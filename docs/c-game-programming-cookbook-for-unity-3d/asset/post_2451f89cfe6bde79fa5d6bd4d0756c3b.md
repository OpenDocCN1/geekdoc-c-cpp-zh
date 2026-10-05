
```cs
// this function will be called whenever an instance of the
// SpawnController class is made
// first
```

```cs
// as no instance already exists, we can safely set instance
// to this one
instance = this;

public static SpawnController Instance
{
    // to every script, this getter setter is the way they
    // get access to the singleton instance of this script
    get
    {
        // the other script is trying to access an instance
        // of this script, so we need to see if an instance
        // already exists
        if (instance == null)
        {
            // no instance exists yet, so we go ahead and
            // create one
            ScriptableObject.CreateInstance<SpawnController>(); // new SpawnController();
        }
        // now we pass the reference to this instance back
        // to the other script so it can communicate with it
        return instance;
    }
}

public void Restart() 
{
    playerTransforms=new ArrayList<Transform>();
    playerGameObjects=new ArrayList<GameObject>(); 
}

public void SetUpPlayers(GameObject[] playerPrefabs, Vector3 playerStartPositions, Quaternion[] playerStartRotations, Transform theParentObj, int totalPrefabs)
{
    // we pass in everything needed to spawn players and take
    // of spawning players in this class so that we don't
    // have to replicate this code in every game controller
    playerPrefabList= playerPrefabs;
    startPositions= playerStartPositions;
    startRotations= playerStartRotations; 
}

// call the function to take care of spawning all the
// players and putting them in the right places
CreatePlayers(theParentObj, totalPlayers);

public void CreatePlayers (Transform theParent, int totalPlayers)
{
    playerTransforms=new ArrayList();
    playerGameObjects=new ArrayList();

    for(int i=0; i<totalPlayers;i++)
    {
        // spawn a player
        tempTrans= Spawn(playerPrefabList[i], startPositions[i], startRotations[i]);

        // if we have passed in an object to parent the
        // players to, set the parent
        if(theParent!=null)
        {
            tempTrans.parent=theParent;
            // as we are parented, let's set the local
            // position
            tempTrans.localPosition= startPositions[i];
        }

        // add this transform into our list of player
        // transforms
        playerTransforms.Add(tempTrans);

        // add its gameobject into our list of player
        // gameobjects (we cache them separately)
        playerGameObjects.Add(tempTrans.gameObject);
    }
}

public GameObject GetPlayerGO (int indexNum)
{
    return (GameObject)playerGameObjects[indexNum];
}

public Transform GetPlayerTransform (int indexNum)
{
    return (Transform)playerTransforms[indexNum];
}

public Transform Spawn(GameObject anObject, Vector3 aPosition, Quaternion aRotation)
{
    // instantiate the object
    tempGO=(GameObject)Instantiate(anObject, aPosition, aRotation);
    tempTrans= tempGO.transform;

    // return the object to whatever was calling
    return tempTrans;
}

// here we just provide a convenient function to return the spawned
// objects gameObject rather than its transform
public GameObject SpawnGO(GameObject anObject, Vector3 aPosition, Quaternion aRotation)
{
    // instantiate the object
    tempGO=(GameObject)Instantiate(anObject, aPosition, aRotation);
    tempTrans= tempGO.transform;

    // return the object to whatever was calling
    return tempGO;
}

public ArrayList GetAllSpawnedPlayers()
{
    return playerTransforms;
}
```

## 4.3.1.1 Script Breakdown

The SpawnController class derives from ScriptableObject:

```cs
public class SpawnController : ScriptableObject
{
```

After the variable declarations, SpawnController.cs sets up a singleton. As it says in the comments, this is based on the work of AngryArt (published on the Unity wiki site http://wiki.unity3d.com/index.php?title=Singleton). Recall that the singleton pattern was discussed earlier in Chapter 2. If you missed it, this just takes care of only ever having one instance of the script in existence at any time so that we always use the same instance regardless of where or how it is accessed by other scripts.

```cs
private static SpawnController instance;

public SpawnController()
{
    // this function will be called whenever an instance of the
    // SpawnController class is made
    // first, we check that an instance does not already exist
    // (this is a singleton, after all!)
    if (instance != null)
    {
        // drop out if exists, to avoid generating
        // duplicates
        Debug.LogWarning("Tried to generate more than one instance of singleton SpawnController.");
        return;
    }

    // as no instance already exists, we can safely set instance
    instance = this;
}
```

After the setup functions, the script moves on to a simple Restart() function that clears out all the ArrayLists used later on by script.

The SetUpPlayers function is a very specific function designed for a specific purpose. That is, it functions to provide information about the players in the game represented by a series of arrays and an integer to say how many players are in the total. This information is not used immediately and will be used later on the script by the CreatePlayers() function.

```cs
public void SetUpPlayers (GameObject[] playerPrefabs, Vector3[] playerStartPositions, Quaternion[] playerRotations, Transform theParentObj, int totalPlayers)
{
    // we pass in everything needed to spawn players and take
    // of spawning players in this class so that we don't
    // have to replicate this code in every game controller
    playerPrefabList= playerPrefabs;
    startPositions= playerStartPositions;
    startRotations= playerRotations; 
}
```
