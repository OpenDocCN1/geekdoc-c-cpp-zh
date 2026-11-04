# Intermezzo on Historical Debugging with IntelliTrace

While we're in the wonderful world of debugging managed code applications, we should take a look at a new feature added to Visual Studio 2010: IntelliTrace. In the example shown in the previous section, we were dealing with an exception that was swallowed inappropriately long before the program started to fail. Wouldn't it be handy to walk the program's execution back in time to investigate the program state outside the scope of the current call stack? That's exactly what IntelliTrace enables.

To play with this exciting new feature, we need to configure it first through the Tools, Options dialog, under the IntelliTrace node in the tree view. Two modes are available; the latter one, called Diagnostic Events and Call Information, is the most powerful. Figure 23.10 shows the desired settings for the next experiment.

![](bbox=[0.059, 0.344, 0.745, 0.625])

FIGURE 23.10  Configuring the new IntelliTrace feature.

Disabling first-chance exceptions for the time being, we'll execute the same program with the Historical Debugging feature properly configured. At the point we crash on the NullReference exception, make the IntelliTrace window visible (if it isn't already) through the Debug, IntelliTrace, Debug History Calls menu. This brings up the view shown in Figure 23.11.

Observe a few things here. At this point, IntelliTrace pretty much shows the same information you would see in the Call Stack window: The debugger was stopped at an exception in method A, with the Main method higher up the stack. However, from this view, we can start doing time travel. Using the buttons in the margin of the code editor, it's possible to go back to the previous event logged by the historical debugger. So far, nothing too exciting; this will just bring us back to the Main method's call to A.

Where the magic comes is when we're back on the call to B from the Main method; now we can step into B based on the IntelliTrace information that has been collected. Not only this, but the technology enables us to debug the call to B by replaying the events