before tempRC. If focusPlayerScript.IsLapDone() is true and tempRC.IsLapDone() is false, the script sets isAhead to true:

```
// has the player completed a lap and is getting ready to
move onto the next one?
if ( focusPlayerScript.GetCurrentLap() &&
tempRC.GetCurrentLap() &&
focusPlayerScript.GetCurrentWaypointNum() == tempRC.GetCurrentWaypoint()
&& (focusPlayerScript.IsLapDone() == true &&
tempRC.IsLapDone() == false )
  isAhead = true;
```

A fifth and final condition does a similar check to the last one, only this time omitting any waypoint checking. The code decodes on whether the players are on the same lap and, when they are on the same lap, whether the focusPlayerScript has finished its lap or not. When focusPlayerScript.IsLapDone() is true and tempRC.IsLapDone() is false, we know the focused player is ahead and can go and set isAhead to true:

```
if ( focusPlayerScript.GetCurrentLap() &&
tempRC.GetCurrentLap() && ( focusPlayerScript.IsLapDone() ==
true && !tempRC.IsLapDone() )
  isAhead = true;
```

At this point, isAhead tells us whether or not the current player represented by focusPlayerScript-tempRC. If isAhead is true, the script can reduce the value of myPos to move the player's race position up to one:

```
if ( isAhead )
{
  myPos--;
n}
```

By the time this loop has iterated all the way through the players, myPos shows exactly which race position the focused player is. In the function ends, returning myPos:

```
return myPos;
```

Both functions StartRace() and StopRace() change the value of raceRunning (to true or false, respectively) and call the UpdateRaceState() function to tell the players ahead change:

```
public void StartRace()
{
  raceRunning=true;
  UpdateRacersRaceState();
}
public void StopRace()
{
  raceRunning=false;
  UpdateRacersRaceState();
}
```