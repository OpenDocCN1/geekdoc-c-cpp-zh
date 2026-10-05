```
// we pass in everything to spawn players and take
// care of spawning players in this class so that we don't
// have to replicate this code in every game controller
playerPrefab=playerPrefabs;
startPositions=playerStartPositions;
startRotations=playerStartRotations;
```

```
// call the function to take care of spawning all the
// players and putting them in the right places
CreatePlayers( theParentObj, totalPlayers );
```

CreatePlayers() takes all of the information passed into the SetUpPlayers() function and deals with the actual instantiation of the player objects into the game scene:

```
public void CreatePlayers ( Transform theParent, int totalPlayers )
{
    playerTransforms=new ArrayList();
    playerGameObjects=new ArrayList();
    for(int i=0; i<totalPlayers; i++)
{
        // spawn a player
        tempTrans= spawn ( playerPrefabList[i],
        startPositions[i], startRotations{i} );
```

```
// if we have passed in an object to parent the
// players to, set the parent
if(theParent!=null)
{
    tempTrans.parent= theParent;
    // as we are parented, let's set the local
    // position
    tempTrans.localPosition= startPositions[i];
```

```
// add this transform into our list of player
// transforms
playerTransforms.Add(tempTrans);
```

```
// add this gameobject into our list of player
// gameobjects (we cache them separately)
playerGameObjects.Add (tempTrans.gameObject);
```

The GetPlayerGO(indexNum) function allows us to get back some information about the players spawned by the CreatePlayers() function. It simply grabs an entry from the playerGameObjects array and returns it, so that we can always access players via a simple index number.

```
public GameObject GetPlayerGO (int indexNum)
{
```