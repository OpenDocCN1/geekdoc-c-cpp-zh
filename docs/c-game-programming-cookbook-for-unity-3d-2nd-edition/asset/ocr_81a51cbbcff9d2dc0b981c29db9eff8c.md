AudioMixer.SetFloat() is used to set the volume level of our AudioMixer to the decibel value in dbVol. Next, we do the same for the music volume:

```
```csharp
public virtual void SetMusicVolumeLevel(float aValue)
{
    float dbVol = Mathf.Log10(aValue) * 20f;
    _theAudioMixer.SetFloat("MusicVol", dbVol);
}
```
```

Above, the music volume is set the same way we did the sounds volume above.

```
```csharp
private float DecibelToLinear(float dB)
{
    float linear = Mathf.Pow(10.0f, dB / 20.0f);
    return linear;
}
```
```

As mentioned earlier in this section, the user interface sliders work at a value between 0 and 1 in this example. The utility function DecibelToLinear above will take a value in decibels and return a number from 0 to 1 depending on how loud or quiet the volume should be – between the range of -80 to 20db.

```
```csharp
void ShowMainMenu()
{
    _canvasManager.TimedSwitchCanvas(2,0);
}
```
```

```
```csharp
public virtual void StartGame()
{
    _canvasManager.HideCanvas(0, false);
    _canvasManager.ShowCanvas(2, false);
    Invoke("LoadGameScene", 1f);
}
```
```

ShowMainMenu() calls on the CanvasManager Component to switch the active canvas from the loading screen (index of 2 in this example) to the main menu which has an index of 0. The index numbers refer to the Canvases position in the UI Canvas Groups list on the Canvas Manager Component on the MenuManager GameObject.

StartGame() starts by hiding the main menu Canvas and then goes on to show the loading screen. We use an Invoke() call to schedule the game to load after 1 second, which gives the CanvasManager enough time to fade out the menu and fade in the loading screen before we jump to the next Scene.

```
```csharp
public virtual void LoadGameScene()
{
    // Load your game here!
    SceneManager.LoadScene(gameSceneName);
}
```
```

LoadGameScene() does just that, utilizing SceneManager.LoadScene() to do it. The name of the Scene to load is stored in gameSceneName – this is a string you can set in the Inspector, which makes it easier to use the menu for different games without having to modify any code.

```
```csharp
public virtual void ShowOptions()
{
    // switch to options menu
}
```
```