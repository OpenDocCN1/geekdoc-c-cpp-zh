
Changes to an NSDictionary because it is immutable. Instead, you have to use the NSMutableDictionary. This is the subclass of NSDictionary that allows such changes.

By now you have probably found it frustrating that the Apple documentation for a class doesn’t at least list all of the methods that are available for objects of a particular type. The documentation contains in-depth descriptions of methods defined for that class but doesn’t show you the methods that are inherited from superclasses. You have to follow the documentation up the tree to find that a particular method is defined several levels up (often in a class you would never have thought to look at).⁴

This general inconvenience can sometimes be a benefit. For example, if you look at the documentation for NSMutableDictionary, you can quickly see how it differs from NSDictionary. Only the additional methods are listed. There are methods for creating a mutable dictionary that allow you to specify the initial capacity of the dictionary.⁵ There are additional methods for adding entries to and removing entries from a mutable dictionary. In every other way, an NSMutableDictionary is just an NSDictionary, so all of those methods in the superclass are available to us in the NSMutableDictionary as well.

So, let’s play with the NSMutableDictionary a bit. First declare an instance variable named runningApps in CurrentApp.h.

Download Dictionaries/HelloApplication16/CurrentApp.h

```objc
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface CurrentApp : NSObject {
    NSObject <ActivityMonitorDelegate> *delegate;
    NSString *name;
    NSDictionary *delegateMethods;
    NSMutableDictionary *runningApps;
}
@property IBOutlet NSObject <ActivityMonitorDelegate> *delegate;
@property(copy) NSString *name;
@end
```

4. You can always press Escape after typing the name of your target and a space to see all of the methods available to you. Use this in conjunction with Quick Help to quickly understand what each method does.

5. As the dictionary grows, more memory will be allocated to it as needed.

We create our mutable dictionary in the init method. Use the setObject:forKey: method to add a new entry to the dictionary that has the application’s name as a key and a time stamp as its value whenever an application is launched.⁶

```objc
[runningApps setObject:[NSDate date] forKey:appName];
```

In place of appName, we’ll need to retrieve the name of the application from the userInfo dictionary for our notification. Similarly, we’ll use the removeObjectForKey: method whenever an application is terminated to remove the entry with the key equal to the name of the application that is terminated.

```objc
[runningApps removeObjectForKey: appName];
```

Let’s add logging to display the value of the runningApps variable at the end of the respondToChange: method. When I run the application and start up iCal, I see this in my Console window:

```text
HelloApplication = "2009-10-03 10:45:36 -0400";
iCal = "2009-10-03 10:45:39 -0400";
```

For completeness, here is CurrentApp.m:

Download Dictionaries/HelloApplication16/CurrentApp.m

```objc
#import "CurrentApp.h"

@implementation CurrentApp

@synthesize delegate, name;

-(void) respondToChange: (NSNotification *) notification {
    SEL methodName = NSSelectorFromString([delegateMethods objectForKey:[notification name]]);
    if ([self.delegate respondsToSelector:methodName]) {
        self.name = [notification.userInfo objectForKey:@"NSApplicationName"];
        [self.delegate performSelector:methodName withObject:self];
    }
    NSLog(@"%@", runningApps);
}
-(void) applicationDidLaunch: (NSNotification *) notification {
    [runningApps setObject:[NSDate date]
                     forKey:[notification.userInfo
                             objectForKey:@"NSApplicationName"]];
    [self respondToChange:notification];
}
-(void) applicationDidTerminate: (NSNotification *) notification {
    [runningApps removeObjectForKey:[notification.userInfo
                                      objectForKey:@"NSApplicationName"]];
    [self respondToChange:notification];
}
-(void) setUpNotification:(NSString *)notification withSelector:(SEL)methodName {
    [[[NSWorkspace sharedWorkspace] notificationCenter]
             addObserver:self
                selector:methodName
                    name:notification
                  object:nil];
}
-(void) registerNotifications {
    [self setUpNotification:NSWorkspaceDidLaunchApplicationNotification
             withSelector:@selector(applicationDidLaunch:)];
    [self setUpNotification:NSWorkspaceDidTerminateApplicationNotification
             withSelector:@selector(applicationDidTerminate:)];
}
-(void) initializeMethodDictionary {
    delegateMethods = [[NSDictionary alloc] initWithObjectsAndKeys:
                       @"applicationDidLaunch:",
                       NSWorkspaceDidLaunchApplicationNotification,
                       @"applicationDidTerminate:",
                       NSWorkspaceDidTerminateApplicationNotification,
                       nil];
}
-(id) init {
    if (self = [super init]) {
        [self registerNotifications];
        [self initializeMethodDictionary];
        runningApps = [[NSMutableDictionary alloc] initWithCapacity:5];
    }
    return self;
}
@end
```

