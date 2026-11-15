```
userState));
return continueTask.Result;
}, scheduler);
}

public event
EventHandler<CalculateCompletedEventArgs>
CalculateCompleted = delegate { };

public class CalculateCompletedEventArgs
: AsyncCompletedEventArgs
{
public CalculateCompletedEventArgs(
string value,
Exception error,
bool cancelled,
object userState) : base(
error, cancelled, userState)
{
Result = value;
}
public string Result { get; private set; }
}
```

In Listing 19.20, this support is provided via the CalculateCompleted
event. Registering for this event will allow the caller to receive a notifica-
tion when the calculation completes. The value of the calculation will be on
the Result property of the CalculateCompletedEventArgs class (which
derives from AsyncCompletedEventArgs). This same class will allow the
caller to check for an error (via the Error property), cancellation (via the
Canceled property), and user state (via the UserState property).

In the past, cancellation support was available in EAP through the
addition of a CancelAsync method, which optionally took an object
objectState parameter. However, with .NET Framework 4, using a Can-
cellationToken would be the preferred approach since it would avoid the
need to save the state.

Frequently with multithreaded operations, not only do you want to be
notified when the thread completes, but you also want the method to pro-
vide an update on the status of the operation. EAP includes support for