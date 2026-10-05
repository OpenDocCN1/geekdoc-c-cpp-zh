To make the windows appear, there are some adjustments needed in both GameManager and UIManager. Open up the UIManager script and add these lines under public GameObject towerInfoWindow; :

```
public GameObject winGameWindow;
public GameObject loseGameWindow;
public GameObject blackBackground;
```

These will hold the references to the windows and the background.

Now these add methods underneath ShowTowerInfoWindow():

```
public void ShowWinScreen()
{
  blackBackground.SetActive(true);
  winGameWindow.SetActive(true);
}

public void ShowLoseScreen()
{
  blackBackground.SetActive(true);
  loseGameWindow.SetActive(true);
}
```

Each of these methods opens the corresponding window and enables the black background to block the player from clicking the towers and tower slots after the game is over.

Save this script and open the GameManager script, which is in the Scripts > Game folder. Add this line to the bottom of OnGameWin():

```
UIManager.Instance.ShowWinScreen();
```

Also add this line to the bottom of the OnGameLose() method:

```
UIManager.Instance.ShowLoseScreen();
```

These will ensure the windows show up when the player wins or loses. Save this script and return to Unity. Select UI Manager, drag Screen Canvas -> WinWindow and LoseWindow to the Win Game Window field and Lose Game Window fields respectively. Finally, drag the BlackBackground GameObject to the Black Background field.