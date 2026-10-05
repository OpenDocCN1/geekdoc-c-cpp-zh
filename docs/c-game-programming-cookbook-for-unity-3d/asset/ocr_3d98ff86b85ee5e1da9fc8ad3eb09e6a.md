This game uses a race manager script. As discussed at the beginning of this chapter, the race manager tracks state for both the individual players and the race overall. The game controller needs to tell the race manager, held in the variable GlobalRaceManager, that the race is beginning, and a new race should be initialized:

```
// tell race manager to prepare for the race
GlobalRaceManager.Instance.NewRace( totalLaps );
```

The spawn system requires two arrays to be passed into it for spawning the players, for the start positions and the start rotations. In this code, the arrays are initialized and populated with positions and rotations from the startPoints array:

```
// initialize some temporary arrays we can use to set up the
players
Vector3 [] playerStarts = new Vector3[numberOfRacers];
Quations [] playerRotations = new Quaternion[numberOfRacers];
```

```
// we are going to use the array full of start positions that must
// be in the editor, which means we always need to make sure
// there are enough start positions for the number of players
```

```
for ( int i = 0; i < numberOfRacers; i++)
{
    // grab position and rotation values from start position
    // transforms into the inspector
    playerStarts[i] = (Vector3) startPoints[i].position;
    playerRotations[i] = ( Quaternion ) startPoints[i].rotation;
}
```

Now that the controller has positions and rotations for the players, SpawnController may be called upon to add the players to the scene:

```
SpawnController.Instance.SetupPlayers( playerPrefab,
playerStarts, playerRotations, playerParent, numberOfRacers );
```

playerTransforms is filled with all of the transforms. We get to them by calling SpawnController.Instance.GetAllSpawnedPlayers(), which returns all of the player transforms created by the spawn controller:

```
playerTransforms=new ArrayList();
```

```
// let's grab references to each player's controller
// script
playerTransforms =
SpawnController.Instance.GetAllSpawnedPlayers();
```

When the game controller communicate with the players, it uses references to them from an array playerList. The next part of the code iterates through the playerTransform array (using the value held in numberOfRacers as a total count) and uses GameObject.GetComponent() to find each instance of the CarController_MVD.cs script attached to each player. As the code steps through each player, it also uses GetComponent() to find its AI controller script to tell it which waypoint control script to use and calls its Init() function:

```
playerList=new ArrayList();
```