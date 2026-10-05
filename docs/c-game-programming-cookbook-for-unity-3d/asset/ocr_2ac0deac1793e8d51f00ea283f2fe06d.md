```
return (int)battlePositions[anID);

private string posList;
private int whichPos;

public string GetPositionListString() {
    // this function builds a string containing a list of
    // players in order of their scoring positions
    // we step through each battler and check its
    // positions and build a hash table that can be
    // accessed by using the position as an index
    for (int b = 1; b < numberOfOfBattlers; b++) {
        whichPos= GetPosition( b );
        tempRC = (BattleController) battleControllers [b];
        sortedPositions[whichPos] = tempRC.GetID();

        if(sortedPositions.Count<numberOfOfBattlers) {
            return "";
        }

        posList="";
        // now we have a populated sortedPositions hash table, let's
        // iterate through it and build the string
        for (int b = 1; b <= numberOfOfBattlers; b++) {
            whichPos=(int)sortedPositions[b];
            posList=posList+b.ToString()+". PLAYER "+whichPos+\
";
        }
        return posList;
    }

public int GetPosition ( int ofWhichID ) {
    // first, let's make sure that we are ready to go (the
    // hashtables may not have been set up yet, so it's
    // best to be safe and check this first
    if(battleControllers==null) {
        Debug.Log("GetPosition battleControllers is NULL!");
        return -1;
    }

    if(battleControllers.ContainsKey(ofWhichID)==false) {
        Debug.Log("GetPosition says no battle controller found for id "+ofWhichID);");
        return -1;
    }
```