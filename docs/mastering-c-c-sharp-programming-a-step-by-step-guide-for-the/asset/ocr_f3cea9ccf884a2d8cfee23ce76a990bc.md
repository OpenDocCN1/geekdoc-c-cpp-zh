Remember, the C# events are based on the C# delegates so the method we use must match the requirements of our delegate – EventHandler. This delegate requires a return type of void and it requires two parameters (a sender object, which is what triggered the event, and the EventArgs object, which contains information about the event that we are raising – this won’t have a lot of information in it for this particular situation, but in other events, that could change).

Somewhere in your code (continue to use the Main method for now), create your method that will handle that event. Something like this:

```
public void HandlePointChanged(object sender, EventArgs eventArgs)
{
    // When the pointer changes, something intelligent should be done; maybe draw the GUI again,
    // or update a different data structure or anything you can think of, really.
}
```

Attaching event handlers to an event is really quite easy to do and, again, the code below can go wherever it needs to go:

```
Point point = new Point();

// This is the most important bit:
point.PointChanged += HandlePointChanged;

// Now, if the point is changed, the event called PointChanged is raised,
// and HandlePointChanged is called.
point.X = 3;
```