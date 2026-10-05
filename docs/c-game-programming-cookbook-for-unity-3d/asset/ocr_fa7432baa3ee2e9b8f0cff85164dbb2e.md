focusPlayerScript.howMany_fraggedOthers contains a count of how many other players this script has fragged.

There is code in this script for three different systems of a player moving up in. The first one only takes into account the number of frags. Whoever has fragged the others gets higher in the ranking. This is commented out in the example game, as it uses the second ranking system further on in the script:

```
// if (focusPlayerScript.howMany_fraggedOthers >\n // tempRC.howMany_fraggedOthers )\n // isAhead=true;
```

When both players have fragged the same amount, ranking will be based on ID. Higher ID will come first on the score board:

```
// check here to see if the frag count is\n // the same and if so we use the id to sort\n // them instead\nif( focusPlayerScript.howMany_fraggedOthers\n == tempRC.howMany_fraggedOthers &&\nfocusPlayerScript.GetID() > tempRC.GetID() )\nisisAhead=true;
```

The third and final condition takes both the number of frags and subtracts it from the number of times this player has fragged:

```
if( focusPlayerScript.howMany_fraggedOthers - focusPlayerScript.\nhowMany_frags ) > ( tempRC.howMany_fraggedOthers -\nfocusPlayerScript.howMany_frags ) )nnisAhead=true;
```

If one of the conditions has set isAhead to true, the myPos variable is decremented, which moves the player up in the rankings. The loop then completes or goes through this process again:

```
{\n if ( isAhead )\n myPos--;\n }\n }\n return myPos;
```

The game controller will call StopBattle() when the game StopBattle() sets battleRunning to false, then calls UpdateBattleStates() to tell all of the battle controllers about the change:

```
public void StopBattle()\{
 // we don't want to keep calling everyone to tell them about\n // the battle being over if we've already done it once, so\n // check first battleRunning is true\n if(battleRunning=true)\n}
```