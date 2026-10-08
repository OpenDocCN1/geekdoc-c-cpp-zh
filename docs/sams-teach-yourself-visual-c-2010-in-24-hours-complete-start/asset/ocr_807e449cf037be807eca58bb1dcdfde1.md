# # By the Way

# ## Raising an Event When Using Event “Properties”

If you use the property-like syntax, the method used to actually raise the event needs to be a bit different to retrieve the event handler from the handler list, as shown here:

```
```
protected virtual void OnAddressChanged(AddressChangedEventArgs e)
{
    var handler = events[addressChangedEventKey] as EventHandler<AddressChangedEventArgs>;
    if (handler != null)
    {
        handler(this, e);
    }
}
```
```

By convention, the name of the event raiser method starts with “On” followed by the name of the event. For non-static events on unsealed classes, this method should be declared as a **protected virtual** method. For static events, non-static events on sealed classes, or events on structs, the method should be public. This method should always have a void return type and take a single parameter, named *e*, which should be typed to the appropriate EventArg s class.

The content of this method also follows a standard pattern, which makes a temporary copy of the event (line 9) to avoid the possibility of a race condition occurring if the last subscriber unsubscribes immediately after the null check (line 10) and before the event is raised (line 12).

GO TO ▶ Hour 23, “Understanding Threads, Concurrency, and Parallelism,” for more information on race conditions.

# # Watch Out!

# ## Multithreading and Events

This pattern only prevents one possible type of race condition, whereby the event becomes null after the check and is only relevant if the code is multithreaded. There are complexities that must be safeguarded against when writing multi-threaded events, such as ensuring that any necessary state is still present in a thread-safe manner before executing code that relies on that state.

# ## Try It Yourself

# ### Publishing and Raising Events

By following these steps, you will explore how to publish and raise events.

+   1. Open the **Hour6** solution in Visual Studio.
2. Add a class named AddressChangedEventArgs to the **PublishAndRaise** project. This class should follow the same pattern as shown in Listing 6.2.