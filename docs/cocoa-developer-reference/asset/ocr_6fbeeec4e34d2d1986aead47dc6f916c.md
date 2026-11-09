While this isn't the most elegant solution, it solves the problem. The finished application is shown in Figure 14.19.

As an exercise, try to extend the application so that the Album box displays the year as well as the artist name.

> > **TIP**
> >
> > One final nicety is to add an auto-refresh feature on load. The finished application implements `applicationDidFinishLaunching:` a `performSelector:withObject:afterDelay:` method calls `refreshList:` one second after start-up. This updates the album list after giving the application a short time to settle.

**Figure 14.19**
Displaying albums automatically. Selecting a new artist lists that artist's albums in the adjacent text field.

![](bbox=[0.185, 0.38, 0.63, 0.731])