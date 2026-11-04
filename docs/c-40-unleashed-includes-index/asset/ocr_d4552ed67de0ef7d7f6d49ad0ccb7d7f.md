multicast delegate. The code that gets generated for our Finished event looks roughly like this:

```
private Action _finished;

public void add_Finished(Action value) {
    _finished = (Action)Delegate.Combine(_finished, value);
}

public void remove_Finished(Action value) {
    _finished = (Action)Delegate.Remove(_finished, value);
}
```

# MULTITHREADING IS SUBTLE

The word roughly in the previous paragraph is all important. In harsh reality, the generated code is slightly more complicated due to multithreading concerns. If multiple threads are adding or removing event handlers simultaneously, the door is wide open for problems.

To understand why this is the case, see how the call to Combine is followed by an assignment (similar for the Remove call). When a thread switch occurs between the call to Combine and the assignment, it's possible another thread messes with the multicast delegate, too. After switching back to the original thread and doing the assignment, the effects from the interrupting thread are overwritten: A race condition exists.

As a user of the language, you don't have to worry about this, but it's good to know this protection is in place.

# Raising Events, the Correct Way

In our CountDown example, you've seen how to raise events using this pattern:

```
if (MyEvent != null)
    MyEvent(/* args */);
```

Looks right, doesn't it? If nobody is listening for the event, MyEvent is null, and we should not attempt to invoke the delegate because that will cause the runtime to yell at us with an unfriendly NullReferenceException.

# WHY IS NULL USED ANYWAY?

It might be surprising that the empty event handlers are being presented with null references. This is really due to the way the Combine and Remove methods on Delegate are implemented, but that just pushes the question further out: Why not just return a MulticastDelegate with an empty invocation list?