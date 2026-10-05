Now that this function has the player's race position and current lap number,
numbers are fed to the UI system to be displayed on screen:

```
// update the display
UpdateRacePositionText();
UpdateLapCounter(theLap);

```

The game controller for this game also deals with updating the text on the user inter-
face count count. The current lap number is passed into UpdateLapCounter() as
parameter, and then it gets checked to make sure that the lap number is within the
laps for the race. If it is too high, it will be capped at the value of totalLaps before the
user interface is set:

```
void UpdateLapCounter (int lap)
{
// if we've finished all the laps we need to finish, let's say cap
// number so that we can have the AI cars count going around the
// track without any negative implications
if (lap > totalLaps) 
theLap = totalLaps;
}
```

```
// we now set the text of the GUI object lap count display
lapText.text = "Lap " + theLap.ToString() + " * of " +
totalLaps.ToString();

```

The UpdateRacePositionText() function updates the text on the position display (
objectText is type of GUIText, referenced via the Unity editor Inspector window).
The string is composed of the value of focusPlayerRacePosition and the numberOfRacers.
Note that the function uses .ToString() to make the conversion between the value and the
string. This appears to be optional in Unity, but it is used here as security in case this
changes in the future:

```
void UpdateRacePositionText ()
{
posText.text = "Pos " + focusPlayerRacePosition.ToString() + " of " +
numberOfRacers.ToString();
}
```

When the race is over, RaceComplete() gets called with an integer parameter contain-
he main player's final position. This is used to compose a message to relay the final
position back to the user via the GUI object finalText.

The function begins by checking doneFinalMessage to make sure that the message is
already being displayed (that should not happen, but I prefer to check it to keep every-
thing safe against any unforeseen calls);

```
public void RaceComplete (int finalPosition)
{
if (!doneFinalMessage)
(
```