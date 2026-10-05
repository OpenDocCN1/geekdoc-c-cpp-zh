```
SaveHighScore();

// show the game over message
gameOverMessage.SetActive(true);
}
```

The UI code uses OnGUI() to render, which is a function called automatically by the Unity engine. The problem with OnGUI() is that it may be called several times every frame, which causes a huge performance hit on mobile devices. If you are intending to converting the game over to run on a mobile system, you may want to look at other GUI solutions instead.

GUI.Label is a simple method for drawing text onto the screen. For this example game, it is used for all of the UI:

```
void OnGUI()
{
    GUI.Label(new Rect (10,100,100,50),"PLAYER 1");
    GUI.Label(new Rect (10,40,100,50),"SCORE "+player_score");
    GUI.Label(new Rect (10,70,200,50),"HIGH SCORE "+player_highscore");
    
    GUI.Label(new Rect (10,100,100,50),"LIVES "+player_lives");
}
```