```
{
  if (UIControl l == null)
    UIControl.UpdateScoreP2(int aScore);
  }
  public void UpdateLivesP2(int aScore) {
    if (UIControl l == null)
      UIControl.UpdateLivesP2(int aScore);
  }
}
```

Player_SpaceShip_IP.cs will deal with the player's health/lives management, but when a player runs out of lives, it calls the PlayerDied() function so that the game controller can decide whether or not the game is actually over. If this is a single-player game, the game can end right after this function call, but if it is a two-player game, we need to make sure that both players have lost all their lives before ending the game completely:

```
public void PlayerDied(int whichID) {
}
```

The ID of the player with no lives left is passed in as a parameter named whichID. This is used to set player1Dead or player2Dead to true, depending on the ID number:

```
if (whichID==1)
  player1Dead=true;

if (whichID==2)
  player2Dead=true;
```

This part of the code checks to see whether this is a two-player game and, if so, tells the UIControl script to show the game-over message. A call to Exit() is scheduled by an Invoke 5 seconds later:

```
if(player1Dead && player2Dead && totalPlayers>1) {
  // both players are dead, so end the game
  UIControl.ShowGameOver();
  Invoke("Exit",5);
}
```

When TotalPlayers is 1, this must be a single-player game, so there is only a need for one call to happen to this function for it to show the game-over message and end the game:

```
else if(totalPlayers==1) {
  // this is a single-player game, so just end the game now
  // both players are dead, so end the game
  UIControl.ShowGameOver();
  Invoke("Exit",5);
}
```