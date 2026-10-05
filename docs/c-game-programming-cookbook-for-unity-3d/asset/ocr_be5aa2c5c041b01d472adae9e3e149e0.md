As with players,gameObjects used to define player start positions are stored in
array called startPoints (again, its references are set in the Inspector window of the Unity
editor. Note that there needs to be at least the same amount of start positions as players
for this function to work (as each player will need one).

The function iterates through the start position objects to get at positions and rotations
from them and store each one into the playerStarts and playerRotations:

```
// initialize temporary arrays we can use to set up the
// players
Vector3 [i] = new Vector3 [numberOfOfPlayers];
Quaternion [i] playerRotations = new Quaternion [numberOfOfPlayers];

// we are going to use the array for of start positions that must
// be in the editor, which means we always need to make sure
// there are enough start positions for the number of players

for ( int i = 0; i< numberOfOfPlayers; i++ )
{
    // grab position and rotation values from start position
    // transforms set in the inspector
    playerStarts[i] = (Vector3)startPoints[i].position;
    playerRotations[i] = (Quaternion)startPoints[i].rotation;
```

Now that the function has arrays for players, start positions and rotations, it can
call upon the SpawnController's instance SetUpPlayers() function to bring them into the
game scene:

```
SpawnController.Instance.SetUpPlayers( playerPrefabList,
playerStarts,playerRotations, playerParent, numberOfOfPlayers );
```

At some point, it is inevitable that this script will need to communicate with the players.
The player transforms get stored in an ArrayList called playerTransforms and references to
they control scripts (instances of PLAYER_LBS.cs) held in an array named playerList.
The SpawnController returns an ArrayList() back from GetAllSpawned
Transforms() that we use to iterate through to get each Player_LBS instance with
GetComponent():

```
playerTransforms=new ArrayList();

// now let's grab references to each player's controller script
playerTransforms =
SpawnController.Instance.GetAllSpawnedTransforms();

playerList=new ArrayList();

for ( int i = 0; i< numberOfOfPlayers; i++ )
{
    tempT=(Transform)playerTransforms[i];
    Player_LBS tempController=
    tempT.GetComponent<Player_LBS>();
    playerList.Add(tempController);
    tempController.Init ( );
}
```