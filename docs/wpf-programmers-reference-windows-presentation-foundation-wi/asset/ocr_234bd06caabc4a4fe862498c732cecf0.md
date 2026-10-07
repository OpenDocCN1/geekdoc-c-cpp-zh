The program’s rewind, play, pause, stop, and forward event handlers are straightforward. They simply invoke the MediaElement’s corresponding methods.

The bookmark Button’s event handler adds the MediaControl’s current position to the lstBookmarks List.

When you select an entry in the ListBox, the lstBookmarks_SelectionChanged event handler executes. After verifying that the ListBox has a selection, the code gets the selected TimeSpan, pauses the media playback, sets the control’s position to the selected TimeSpan, and updates the ScrollBar to show the new position.

When the timer’s Tick event occurs, the tmrProgress_Tick event handler sets the ScrollBar Value to show the control’s position in the media.

When the MediaElement raises its MediaOpened event, the code determines whether the control’s NaturalDuration property has a TimeSpan value and, if it does, prepares the ScrollBar to display the media’s progress.

Finally, when you scroll the ScrollBar, the program adjusts the media’s position accordingly.