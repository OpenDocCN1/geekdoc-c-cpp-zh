# # Chapter 7 Introducing Expression Blend

After developers spend a few seconds thinking about the fact that transitioning between different visual states is all done smoothly with animations, they start to see the power of this framework.

This means that when a Silverlight object transitions from one visual state to another, it does so with an animated storyboard. You can control how long it takes to switch to this new state and any special effects that occur as a result of this switch.

As a curmudgeonly as I am about using visual design tools, I must admit that hand-typing in all the visual state management stuff, even for simple property changes, is going to get really old really fast. I am a firm believer in using the best tool for the job, and I know that working with visual states is absolutely best done in Blend.

Here's a little food for thought and an assignment to do some exploring on your own with Blend: Stock controls come with their own visual states, and different user interaction will switch a control between visual states. A page is just a different type of control. This means that a page can have visual states and you can create your own custom visual states.

One of the biggest pains when building UIs for the iPad and iPhone is dealing with rotation. Making sure that the user interface looks good when rotated between landscape and portrait is a difficult and time-consuming process, especially when you consider that you often need to hand-code property changes to your views when the user rotates the phone or the iPad. What if you were to assign names to your visual states such as “portrait” and “landscape” or “portraitup,” and so on? Now all you need to do in Blend is rotate the design surface to the right orientation and, in that particular visual state, record mode, move and resize all your controls accordingly. Next, you need to programmatically transition your page’s visual state every time the device changes orientation.

Here is some code you can override in your MainPage.xaml.cs that will programmatically transition the page from its current visual state to the new one, invoking any custom animations, layout changes, color changes, and whatever else you want done. Again, remember that all these changes can be done in a timed, animated storyboard.

```
protected override void OnOrientationChanged(OrientationChangedEventArgs e)
{
    // if you have 4 states instead of 2
    // PortraitUp, PortraitDown, LandscapeLeft, LandscapeDown
    // VisualStateManager.GoToState(this, e.Orientation.ToString(), true);
    // if you just have Portrait or Landscape
    string orientation = (e.Orientation & PageOrientation.Portrait) != 0
        ? "Portrait" : "Landscape";
    VisualStateManager.GoToState(this, orientation, true);
    base.OnOrientationChanged(e);
}
```