of the pattern, therefore, is to *humiliate* that code by making it too simple to bother testing. We saw a simple example of this earlier, in the “Testing GUIs” section, but now let’s take a deeper look.

The general strategy is shown in Figure 4.6. The code that communicates across the boundary is separated into two elements: the presenter and the *Humble Object* (denoted here as the `HumbleView`). The communication between the two is a data structure named the `Presentation`.

![](bbox=[0.2, 0.31, 0.82, 0.59])

Let’s assume that our application (not shown) wants to display something on the screen. It sends the appropriate data to the presenter. The presenter then unpacks that data into the simplest possible form and loads it into the `Presentation`. The goal of this unpacking is to eliminate all but the simplest processing steps from the `HumbleView`. The job of the `HumbleView` is simply to transport the unpacked data in the `Presentation` across the boundary.

To make this concrete, let’s say that the application wants to put up a dialog box that has Post and Cancel buttons, a selection menu of order IDs, and a grid of dates and currency items. The data that the application sends to the