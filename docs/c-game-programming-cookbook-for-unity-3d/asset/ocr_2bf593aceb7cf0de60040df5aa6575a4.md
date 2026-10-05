there is no script attached to the same GameObject with the function PlayerFinishedRace(), the parameter SendMessageOptions.DontRequireReceiver is used, which means that no errors or warnings will occur if there is no script to receive the message:

```
gameObject.SendMessage("PlayerFinishedRace",
    finalRacePosition, SendMessageOptions.DontRequireReceiver);
```

At RaceStart(), our internal state variables are Finished and raceRunning are set to false. Note that raceRunning starts out false because it will be set by another function, a little further on from the initialization of this script:

```
public void RaceStart()
{
    isFinished=false;
    raceRunning=false;
}
```

Other scripts may need to know whether this player has finished racing. The IsFinished() function will return a Boolean to that effect:

```
public bool IsFinished()
{
    return isFinished;
}
```

When other scripts need to find out what the player's current lap is, the GetCurrentLap() function gets the latest information by the player's ID as a parameter (so that the global race manager knows who is asking for their lap count) and adds 1 to the return value from GlobalRaceManager.Instance.GetLapsDone() will be how many laps are completed, what the current lap is:

```
public int GetCurrentLap()
{
    return GlobalRaceManager.Instance.GetLapsDone(myID)+1;
}
```

The game could be reset by another script, calling for the lap counter for this player to be reset, too. The GlobalRaceManager object provides the ResetLapCount() function for this, with its parameter being the unique ID from myID:

```
public void ResetLapCount()
{
    GlobalRaceManager.Instance.ResetLapCount(myID);
}
```

This race controller script tracks where the player is on the track by monitoring its progress along a path of waypoints. In the example here, those waypoints are the ones used to drive the AI players around. By keeping tags on the waypoints, this script may be accessed to find where the car is and compare it to other cars are and calculate race positions. GetWaypointNum() will return the player's current-WaypointNum integer variable: