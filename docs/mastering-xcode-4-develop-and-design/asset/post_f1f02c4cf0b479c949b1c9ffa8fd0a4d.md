
**Figure 20.8** The CPU strategy

**Figure 20.9** The instrument chooser pop-up

**Figure 20.10** The Threads strategy

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_348_0.png)

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_348_1.png)

## The Instruments View

The Instruments view (**Figure 20.11**) shows a list of all instruments (or cores or threads, depending on the selected strategy) in the top list. Each instrument can be selected by clicking it in the list. Once selected, pressing the Delete key will remove the instrument (and its data for all recorded sessions) from the trace document. Click the info button (i) to the right of each instrument to reveal a popover (**Figure 20.12**) that offers more trace recording data and track display options.

> **NOTE:** The control immediately below the list of instruments zooms in and out of the timeline. It is not actually part of the Instruments view and remains where it is when the view is toggled. Similarly, the instrument chooser pop-up seen in Figure 20.9 belongs to the navigation bar of the Detail view.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_349_0.png)

**Figure 20.13** The Detail view navigation bar

## The Detail View

Whereas the Instruments view (and the tracks it records) control and display the basics of what is collected, the Detail view is where the actual trace information is shown and explored. As you toggle the Detail view, notice how the navigation bar at its top always remains visible. This lets you continue navigating the data (if only for the sake of the Extended Detail view) without the Detail view being shown.

The navigation bar (**Figure 20.13**) is composed of three separate areas. The left-most area is the instrument chooser pop-up control (which you saw in Figure 20.9). This control lets you choose which instrument’s trace information is shown in the Detail and Extended Detail views and has the same effect as clicking an instrument in the list. To the right of the instrument chooser, the display mode lets you choose how the trace information is displayed. The list of available modes depends on the selected instrument, but most have the Call Tree and Console modes in common. Finally, the rest of the bar is dedicated to navigational context (much like the Jump Bar above Xcode’s editors), letting you navigate into and out of levels of detail in the current view.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_349_1.png)

**Figure 20.14** The active instrument’s options list

Beneath the instrument chooser control are categorical lists of filters and display options specific to the active instrument (**Figure 20.14**). These controls are visible only when both the Detail and Instruments views are shown, and their content can vary widely from instrument to instrument. A common use case is to run a time profile of your application, choose the Call Tree display mode, and then (under the Call Tree group in the filter and options list) choose to hide missing and system symbols and show only Objective-C information. This gives you a view of only your own code, as opposed to including information about the myriad system libraries against which your code links.

**Figure 20.15** The Detail view showing call tree information

The main view (usually a table or outline) lists the individual data points that Instruments gathered about your application; the information it shows is specific to the selected instrument. Figure 20.15 shows the Objective-C–related call tree information collected by the Time Profiler. The top result reveals the method in which TestApp spent most of its time during the profiling session: the -drawRect:contentsOnly: method of the WebFrame class, which is part of the WebKit framework. This makes sense because I used TestApp’s Web window to navigate around a few Web pages for the duration of the trace. As a result, WebKit was busy drawing Web pages. You’ll explore the Time Profiler in more depth later in this chapter. Double-clicking entries in the list can often drill down into further detail. Again, this is instrument specific, so a general description is not possible here.

## The Extended Detail View

The Extended Detail view (Figure 20.16) shows extended information about the selected data in the Detail view. As with the rest of the detail-oriented views, its content is instrument specific. In the figure, the view is displaying extended detail about the selected Time Profiler symbol in Figure 20.15. In this case, it’s appropriate to show the heaviest stack trace (the stack trace responsible for the bulk of the calls to the selected symbol). This view represents the same information as found in the Debug navigator. The slider on the bottom works in the same way as the slider in the Debug navigator as well—it smartly filters out “uninteresting” chunks of the stack trace, depending on its position.

**Figure 20.16** The Extended Detail view

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_351_0.png)

**Figure 20.17** The Target control’s menu

## Launching Instruments

Now that you’re familiar with the main aspects of the Instruments interface, you’re ready to launch it for yourself. There are two ways to do this. You’ll learn the long way first to get a feel for how Instruments attaches to a process, and then you’ll learn the easy way.

### The Long Way

The long way involves launching Instruments yourself from the /Developer/Applications folder. You’ll then choose a template for your document and click Choose. The document is configured and awaits your command. The next step is to choose the process to which you want Instruments to attach. Use the Target control and navigate its menu (Figure 20.17) to find and select the running process of your choice. The final step is to begin the trace by pressing the Record button.

The long way is the only way to attach to processes that are already running or that are running outside Xcode. The most interesting part of that sentence is the implication that you can in fact attach to other processes for a variety of diagnostic reasons. As a power user or system administrator, for example, you can even monitor a process’s file system access—handy for snooping on an installer’s payload as it’s delivered.

### The Easy Way

The easy way (for your Xcode projects) is to choose the Profile action from within Xcode. You’re already familiar with the Run, Test, and Archive actions. You can trigger the Profile action by choosing Product > Profile from the main menu; or by clicking and holding the Run button and then choosing Profile from its menu; or by pressing Command+I. Of course, you must have a project or workspace open and it must build successfully (just as when performing the Run action).

Assuming your project builds successfully, Instruments will launch and prompt you for a template for your new trace document, just as you saw in Figure 20.1. Once you choose your template, Instruments will launch your application, attach to it, and begin recording the trace. You’ll see this in action in the examples in the next section.

Now that you know the Instruments basics, it’s time to apply them to common debugging and profiling tasks. You’ll start by using the Time Profiler to track down a contrived performance problem. You’ll then find a memory leak and track down and kill a zombie invasion.

## Time Profiling

You don’t get very far in a moderate-to-complex application without encountering performance problems. Such problems have traditionally been difficult to track down. More often than not, the cause is entirely different from what you suspected. Instruments’ Time Profiler template has an uncanny ability to show you inefficiencies in your code you may not even have suspected.

To begin, open TestApp’s TestAppAppDelegate.m file and change the -applicationDidFinishLaunching: method so that it includes this line:

```
    [self doSomethingStupid];
```

After the closing curly brace of the -applicationDidFinishLaunching: method, add this new method:

```
- (void)doSomethingStupid
{
    NSMutableArray *array = [NSMutableArray
                             arrayWithCapacity:1000000];
    NSNumber *number;
    for (NSInteger i = 0; i < 10000; i++)
    {
        number = [NSNumber numberWithInteger:i];
        [array addObject:number];
    }
}
```
