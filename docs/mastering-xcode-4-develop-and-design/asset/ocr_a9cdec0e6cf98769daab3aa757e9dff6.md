![](bbox=[0.135, 0.204, 0.718, 0.225])

**FIGURE 20.13** The Detail view navigation bar

# THE DETAIL VIEW

Whereas the Instruments view (and the tracks it records) control and display the basics of what is collected, the Detail view is where the actual trace information is shown and explored. As you toggle the Detail view, notice how the navigation bar at its top always remains visible. This lets you continue navigating the data (if only for the sake of the Extended Detail view) without the Detail view being shown.

The navigation bar (**Figure 20.13**) is composed of three separate areas. The left-most area is the instrument chooser pop-up control (which you saw in Figure 20.9). This control lets you choose which instrument’s trace information is shown in the Detail and Extended Detail views and has the same effect as clicking an instrument in the list. To the right of the instrument chooser, the display mode lets you choose how the trace information is displayed. The list of available modes depends on the selected instrument, but most have the Call Tree and Console modes in common. Finally, the rest of the bar is dedicated to navigational context (much like the Jump Bar above Xcode’s editors), letting you navigate into and out of levels of detail in the current view.

![](bbox=[0.739, 0.319, 0.932, 0.573])

**FIGURE 20.14** The active instrument’s options list

Beneath the instrument chooser control are categorical lists of filters and display options specific to the active instrument (**Figure 20.14**). These controls are visible only when both the Detail and Instruments views are shown, and their content can vary widely from instrument to instrument. A common use case is to run a time profile of your application, choose the Call Tree display mode, and then (under the Call Tree group in the filter and options list) choose to hide missing and system symbols and show only Objective-C information. This gives you a view of only your own code, as opposed to including information about the myriad system libraries against which your code links.