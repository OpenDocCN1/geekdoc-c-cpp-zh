```
void UpdatePositions()
{
    // here we need to talk to the race controller to
    get what we need to display on screen
    theLap =
    GlobalRaceManager.instance.GetLapsDone(focusPlayerID) + 1;

    // update the display
    UpdateLapCounter(theLap);
}
```

Above, UpdatePositions() gets the lap currently being run by the player we are focusing on, whose ID is in focusPlayerID. This was another variable set in the SetupPlayers() function when we first added all of the vehicles to the Scene. The GlobalRaceManager class takes care of tracking positions and laps, and to find out how many laps the player has completed we can call GlobalRaceManager.instance.GetLapsDone(). Passing the player ID as a parameter means that it will return the current lap count of that player as an integer. We store that into the variable theLap, which is used in the next line above to pass into the UpdateLapCounter() function as a parameter. This will update the user interface lap display.

To update the user interface's lap counter, we have the function UpdateLapCounter():

```
void UpdateLapCounter(int theLap)
{
    // if we've finished all the laps we need to finish,
    let's cap the number so that we can
    // have the AI cars continue going around the track
    without any negative implications
    if (theLap > totalLaps)
        theLap = totalLaps;

    // now we set the text of our GUIText object lap
    count display
    _uiManager.SetLaps(theLap, totalLaps);
}
```

The current lap number is passed into UpdateLapCounter() as a parameter, then it gets checked to make sure that the lap number is within the total laps for the race. If it is too high, it will be capped at the value of totalLaps.

A class named RaceUIManager will deal with setting the Text object in the Scene – this is added as a Component to the GameManager GameObject in our core Scene.

We call out to _uiManager to SetLaps() above, passing in the current lap and total number of laps as parameters. This will be displayed as 'Lap x/x'.

When the race is over, RaceComplete() is called to start bringing everything to a halt:

```
public void RaceComplete()
{
    // set all players to AI so that they continue driving
    for (int i = 0; i < _playerList.Count; i++)
    {
        // set to AI
        _playerList[i].AIControlled = true;
        // disable the keyboard input Component for
        AI players..
        _playerList[i].GetComponent<RaceInputController>().SetInput
        Type(RaceInputController.InputTypes.noInput);
    }
}
```