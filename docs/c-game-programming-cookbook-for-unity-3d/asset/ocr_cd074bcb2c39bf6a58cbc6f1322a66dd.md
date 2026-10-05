the name of the Collider to see whether it was the start/finish line trigger. If LapDone is true and the start/finish line trigger was hit, the code continues incrementing the counter in the variables lapsComplete:

```
if(
    other.name=="TRIGGER_STARTLINE" && isLapDone==true)
    // increase lap counter
    lapsComplete++;
```

As the lap is incremented, the end of this lap has been reached so we need to use the LapDone variable to track the next lap. It is reset to false here:

```
// reset our lapDone flag ready for when we finish
// the next lap
isLapDone=false;
```

The GlobalRaceManager instance needs to know when a lap completes so it can keep tabs on each player's current lap situation. The following line makes a call out to the GlobalRaceManager's CompletedLap() function and passes in this vehicle's unique ID to identify itself:

```
// tell controller we just finished a lap and
// which lap we are now on
GlobalRaceManager.Instance.CompletedLap(myID);
```

Finally, the function lets the player script know that a lap has been completed by sending a message upward through the component hierarchy. GameObject.SendMessageUp is used to call a function named LapFinished with the optional parameter to ignore whether or not the message actually gets received, to be safe:

```
// not the cleanest solution, but it means we don't
// have hardware in the game controller script
// type or the player control script at least. Here,
// we take our object and do a SendMessage call to
// it, to say the lap finished
gameObject.SendMessageUp("LapFinished",MessageOptions.DontRequireReceiver);
```

# 12.3.3 Global Race Manager

The race controller script manages data for each player and registers itself with the global race manager as it instantiates. The global race manager then takes care of managing the bigger picture, dealing with comparing players to calculate race positions and keeping tabs on laps and global state.

Below is the GlobalRaceManager.cs script in full:

```
using UnityEngine;
```