6. There’s no real reason for doing this other than to show that we can add and remove entries to/from our dictionary.

Before moving on, remove all of the lines that I highlighted in the previous code listings of the header and implementation files for CurrentApp. They don’t do any harm, but they clutter up the example a bit, and now that you know how to create and work with a mutable dictionary, we don’t need to keep them around.

### 13.8 Exercise: Adding an Icon

Now that we’ve tidied up our code, let’s use the userInfo dictionary to add another feature to HelloApplication. Let’s display the icon of the application being launched or terminated.

So, for example, when we quit iCal, our display should look something like this:

![](img/9355405953264484a02198b0e3d25b7e_221_0.png)

We can accomplish this change by adding an outlet to the ActivityController header file, and by reshaping our code. As is often the case with Cocoa programming, it can take a while to figure out how to accomplish this third step. Let’s take care of the easier steps first.

In Xcode, add an outlet named imageView to the header file ActivityController.h. The outlet should be a pointer to an NSImageView.

In Interface Builder, find an NSImageView described as an *image well* in the Library, and drag it into your window. Adjust the window, text field, and image well so that they look like the picture you saw at the beginning of this section.

Adjust the size settings so that the user can adjust the size of the window only in the horizontal direction. When the window grows, the image well should stay where it is, and the text field should grow so that it remains the same distance from the left and right sides.

Before leaving Interface Builder, connect the imageView outlet you created in your header file to the image well. Save your work.

We’ll take advantage of a new class that was added in Snow Leopard. NSRunningApplication lets you send messages and get information about a currently running user application. Look back at the last entry we saw when we displayed the userInfo dictionary in the Console window:

```text
NSWorkspaceApplicationKey = "<NSRunningApplication:
    0x200019ae0 (com.apple.iCal - 7130)>";
```

The NSRunningApplication has the following properties:

- activationPolicy
- active
- bundleIdentifier
- bundleURL
- executableArchitecture
- executableURL
- finishedLaunching
- hidden
- icon
- launchDate
- localizedName
- processIdentifier
- terminated

All the information that is contained in the rest of the userInfo dictionary and more is contained in the instance of the NSRunningApplication with the key NSWorkspaceApplicationKey.

Because you are developing in Snow Leopard, you can restructure your application to use NSRunningApplication wherever possible. Instead of retrieving and storing the application name from the userInfo dictionary, we can retrieve and store the running application. And instead of passing an instance of CurrentApp to our delegate methods, we can pass the running application and use it to display the name and the icon.⁷

Take a few minutes to try to get this to work before moving on to read a solution.

### 13.9 Solution: Adding an Icon

Your header file should look like this:

Download Dictionaries/HelloApplication17/ActivityController.h

```objc
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface ActivityController : NSObject <ActivityMonitorDelegate> {
    NSTextField *activityDisplay;
    NSImageView *imageView;
}
@property IBOutlet NSTextField *activityDisplay;
@property IBOutlet NSImageView *imageView;
@end
```

In Interface Builder, you should have had no problem adding your image well and using the blue guidelines to arrange the image well and text field inside the window. You should have used the Size inspector to set the minimum and maximum size of the window. If the height is the same for the minimum and maximum sizes, your end user can adjust

7. There was no need for this overhead when we just needed the name of the application. Now it makes sense to use the NSRunningApplication instance we retrieve from the userInfo dictionary.
