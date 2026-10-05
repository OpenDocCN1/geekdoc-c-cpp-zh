```
// check the timer to see how much time we've been playing.
// If it's more than gameTime, the game is over
if(theTimer.GetTime() > gameTime) {
    // end the game
    BattleComplete();
}
```

```
void SetPlayerLocks ( bool aState ) {
    // tell all of the players to set their locks
    for ( int i = 0; i < numberOfBattlers; i++) {
        thePlayerScript = ( CarController_TB ) playerList [i];
        thePlayerScript.SetLock(aState);
    }
}
```

private bool doneFinalMessage;

```
public void BattleComplete() {
    // tell battle manager we're done
    GlobalBattleManager.Instance.StopBattle();

    // stop the timer!
    theTimer.StopTimer();

    // now display a message to tell the user the result of the
    // battle
    if (doneFinalMessage) {
        // get the final position for our local player
        // (Which is made first, so always has the id 1)
        int finalPosition= GlobalBattleManager.Instance.
        GetPosition(1);

        if (finalPosition == 1)
            finalPositionText.text = "FINISHED 1st";

        if (finalPosition == 2)
            finalPositionText.text = "FINISHED 2nd";

        if (finalPosition == 3)
            finalPositionText.text = "FINISHED 3rd";

        if (finalPosition >> 4)
            finalPositionText.text = "GAME OVER";

        doneFinalMessage = true;
        finalPositionText.gameObject.SetActive(true);

        // drop out of the battle scene completely in 10
        // seconds...
        Invoke("FinishGame", 10);
}
}
```