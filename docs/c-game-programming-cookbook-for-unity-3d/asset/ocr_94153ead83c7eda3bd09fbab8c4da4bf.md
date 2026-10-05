playerStarts [i] = (Vector3) startPoints [i].position;
playerRotations [i] = ( Quaternion ) startPoints [i].rotation;
}

One important thing to note is that the first player listed in the playerPrefab(set in the Unity Inspector window) should be the user's player prefab and not an AI–script is based on the assumption that the first player will always be the one to focus on UI, scoring, and game following, etc.:

```
SpawnController.Instance.SetUpPlayers( playerPrefabList,
playerStarts, playerRotations, playerParent, numberOfOfBattlers);

playerTransforms=new ArrayList();
```

```
// now let's grab references to each player's controller script
playerTransforms=SpawnController.Instance;
GetAllSpawnedPlayers();
```

```
playerList=new ArrayList();

for ( int i = 0; i < numberOfOfBattlers; i++) {

Transform tempT=(Transform)playerTransforms[i];
CarController_TB tempController=
tempT.GetComponent<CarController_TB>();

playerList.Add(tempController);
BaseAIController tempA=tempController.GetComponent
<BaseAIController>());

tempController.Init();
}
```

The players in Tank Battle are going to know which gameObject the player is, to be able to chase and track it. The game with all the tanks defaulting to the user. This behavior will fail, be overridden by the AI if it gets close to another AI opponent, it will attack a close target regardless of whether or not it is the user.

Here the condition is to see whether the loop (i) is at a value greater than 0 so that we know this is not a user (remember that users are always the first player in the playerPrefab array will always be 0 index):

```
if (i>0) {
}
```

The SpawnController.Instance.GetPlayerGO() function gives back the gameObject for a specific player based on its ID passed as a parameter:

```
// grab a ref to the player's gameObject
// later use
playerGO1 = SpawnController.Instance.GetPlayerGO( 0 );
```

Next, the user's transform is passed to the AI player with a call to SetChaseTarget:

```
// tell AI to get the player!
tempAI.SetChaseTarget( playerGO1.transform );
```