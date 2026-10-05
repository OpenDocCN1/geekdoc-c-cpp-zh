
```csharp
// check the timer to see how much time we've been playing.
// If it's more than gameTime, the game is over
if(theTimer.GetTime() > gameTime) {
    // end the game
    BattleComplete();
}
```

```csharp
void SetPlayerLocks ( bool aState ) {
    // tell all of the players to set their locks
    for ( int i = 0; i < numberOfBattlers; i++) {
        thePlayerScript = ( CarController_TB ) playerList [i];
        thePlayerScript.SetLock(aState);
    }
}
```

private bool doneFinalMessage;

```csharp
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

```csharp
void FinishGame ()
{
    Application.LoadLevel( mainMenuSceneName);
}
```

```csharp
void ShowCount1 ()
{
    count1.SetActive( true);
    count2.SetActive(false);
    count3.SetActive(false);
}
```

```csharp
void ShowCount2 ()
{
    count1.SetActive(false);
    count2.SetActive(true);
    count3.SetActive(false);
}
```

```csharp
void ShowCount3 ()
{
    count1.SetActive(false);
    count2.SetActive(false);
    count3.SetActive(true);
}
```

```csharp
void FinishedCount ()
{
    HideCount();
    // let the timer begin!
    theTimer.StartTimer();
}
```

```csharp
void HideCount ()
{
    count1.SetActive(false);
    count2.SetActive(false);
    count3.SetActive(false);
}
```

```csharp
public void PlayerHit(Transform whichPlayer)
{
    // tell our sound controller to play an explosion sound
    BaseSoundController.Instance.PlaySoundByIndex(1,
    whichPlayer.position);
}
```

```csharp
// call the explosion function!
// Explode(whichPlayer.position);
```

```csharp
public void PlayerBigHit(Transform whichPlayer)
{
    // tell our sound controller to play an explosion sound
    BaseSoundController.Instance.PlaySoundByIndex(2,
    whichPlayer.position);
}
```

```csharp
// call the explosion function!
// Explode(whichPlayer.position);
```

```csharp
public void Explode ( Vector3 aPosition )
{
    // instantiate an explosion at the position passed into this
    // function
    Instantiate( explosionPrefab,aPosition, Quaternion.identity );
}
```

## 13.4.1 Script Breakdown

GameController_TB is very similar to the game controller used in the example Metal Vehicle Doom. It derives from the BaseGameController class and uses lots of the same logic, so rather than repeat everything here I will highlight the main differences and go through those, instead.

As per the other game control scripts in this unit, it derives from BaseGameController:

```csharp
using UnityEngine;
using System.Collections;
```

```csharp
public class GameController_TB : BaseGameController
{}
```

There are a few differences in the Init() function worth mentioning:

```csharp
void Init()
{
    SpawnController.Instance.Restart();

    // in case we need to change the timescale, it gets set here
    Time.TimeScale = gameSpeed;
}
```

Unlike Metal Vehicle Doom, there is no lap counting in this script—the player's position, in a leaderboard-style scoring system, is tracked by the battle controller and battle manager scripts. Here in the Init() function where GlobalBattleManager gets all to initialize:

```csharp
// tell battle manager to prepare for the battle
GlobalBattleManager.Instance.NewBattle();
```

Just like Metal Vehicle Doom, all of the players' start positions and rotations are copied into new arrays to be fed to the SpawnController to set up:

```csharp
// initialize some temporary arrays we can use to set up the players
Vector3 [playerStarts] = new Vector3[numberOfBattlers];
Quaternion [playerRotations] = new Quaternion[numberOfBattlers];
```

we are going to use the full array of start positions that must
// be set in the editor, which means we always to make sure
// that there are enough start positions for the number of players

```csharp
for ( int i = 0; i < numberOfBattlers; i++)
{
    // grab position and rotation
    playerStarts[i] = (Vector3)playerList[i].transform.position;
    playerRotations[i] = playerList[i].transform.rotation;
}
```
