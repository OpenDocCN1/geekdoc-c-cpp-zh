This line connects the handler (end_program) to the signal called clicked, which is emitted by a button widget when the mouse is clicked on it. We use the GTK_CALLBACK function to make sure the compiler knows that the end_program function is a valid callback

Signals are used a lot in GTK, all widgets generate signals under various circumstances - mostly interacted with by the user, but also when certain system events occur. Each type of widget has a set of signals it can generate, the g_signal_connect function is used to 'connect' a handler function to them, meaning it will be called when the signal is generated

Handling signals is one of the most important jobs of the main loop which runs inside gtk_main - if a signal is generated, code in the main loop checks to see if there is a handler associated with that signal, and calls the handler if

By building and running the new code. Now we have a button on the window as before, but when we click the button, the window closes and, importantly, the program exits as well. This still isn't perfect, though - if we click the X at the top right, the window closes but the program doesn't exit. Let's fix that.

The way we do this is to connect another handler to the signal generated when that X is clicked. The name of this signal is delete_event and it is generated from the window widget. So we need to connect the same handler to that event as well:

```
g_signal_connect(win, , G_CALLBACK(end_program), NULL);
```

Note that we connect to win rather than to btn this time - the delete_event signal is created by the widget rather than the button. Now if the window is closed by clicking the X, the delete_event signal causes the end_program handler to be called and the main loop then exits.

We've got now a GTK application that opens and closes cleanly, but it still doesn't do anything. So in the next chapter, we'll make it do something useful.