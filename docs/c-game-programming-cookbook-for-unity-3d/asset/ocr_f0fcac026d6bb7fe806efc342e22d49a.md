```
Camera.main.SendMessage("SetTarget", aTarget);
} else {
    // tell the camera script to target the player
    Camera.main.SendMessage("SetTarget",
    playerGO1.transform);
}
```

```
// finally, tell the radar about the new player
tRadarControlsScript.SetCenterObject( playerGO1.transform );
```

```
void StartPlayer() {
    // grab a reference to the main player's data manager so we
    // update its values later on (scoring, lives etc.)
    mainPlayerDataManager = 
    playerGO1.GetComponent<BasePlayerManager>().DataManager;

    // all ready to play, let's go!
    thePlayerScript.GameStart();
}
```

```
public override void EnemyDestroyed( Vector3 aPosition, int pointsValue, int hitByID) {
    // tell our sound controller to play an explosion sound
    BaseSoundController.Instance.PlaySoundByIndex(1, aPosition);

    // tell main data manager to add score
    mainPlayerDataManager.AddScore( pointsValue );

    // update the score on the UI
    UpdateScoreUI( mainPlayerDataManager.GetScore() );

    // play an explosion effect at the enemy position
Explode( aPosition );

    // tell spawn controller that we're one enemy closer to the
    // next wave
    WaveSpawnController.Fragged();
}
```

```
public void PlayerHit(Transform whichPlayer) {
    // tell our sound controller to play an explosion sound
    BaseSoundController.Instance.PlaySoundByIndex(2, whichPlayer.position);

    // call the explosion function!
Explode( whichPlayer.position );
}
```

```
public void AddEnemyToRadar( Transform aTransform) {
    theRadarControlScript.AddEnemyBlipToList( aTransform);
}
```