# Unity Games by Tutorials
Chapter 11: Introducing the UI

```
singleton.enemiesLeft--;nsingleton.gameUI.SetEnemyText(singleton.enemiesLeft);

// Give player bonus for clearing the wave before timer is done
if (singleton.enemiesLeft == 0)
{
    singleton.score += 50;
    singleton.gameUI.ShowWaveClearBonus();
}
```

This will be called when robots are killed. It removes one robot from the enemy count and updates the UI. If there are no enemies left, it alerts the player of a bonus score they earned and it adds "50" to the score.

The player should also get points every time they kill a robot. Add the following method just below the last one:

```
public void AddRobotKillToScore()
{
    score += 10;
    gameUI.SetScoreText(score);
}
```

This will give the player points when they kill a robot.

The player should also get one point for every second they survive an attack. Add the following method below the last one:

```
IEnumerator increasesScoreEachSecond()
{
    while (!gameOver)
    yield return new WaitForSeconds(1);
    score += 1;
    gameUI.SetScoreText(score);
}
```

The above is a coroutine that updates the score every single second when the game is running.

Now, you need to update Start() to set up your new variables. Add the following after the line containing singleton = this;

```
StartCoroutine("increaseScoreEachSecond");
isGameOver = false;
time.timeScale = 1;
waveCountdown = 30;
enemiesLeft = 0;
StartCoroutine("updateTimer");
```

![](bbox=[0.118, 0.933, 0.268, 0.953])

312