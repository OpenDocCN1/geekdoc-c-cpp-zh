```
public void FaderOff()
{
    FadeCanvasGroup.alpha = 0;
}
```

Above, the fade Canvas can be hidden or displayed instantly by setting its alpha value to 0 or 1 depending on whether it's on or off.

The last function of CanvasManager is the TimedSwitchCanvas() function mentioned above:

```
public void TimedSwitchCanvas(int indexFrom, int indexTo)
{
    lastGroup = indexFrom;
    currentGroup = indexTo;
    StartCoroutine(StartFadeCanvasSwitch(_UICanvasGroups[indexFrom], _UICanvasGroups[indexTo], fadeDuration, waitBetweenFadeTime));
}
```

TimedSwitchCanvas uses the StartFadeCanvasSwitch coroutine, which you will find further on in the script below.

Below, we move on to the coroutines used for fading the Canvases:

```
public static IEnumerator FadeCanvasIn(CanvasGroup theGroup, float fadeDuration)
{
```

The FadeCanvasIn coroutine starts by declaring a locally scoped currentTime variable, which will be used to track timing during the fade.

Next, as we should never assume what alpha level the Canvas might be set at, we get the start alpha value from the Canvas itself – theGroup.alpha – and store it in another locally scoped variable named currentAlpha.

The function is fading in a Canvas, so we go ahead next and enable interactions with it as soon as the fade starts. You could move this to the end, if you wanted to lock the interaction until after the fade ends, but I like to give users access to the Canvas as soon as possible to avoid any frustration from impatient clickers!

```
theGroup.interactable = true;
theGroup.blocksRaycasts = true;
```

Now we have everything set, the next chunk of code deals with the fade:

```
while (currentTime < fadeDuration)
{
    currentTime += Time.deltaTime;
}
```

The great thing about coroutines, in my opinion, is how self-contained they are and the linear way that the code runs. The coroutine does not stop until the while condition is met, above, that is, when currentTime is not less than fadeDuration.

Each time the while loop above runs, we add Time.deltaTime to the currentTime variable – which is increasing currentTime by the amount of time since the last engine update so we know exactly how long this coroutine has been running.