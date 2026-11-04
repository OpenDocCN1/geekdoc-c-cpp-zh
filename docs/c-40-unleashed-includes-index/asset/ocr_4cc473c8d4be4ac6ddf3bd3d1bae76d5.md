![](bbox=[0.11, 0.1, 0.86, 0.42])

FIGURE 18.16 Auto-completion for generating and adding an event handler.

Okay, so the use of the sender parameter seems useful, so what about the EventArgs parameter? In the running example from Windows Forms, we’ve seen three different EventArgs types, as shown in Figure 18.17.

![](bbox=[0.1, 0.64, 0.75, 0.87])

FIGURE 18.17 EventArgs form a class hierarchy.

As the name implies, EventArg types represent an event's arguments, which contain useful information about the event that was raised.

Notice some exposed properties are not just get-only, such as the KeyEventArgs's Handled property. This allows a handler to communicate back to the event source about further action to be taken. In case of keyboard input, this makes sense because key input is usually to be processed by only a single entity in the system.

Besides the event's data provider role played by EventArgs subtypes, there's another key aspect to them: The class hierarchy formed by EventArgs types yields some