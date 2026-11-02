you see message dialogs. Note that a message dialog is used only when the app is in the foreground. Toast notifications, as we'll see in Chapter 16, "Alive with Activity," typically apply only to background apps.

![](bbox=[0.193, 0.154, 0.803, 0.238])

+   - Finally, other errors that don't require user action can be displayed either inline (on the app canvas) or through flyouts. See Laying out your UI errors for full details; we'll see some examples later on as well.

Where the app bar (on the bottom) is concerned, it's also important to organize your commands into sets, as this streamlines implementation as we'll see in the next section. For full guidance I recommend Guidelines and checklist for app bars and Commanding Design in the documentation, which provide many specifics on placement, spacing, and grouping. That guidance can be summarized as follows:

+   - First, make two groups of commands: one with those commands that appear throughout the entire app, regardless of context, and another with those that show only on certain pages. The app bar control is fairly simple to reconfigure at run time for different groups.
+   - Next, create command sets, such as those that are functionally related, those that toggle view types, and those that apply to selections. Remember that an app bar command can display a popup menu, as shown below, to provide a list of options and/or additional controls, including longer labels, drop-down lists, checkboxes, radiobuttons, and toggle switches. In this way you can combine closely related commands into a single one that gets more room to play than its little space on the app bar proper.

![](bbox=[0.184, 0.618, 0.447, 0.79])

+   - For placement, put persistent commands on the right side of the app bar and the most common context-specific commands on the left. After that, begin to populate toward the middle. This recommendation comes from the ergonomic realities of human hands: fingers and thumbs—even on the largest hands of basketball players!—grow only so long and can reach only so far on the screen without having to move one's hand. The most commonly used