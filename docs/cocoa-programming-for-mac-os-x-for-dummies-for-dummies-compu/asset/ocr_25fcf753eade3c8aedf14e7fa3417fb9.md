# Check box

![](bbox=[0.24, 0.14, 0.46, 0.24])

Figure 9-6: The button's image is centered vertically now.

![](bbox=[0.49, 0.14, 0.7, 0.47])

So far, you’ve looked at buttons that users click to perform an action. Not all buttons have to trigger an action, though. The check box button, for example, can behave more passively. Rather than firing some action, a check box button might simply indicate a binary state, such as toggling a feature on and off or for answering a Yes/No question. A check box can act like a button, however, in that it’s also capable of triggering an action just like a push button. Figure 9-7 shows a check box control.

You can add a check box to your interface by dragging one from the Library window in Interface Builder. In the Inspector window, you can set the default state of the check box as well as its title and other cosmetic features.

When using check box controls, your code typically checks the state of the control and performs an appropriate operation. To demonstrate, this snippet of code checks the state of a check box control outlet, $\mathit{prefsCheckbox}$, and acts accordingly:

```
```CPP
if ( (prefsCheckbox .state))
// Save Preferences
else
// Don't Save Preferences
```
```