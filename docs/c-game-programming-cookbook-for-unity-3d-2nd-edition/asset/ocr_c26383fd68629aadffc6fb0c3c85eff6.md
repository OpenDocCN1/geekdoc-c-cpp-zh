You may be used to the pattern now – each of these functions calls it corresponding UnityEvent. Above, it is the OnGameEnding event.

We play a little sound at the end of the game to let the player know that things did not go so well, and the game is over. __soundComponent.PlaySoundByIndex() passes in 0 to the BaseSoundController Component as the sound to play.

CallFadeOut() gets a scheduled call next, in 2 seconds time, to fade out the Scene. Then, we get a scheduled call to GameEnded() to load the main menu and quit the game in 3 seconds.

```
```csharp
public override void GameEnded()
{
    OnGameEnded.Invoke();
    LoadMainMenu();
}
```
```

GameEnded() calls its UnityEvent, then on to LoadMainMenu(). The LoadMainMenu() function will show up below, toward the end of this C# script.

```
```csharp
public override void RestartLevel()
{
    Invoke("CallFadeOut", 2f);
    Invoke("LoadSceneLoaderToRestart", 4f);
}
```
```

RestartLevel() does just that by calling CallFadeOut() to darken the Scene in 3 seconds, then it schedules a call to LoadSceneLoaderToRestart() for 4 seconds' time.

```
```csharp
void LoadSceneLoaderToRestart()
{
    SceneManager.LoadScene("blaster_sceneLoader");
}
```
```

Since the LevelVars class still has the values set up for loading the same level we are already on, all we do to have it restart is to reload the Scene loader. LoadSceneLoaderToRestart(), above, uses SceneManager.LoadScene() to tell Unity to load blaster_sceneLoader.

```
```csharp
void LoadMainMenu()
{
    SceneManager.LoadScene("blaster_menu");
}
void LoadGameCompleteScene()
{
    SceneManager.LoadScene("blaster_menu");
}
}
```
```

The final two functions of the BlasterGameManager class use SceneManager to load the blaster_menu Scene. LoadGameCompleteScene() is provided for you to customize should you use this project as a template. This is where you should put your celebration for completing the entire game or loading of another Scene to congratulate your player or something like that.

# 15.3.2 The BlasterPlayer Class

The BlasterPlayer class is a sort of glue between the Components and game logic. All of the movement of the player is taken care of by a separate Component, the