Again, you can see above that there are two versions of the same function – one that only takes the index of the Canvas and the other taking the index and an additional Boolean to specify fade mode, in the same way that HideCanvas() did.

The only differences between HideCanvas() and ShowCanvas() are that, above, we call the coroutine FadeCanvasIn() rather than FadeCanvasOut() from the HideCanvas() function – and the alpha gets set to 1 instead of 0 when we are dealing with the no fade code.

Next up, LastCanvas():

```
```csharp
public void LastCanvas()
{
    TimedSwitchCanvas(currentGroup, lastGroup);
}
```
```

Often you need to provide a method to get from a sub-menu back to the main menu, or back to the previous screen. To speed up the process of developing menus with this behavior, we have the LastCanvas() function, which changes the Canvas currently being displayed to the last one. It uses the variable lastGroup to keep tabs on what was previously open. As this is only a single level system, if you need to get back from multiple levels of menu you will need to extend this further or manually set which menu should display next.

In LastCanvas(), notice that it is not using a coroutine this time, but instead a function named TimedSwitchCanvas() that will coordinate the timing to switch Canvases. TimedSwitchCanvas takes two array index values – the first, the Canvas to hide and the second value is the Canvas to show. TimedSwitchCanvas() will carry out a fade out, a pause (specified by WaitBetweenFadeTime variable, accessible via the Inspector) and then fade in the new Canvas. This means to fade out a UI Canvas and to fade in another one, we can use TimedSwitchCanvas() without having to deal with the timing between fades.

The FadeIn() and FadeOut() functions are next:

```
```csharp
public void FadeOut(float timeVal)
{
    StartCoroutine(FadeCanvasIn(FadeCanvasGroup, timeVal));
}

public void FadeIn(float timeVal)
{
    StartCoroutine(FadeCanvasOut(FadeCanvasGroup, timeVal));
}
```
```

FadeIn() and FadeOut() use the FadeCanvasIn and FadeCanvasOut coroutines to fade in or out a specific Canvas – the reference to which is held in the variable FadeCanvasGroup. As mentioned earlier in this section, CanvasManager provides a method for easily fading a Scene in or out using the above code.

When a Scene first loads, the fade Canvas needs to cover the screen for a fade out effect to work, so we also need functions to snap the fade Canvas on or off as needed:

```
```csharp
public void FaderOn()
{
    FadeCanvasGroup.alpha = 1;
}
```
```