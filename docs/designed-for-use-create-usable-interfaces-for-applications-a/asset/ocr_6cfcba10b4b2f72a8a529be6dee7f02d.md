# 20.2 Unexpected Modes

Dialog boxes are a specific type of mode. Unlike nonobvious modes, dialog boxes are usually reasonably obvious, at least when they first pop up. They are, however, often unexpected, therefore causing the same problems as nonobvious modes: the user interface doesn’t do what the user wants because it is not in the mode the user expects.

![](bbox=[0.25, 0.22, 0.38, 0.31])

THE USER EXPECTS TYPED TEXT TO APPEAR IN HIS DOCUMENT

![](bbox=[0.5, 0.22, 0.65, 0.31])

BUT THE UNEXPECTED DIALOG BOX "EATS" TYPED TEXT

Not only do dialog boxes change the mode of the user interface unexpectedly, but it’s also possible that the user’s input is mistakenly interpreted as input for the modal dialog box, rather than for the previously active window. (This is called stealing focus, since it moves the computer’s focus from where the user wants it to be to somewhere else.) This means that the user may accidentally discard a modal window or approve something she intended to reject. Instead of moving the cursor to a new line, the Return key may unmount a network disk or delete a file, because that was the default button’s action in the modal window.

# 20.3 Sticky Modes

This is my alarm clock. To change the time the when the alarm goes off, I have to push the topmost button. This puts the clock into its “change alarm time” mode. In that mode, the topmost button now changes the hour of the alarm. So, if I can’t push this button again to exit the mode, how do I exit the mode?

![](bbox=[0.52, 0.62, 0.78, 0.84])

It is often not obvious to the user how to resolve an active mode, and this causes usability problems. Another example of this is the Insert