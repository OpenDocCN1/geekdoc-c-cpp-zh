Unity Games by Tutorials

Chapter 18: Making A Tower Defense

+   3. If there are no more enemies, the player has won, call OnGameWin().

+   4. When the Escape key is pressed, call QuitToScreen().

+   5. When the player wins, play the win audio clip and set gameOver to true.

+   6. Return to the TitleScene scene.

Now add these methods below the others:

```
//1
public void OnEnemyEscape()
{
    escapedEnemies++;
    if (escapedEnemies == maxAllowedEscapedEnemies)
    {
        // Too many enemies escaped, you lose the game
        OnGameLoss();
    }
}
//2
private void OnGameLoss()
{
    gameOver = true;
    AudioSource.PlayAtPoint(gameLossSound, Camera.main.transform.position);
    EnemyManager.Instance.DestroyAllEnemies();
    WaveManager.Instance.StopSpawning();
}
//3
public void RetryLevel()
{
    SceneManager.LoadScene("Game");
}
```

Quite simply:

+   1. If the amount of enemies that have escaped surpasses the amount allowed, OnGameLose.

+   2. Set gameOver to true, destroy all enemies that are still on the map and tell the WaveManager to stop spawning new enemies.

+   3. Reload the Game scene.

That's it for the GameManager script! Save the script and return to the editor.

Create a new empty GameObject, name it Game Manager and parent it to Managers. Add the GameManager script to it.

![](bbox=[0.118, 0.932, 0.278, 0.952])

527