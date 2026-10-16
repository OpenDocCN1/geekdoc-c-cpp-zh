# Listing 17.12

# Removing yourself as an observer.

```
@implementation Foo

-(void)dealloc;
{
    [[NSNotificationCenter defaultCenter] removeObserver:self];
    [super dealloc];
}

@end
```

# Discussion

The NSNotificationCenter provides the implementation of the Observer pattern in Objective-C. It enables objects to post notifications about changes in their state and then allows any objects which wish to be notified of those changes to observe for those notifications. The NSNotificationCenter allows multiple objects to observe notifications and also allows multiple objects to post a given notification. In this way, it provides a many to many relationship between observers and notifiers. One question that you might be asking would be when to use NSNotificationCenter versus the delegate pattern. Firstly, you should use the NSNotificationCenter whenever there might be multiple parties interested in the information that you are sending the notification about. The delegate pattern really only works in a one-to-one relationship. You may be connected to implement an array of delegates when working with the delegate pattern to overcome this limitation. Instead of doing this, you should consider using the NSNotificationCenter.

Another case where the NSNotificationCenter makes a bit more sense than using a delegate is in cases where the Observer and the observed object are far away from each other in your code. In other words, if the observer and the thing that you want to observe are in totally different subsystems, and getting references from one side of your application to the other presents challenges, the NSNotificationCenter, being a global singleton, provides a convenient interface between those two objects. There are some limitations when working with the NSNotificationCenter, specifically, it's really only designed for passing around simple data. It does not allow for the complex definition of delegate protocols and so on which make working with delegates so convenient. You are limited, as far as the data passed during the notification process to the object and the userInfo dictionary. This doesn't mean that it is impossible to send complex data, simply that it is not as convenient as the delegate protocol is.