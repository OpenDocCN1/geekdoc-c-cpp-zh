# Note

This calculator is designed to perform just a single operation between two fractions. It's left as an exercise at the end of this chapter for you to remove this limitation.

![](bbox=[0.363, 0.196, 0.616, 0.549])

Figure 21.17 Fraction calculator after launch.

The display is continuously updated as keys are pressed. Figure 21.18 shows the display after the fraction 4/6 has been entered and the multiplication key has been pressed.
Figure 21.19 shows the result of multiplying the fractions 4/6 and 2/8 together.You'll note that the result of 1/6 indicates that the fraction itself has been reduced.

# Starting the New Fraction_Calculator Project

The first iPhone program started from aWindows-based project template. Here you will (minimal) UI work directly in the application controller (the AppDelegate class).This is not the recommended approach for developing UI-rich applications. The AppDelegate class typically handles changes related to the state of the application itself, such as when the application finishes launching or when it is to be deactivated.

The view controller (implemented with the ViewController class) is where you should perform your actions related to the UI. This might be displaying text, reacting to the pressing of a button, or putting an entirely new view on the iPhone's screen.