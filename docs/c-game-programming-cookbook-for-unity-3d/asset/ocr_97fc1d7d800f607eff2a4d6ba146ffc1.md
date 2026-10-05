If the vehicle has been going the wrong way for too long, the function Respawn() is called to put it back on the track facing in the right direction:

```
// it's been x resetTime seconds in the wrong way
// way, let's respawn this thing:
Respawn();
```

```
} else if (isAIControlled) {
```

When this condition is met, the car is not going the wrong way and it is not an AI-controlled vehicle so a call is made to the game controller to UpdateWrongWay(), telling that we are not going the wrong way so that the UI may be updated accordingly:

```
GameController_MVD.Instance.UpdateWrongWay(false);
}
```

In racing games, one common method for keeping the game interesting is to employ something rubber banding. It gets its name from the type of effect that happens when the top speed of racers is increased when they fall too far behind and decreased when they get too far ahead—the players rubber band in front and behind the main player.

Done with some subtlety, rubber banding can help to provide an exciting race each time. When it is not handled well, the effect can be frustrating as the AI players gain the lead time the player starts ahead, so use it with caution! This really is one of those unseen parts of the game that needs to be carefully balanced but, despite having such a strong impact on gameplay, most players will not even notice.

To tell it is time for an AI player to go faster and when it is for that player to go slower, the code here uses RacePosition to see where this player stands. If myRacePosition is greater than 3—meaning that this player is in fourth place or worse—then the maximum acceleration rate of the vehicle, in the variable accelMax, is set to catch accelMax to make it faster. If the position of this player is first (myRacePosition<2), then accelMax is set to the original acceleration rate held by originalAccelMax multiplied by 0.25, slowing down the vehicle:

```
accelMax = originalAccelMax;

// catch up if this car is falling behind in the race
if(isRacingRunning && isAIControlled)
{
    if(myRacePosition>3)
    {
        // speed up
        accelMax = catchUpAccelMax;
    } else {
        accelMax= originalAccelMax;
    }
}

// first place, let's slow you down!
if(myRacePosition<2)
```