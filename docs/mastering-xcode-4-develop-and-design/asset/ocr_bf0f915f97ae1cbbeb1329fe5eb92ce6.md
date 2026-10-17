![](bbox=[0.13, 0.172, 0.607, 0.371])

FIGURE 20.19 Source code overlaid with a heat map

Many developers’ knee-jerk reaction would be to blame the tight for loop. Of course it’s going to take a while to create ten thousand objects. Astute Cocoa / Objective-C developers will know better with such a contrived example, but here’s where the Time Profiler really shines. Double-click the -[TestAppAppDelegate doSomethingStupid] symbol in the list, and the Detail view will prove its name (Figure 20.19).

In the figure, TestAppAppDelegate.m is displayed with some additional information overlaid. Instruments has broken down the time spent in that symbol (the -doSomethingStupid method) to highlight the most time-consuming instructions within it.

To see the percentages (as in Figure 20.19), you may need to click the gear button in the upper-right corner and select View as Percentage from the menu. The overlay is color-coded to serve as a sort of heat map, where the color (ranging from “red hot” to “not-so-hot yellow” and beyond) represents how much time your computer spent executing the most time-consuming instructions.

This makes one thing very obvious: The culprit isn’t the for loop, though it certainly takes time. The red-hot instruction (89.5 percent of the method’s time in the example above) was the line where you allocated and initialized an NSMutableArray. If you don’t already know why this is, here’s where Instruments gets even better.

Click the Call Tree segment of the Detail view’s navigation bar to get back to the list of symbols. Deselect the Hide System Libraries check box to show all the system library calls in addition to those of TestApp. TestApp’s symbols should be gone, replaced by some system library symbols. Because the call tree is inverted, the deepest call in the stack is shown as top-level objects, and the top results are the calls that happened as a result of -doSomethingStupid.