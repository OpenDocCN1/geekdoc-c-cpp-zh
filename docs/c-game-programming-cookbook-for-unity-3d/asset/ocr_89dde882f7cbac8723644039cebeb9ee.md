```
// this function will be called whenever an instance of the
// SpawnController class is made
// first
```

```
// as no instance already exists, we can safely set instance
// to this one
instance =;
```

# public static SpawnController Instance

```
{ // to every script, this getter setter is the way they
// get access to the singleton instance of this script
get
```

```
{ // the other script is trying to access an instance
// of this script, so we need to see if an instance
// already exists
if (instance == null)
{
    // no instance exists yet, so we go ahead and
    // create one
```

```
ScriptableObject.CreateInstance<SpawnController>(); // new SpawnController();
{ // now we pass the reference to this instance back
// to the other script so it can communicate with it
return instance;
```

# public void Restart() {

```
playerTransforms=new ArrayList<Transform>();
playerGameObjects=new ArrayList<GameObject>(); }
```

# public void SetUpPlayers(GameObject[] playerPrefabs, Vector3
playerStartPositions, Quaternion[] playerStartRotations, Transform
theParentObj, int totalPrefabs)

```
{ // we pass in everything needed to spawn players and take
// of spawning players in this class so that we don't
// have to replicate this code in every game controller
playerPrefabList= playerPrefabs;
startPositions= playerStartPositions;
startRotations= playerStartRotations; }
```