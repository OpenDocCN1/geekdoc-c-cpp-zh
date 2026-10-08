![](bbox=[0.24, 0.13, 0.81, 0.49])

![](bbox=[0.14, 0.35, 0.23, 0.49])

# # Making Progress at the Bar

Anyone who has ever used a computer knows that some functions — such as creating a large movie in iMovie or ripping a bunch of MP3 files in iTunes — require a long time to process. As lengthy operations proceed, the thoughtful programmer displays some sort of feedback to let the user know that the computer is working on something. To do this in Cocoa, use the `NSIndicator` control. To add an `NSIndicator` control to your project, search for **Indicator** in the Library window of Interface Builder and then drag one to your interface.

`NSIndicator` can display two kinds of progress bars:

> **Indeterminate:** Display an indeterminate progress indicator when you don’t know how long the process will take, such as when you’re searching for files on a hard drive. The indeterminate progress indicator has two different looks — one variety looks like a barber pole and the other spins.

> **Determiniate:** Use determiniate progress indicators when you know how long a process takes to complete, such as when you repeat a task ten times.