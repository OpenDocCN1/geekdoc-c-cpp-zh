Here we check whether this player has finished the race (by checking its entry
in raceLaps the variable totalLaps), and if it has finished, this player's entry in the
raceFinished Hashtable is updated to true:

```
if((int) raceLaps[anID]==totalLaps)
    raceFinished[anID] = true;
```

The function now retrieves this player's race controller from the raceControllers Hashtable,
that it can call on its RaceFinished() function to let it know that this player's race is over:

```
// tell the race controller
// finished racing
tempRC = (RaceController) raceControllers [anID];
tempRC.RaceFinished();
```

If there is ever a need to restart the race for a specific player, ResetLapCount() takes a
player ID number and resets its entry in the raceLaps Hashtable to 0:

```
public void ResetLapCount(int anID)
{
    // if there's ever a need to restart the race and reset laps
    // for this player, we reset its entry
    // in the raceLaps hashtable here
    raceLaps[anID]=0;
}
```

This function calculates race positions is an on-demand system whereby it is
only updated when a position is requested. When GetPosition() is called, the code checks
that raceControllers is not null, making sure that everything has been set up correctly:

```
public int GetPosition ( int ofWhichID)
{
    // first, let's make sure that we are ready to go (the
    // hashtables may not have been set up yet, so it's
    // best to be safe and check this first)
    if(raceControllers==null)
{
        Debug.Log("GetPosition raceControllers is NULL!");
        return -1;
    }
```

We need to know for the raceControllers Hashtable contains an entry for the
ID being passed in as a parameter to this function call, or the function will fail later
along the code:

```
if(raceControllers.ContainsKey(ofWhichID)==false)
{
    Debug.Log("GetPosition says no race controller
found for id "+ofWhichID);");
    return -1;
}
```