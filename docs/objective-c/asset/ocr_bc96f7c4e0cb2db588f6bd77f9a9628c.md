```
selector:@selector(stuffChanged:)
name:MY_FANCY_NOTIFICATION
object:nil];
}
```

When adding your object as an observer, you must provide a selector which will be called when the notification is received. In this case, the selector being specified is the -stuffChanged: method. This method must be specified to take a single parameter. When it is called the parameter that is passed will be an instance of NSNotification. This object contains information about the notification, what object posted the notification, and the userInfo object that was specified by that object when the notification was posted. Listing 17.11 shows the implementation of the -stuffChanged: method.

# Listing 17.11

# Implementation of the -stuffChanged: method

```
-(void)stuffChanged:(NSNotification *)inNotification;
{
    Bar *bar = (Bar *)[inNotification object];
    [bar askSomeQuestion];

    NSString *someData = [[inNotification userInfo] objectForKey:@"somedata"];
    [self doSomething];
}
```

Finally, an important part of being an observer is making sure that you remember to remove yourself as an observer when you are being deallocated. Failure to do so may cause an error, because you're object is no longer valid but it is still referenced in the NSNotificationCenter. To remove yourself as an observer from NSNotificationCenter, you call the object method -removeObserver:.

Listing 17.12 shows an implementation of a dealloc method where the object is removing itself as an observer from the NSNotificationCenter.

# NOTE

You need only call this method once for any given observer. Even if you are observing multiple notifications that may be received from multiple different observable objects, using this call to remove yourself as an observer will remove you as an observer completely for all notifications.