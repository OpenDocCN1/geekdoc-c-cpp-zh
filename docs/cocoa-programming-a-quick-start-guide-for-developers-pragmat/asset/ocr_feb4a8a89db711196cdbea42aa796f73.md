First we obtain our application’s notification center with this call:

```
```objc
[NSNotificationCenter defaultCenter]
```
```

Note that this is a different call than when we were getting a handle to the notification center for our workspace. Once we have the notification center, we post notifications using postNotificationName:object:. All that remains is for us to register for and respond to these notifications.

# 11.9  Exercise: Receiving the Custom Notifications

Register observers in the ActivityController for the notifications we created in the previous section. Implement methods applicationDidLaunch: and applicationDidTerminate: in ActivityController that print “Launched.” or “Terminated.” in the text field when the appropriate notification is received.

# 11.10  Solution: Receiving the Custom Notifications

You know how to do every step in this exercise; now let’s put it all together. Add the registerNotifications and setUpNotificationsWithSelector: methods that we used in CurrentApp. Call registerNotifications from awakeFromNib.

When you receive a notification, you need to change the activeDisplay’s string value to either “Launched.” or “Terminated.”

```
```objc
// Download Notification/HelloApplication6/ActivityController.m
#import "ActivityController.h"
#import "CurrentApp.h"

@implementation ActivityController

@synthesize currentApp, activityDisplay;

-(void) applicationDidLaunch: (NSNotification *) notification {
    [self.activityDisplay setStringValue:@"Launched."];
}
-(void) applicationDidTerminate: (NSNotification *) notification {
    [self.activityDisplay setStringValue:@"Terminated."];
}
-(void)setUpNotification: (NSString *)notification withSelector:(SEL)methodName {
    [[NSNotificationCenter defaultCenter]
        addObserver:self
        selector:methodName
        name:notification
        object:nil];
}
```
```