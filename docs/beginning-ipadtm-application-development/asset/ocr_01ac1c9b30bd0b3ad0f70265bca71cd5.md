6. In the ApplePushNotificationAppDelegate.m file, type the following bold code:

```
```objc
#import "ApplePushNotificationAppDelegate.h"

#import "ApplePushNotificationViewController.h"

@implementation ApplePushNotificationAppDelegate

@synthesize window;
@synthesize viewController;

- (void)applicationDidFinishLaunching:(UIApplication *)application {
    [window addSubview:viewController.view];
    [window makeKeyAndVisible];

    NSLog(@"Registering for push notifications...");
    [[UIApplication sharedApplication]
    registerForRemoteNotificationTypes:
    (UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge |
     UIRemoteNotificationTypeSound)];
}

- (void)application:(UIApplication *)app
didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {

    NSString *str = [NSString
    stringWithFormat:@"Device Token=%@",deviceToken];
    NSLog(str);
}

- (void)application:(UIApplication *)app
didFailToRegisterForRemoteNotificationsWithError:(NSError *)err {

    NSString *str = [NSString stringWithFormat: @"Error: %@", err];
    NSLog(str);
}

- (void)application:(UIApplication *)application
didReceiveRemoteNotification:(NSDictionary *)userInfo {

    for (id key in userInfo) {
        NSLog(@"key: %@, value: %@", key, [userInfo objectForKey:key]);
    }
}

- (void)dealloc {
    [viewController release];
    [window release];
    [super dealloc];
}

@end
```
```

7. Press Command-R to test the application on a real device. Press Shift-Command-R in Xcode to display the Debugger Console window. Carefully observe the device token that is printed. The device token is of the format: xxxxxxxx xxxxxxxx xxxxxxxx xx xxxx xxxxxxxx xxxxxxxx xxxxxxxx