```
// first, we need to find the player that we're trying to
// calculate the position of
focusPlayerScript= (BattleController)
battleControllers(ofWhichID);
```

```
// start with the assumption that the player is in last
// place and work up
myPos = numberOfBattlers;
for (int b = 1; b < numberOfBattlers; b++)
{
    // assume that we are behind this player
    isAhead = false;

    // grab a temporary reference to the 'other' player
    // we want to check against
    tempRC = (BattleController) battleControllers[b];

    // if car 2 happens to be null (deleted for example)
    // here's a little safety to skip this iteration
    if(tempRC==null)
        continue;
}
if (focusPlayerScript.GetID() != tempRC.GetID())
{ // << make sure we're not trying to compare same objects
    // check to see if this player has fragged
    if (focusPlayerScript.howMany_fraggedOthers
        > tempRC.howMany_fraggedOthers )
    {
        isAhead=true;
        // we check here to see if the frag count is
        // the same and so we use the id to sort
        // them insist
        if (focusPlayerScript.howMany_fraggedOthers
            == tempRC.howMany_fraggedOthers &&
            focusPlayerScript.GetID() == tempRC.GetID())
            isAhead=true;
            // alternative version just for fun... counts
            // fragged times too
            // check to see if this player has fragged
            if (focusPlayerScript.howMany_fraggedOthers
                - focusPlayerScript.howMany_frags ) >
                tempRC.howMany_fraggedOthers -
                focusPlayerScript.howMany_frags ))
                isAhead=true;
    }
}

if ( isAhead)
{
    myPos--;
}
return myPos;
```