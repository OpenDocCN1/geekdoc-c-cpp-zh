
Unity Games by Tutorials

## Chapter 19: Making Towers

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_552_0.png)

Select BtnUpgradeTower, drag TowerInfoWindow to the On Click () Object field and select TowerInfoWindow ► UpgradeTower in the method dropdown.

That's for the Tower Info Window. Now drag an instance of the StoneTower prefab into the scene from the PrefabsTower folder. Select the StoneTower onto the Pointer Click Event's Object and drag StoneTower,ShowTowerInfo in the method dropdown. Press the Apply button to save the prefab then delete Tower from the Hierarchy.

The UIManager still needs a reference to the Tower info window in order to be able to show it. Select UIManager and drag TowerInfoWindow to its Tower info field.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_552_1.png)

Save the scene and test out the new changes by pressing the Play button. Buy a tower and try to upgrade it by clicking on the tower and pressing the Upgrade button in the Tower info window.

## Win and lose windows

These are the windows that appear when the player wins or loses the game:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_552_2.png)

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

## Unity Games by Tutorials

## Chapter 19: Making Towers

| Screen Canvas | UI Manager (Script) |
|---|---|
| > TopBar | UIManager |
| > AddTowerWindow | AddTowerWindow |
| > TowerInfoWindow | TowerInfoWindow |
| Black-background | Win Game Window None (Game Object)|
| > WinWindow | Lose Game Window None (Game Object)|
| > LoseWindow | Black-background (Game Object)|

Now, add the events on both the Win and Lose windows. Select WinWindow's child BtnNextLevel and drag GameManager to the On Click () Object field. Then select GameManager > Retrylevel in the drop-down.

Now select BtnQuit, drag GameManager to its Object field and select GameManager > QuitToFullScreen in the method dropdown.

Finally, do the same for LoseWindow's children, BtnRetry and BtnQuit.

Save your course and press the Play button to test the game. Either kill or lose the game. You should be presented with either the Win or Lose window!

## Enemy health bars

Right now, there's no way of knowing how much health an enemy has left. This can be fixed by adding health bars to the enemies:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_554_0.png)

The Health Bar prefab is located in the Prefabs > UI folder. In order for it to work, the UI Manager and Enemy Manager need some additions to their scripts. Open the UIManager script and add these variables underneath public Text txtEscapedEnemies;

```
public Transform enemyHealthBars;
public GameObject enemyHealthPrefab;
```

The variable enemyHealthBars holds a reference to the parent EnemyHealthBars and enemyHealthBarPrefab stores a reference to the Health Bar prefab so new ones can be spawned.

Now, add this method underneath ShowLoseScreen() for the actual making of the health bar:

```
//1
public void CreateHealthBarForEnemy(Enemy enemy)
{
//2
GameObject healthBar = Instantiate(enemyHealthBarPrefab);
//3
healthBar.transform.SetParent(enemyHealthBars, false);
//4
healthBar.GetComponent<EnemyHealthBar>().enemy = enemy;
}
```

Going over the above method:

- 1. CreateHealthBarForEnemy accepts the enemy that needs a health bar as its parameter.
- 2. Create a new health bar.
- 3. Parent the new health bar to EnemyHealthBars.
- 4. Pass the enemy reference to the health bar.

Save this script and open up the EnemyManager script located in the Scripts > Game Enemy folder. Add this line to the bottom of the RegisterEnemy() method: UIManager.Instance.CreateHealthBarForEnemy(enemy);

This will create a new Health Bar for each enemy that spawns. Save this script and return to Unity.

Select the UIManager and drag Screen Canvas -> EnemyHealthBars from the Hierarchy to the Enemy Bars prefab. Then drag the Prefab -> UI -> Health Bar from the Project panel to the Enemy Bars prefab field.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_555_0.png)

Save the scene and run the game. You'll notice the enemies entering the map now have small health bars above their bodies!

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_556_0.png)

## Center window

The Center window is used to notify the player a new wave of enemies is coming:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_556_1.png)

Open up the UIManager script and add this variable underneath public GameObject blackBackground;

```
public GameObject centerWindow;
```

This holds the reference to the Center window. Now add this to coroutine under the CreateHealthBarForEnemy() method:

```
//1
public void ShowCenterWindow(string text)
{
    centerWindow.transform.FindChild("TxtWave").GetComponent<Text>().
    text = text;
    StartCoroutine(EnableAndDisableCenterWindow());
}
//2
private IEnumerator EnableAndDisableCenterWindow();
```

```
{
  for (int i = 0; i < 3; i++) {
    yield return new WaitSeconds(.4f);
    centerWindow.SetActive(true);
    yield return new WaitSeconds(.4f);
    centerWindow.SetActive(false);
  }
}
```

Here's what each section does:

- 1. The text of the Center window set for the parameter. Then start EnableAndDisableCenterWindow().
- 2. This enables the Center window every 0.4 seconds three times so it flickers to demand the player's attention.

Save this script and open up the WaveManager script located in Scripts > Game > Wave. Add this line inside the Wave() method, right above break;

```
UIManager.Instance.ShowWindow("Wave " + GameManager.Instance.waveNumber);
```

Since WaveManager is class responsible for making waves, it's the perfect place to let the UI Manager know to show the Center window.

Save this script and return to Unity. Time to wire up. Select UIManager in the Hierarchy and drag CenterWindow to its Center Window field.

| CenterWindow | Tower Info | TurningWindow |
|---|---|---|
| TxtWave | Win Game Window | LoseWindow |
| TowerSlots | Lose Game Window | LoseWindow |
| | Black Background | Black Background |
| | Center Window | None (Game Object)|

All set! Save your scene and press the button to test it. The Center window should flicker three times at the start of wave.

## Damage Canvas

Now open up the UIManager script for the last time to show the Damage Canvas. This has a red border to indicate an enemy has escaped.

```
public GameObject damageCanvas;
```

This is a reference to the Damage Canvas.

Now add this method and coroutine combo under the other methods:

```
//1
public void ShowDamage()
{
    StartCoroutine(DoDamageAnimation());
}
//2
private IEnumerator DoDamageAnimation()
{
    for (int i = 0; i < 3; i++) {
        yield return new WaitSeconds(.1f);
        damageCanvas.SetActive(true);
    }
    yield return new WaitSeconds(.1f);
    damageCanvas.SetActive(false);
}
```

Save this script and switch over to the GameManager script. Inside the OnEnemyEscape(), add this line under escapedEnemies++:

```
UIManager.Instance.ShowDamage();
```

Save this script and return to Unity for the final linking. Select UIManager drag Screen Canvas DamageCanvas onto the DamageCanvas field.

| Screen Canvas | Black Background | Black Background |
| --- | --- | --- |
| > DamageCanvas | Center Window | Center Window |
| > TopBar | DamageCanvas | None (Game Object)|

Now save your scene and play it to test the effect. Few enemies pass through to the exit and you'll see the red border blinking away!
