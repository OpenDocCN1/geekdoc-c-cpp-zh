```
// NOTE: if you change the name of the function
// PlayerFinishedRace, make sure it isn't the same as any
// functions in any other script attached to the
// // player, or you could cause problems
gameObject.SendMessageUpwards("PlayerFinishedRace*",
finalRacePosition, SendMessageOptions.DontRequireReceiver);
}
```

```
public void RaceStart()
{
    isFinished=false;
    raceRunning=false;
}
```

```
public bool IsFinished()
{
    return isFinished;
}
```

```
public int GetCurrentLap()
{
    return GlobalRaceManager.Instance.GetLapsDone(myID) +1;
```

```
public void ResetLapCounter()
{
    GlobalRaceManager.Instance.ResetLapCount(myID);
}
```

```
public int GetCurrentWaypointNum()
{
    return currentWaypointNum;
}
```

```
public float GetCurrentWaypointDist()
{
    return currentWaypointDist;
}
```

```
public bool IsFinished()
{
    return isFinished;
}
```

```
public bool IsLapDone()
{
    return isLapDone;
}
```

```
public void UpdateRaceState(bool aState)
{
    raceRunning=aState;
}
```

```
public void SetWayController(Waypoints_Controller aControl)
{
    waypointManager=aControl;
}
```