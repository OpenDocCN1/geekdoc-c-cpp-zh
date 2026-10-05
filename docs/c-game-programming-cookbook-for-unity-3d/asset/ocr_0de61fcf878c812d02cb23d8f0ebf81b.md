```
public GameObject gameOverMessage;
public GameObject getReadyMessage;
```

```
void Awake () {
    Init();
}
```

Before showing the main UI, the player_highscore variable needs to be populated with the high score saved in a PlayerPrefs file. The function LoadHighScore() is called to set up:

```
void Init () {
    LoadHighScore();
}
```

Both messages (gameOverMessage and getReadyMessage) are hidden at the start of the game by calling the HideMessages() function:

```
HideMessages ();
```

The message to get ready (the reference to which is in the getReadyMessage) will be on screen in 1 second after the function call, as set up by the Invoke command:

```
Invoke("ShowGetReady", 1);
```

The get-ready message stays on the screen for another second before the following Invoke call is activated and the message hidden from view:

```
Invoke("HideMessages", 2);
```

In HideMessages(), both messages are hidden using the GameObject.SetActive() function:

```
public void HideMessages() {
    gameOverMessage.SetActive(false);
    getReadyMessage.SetActive(false);
}
```

The function dedicated to showing the get-ready message is called from the Init() function via Invoke:

```
public void ShowGetReady() {
    getReadyMessage.SetActive(true);
}
```

When the game has ended, ShowGameOver() gets called. The high score is saved into the PlayerPrefs file and the message set to active (shown) via GameObject.SetActive():

```
public void ShowGameOver() {
}
```