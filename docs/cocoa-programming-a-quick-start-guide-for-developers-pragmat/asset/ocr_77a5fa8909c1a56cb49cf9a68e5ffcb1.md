to listing required methods. In this code snippet, aRequiredMethod and anotherRequiredMethod are required, while anOptionalMethod is optional.

```
```objective-c
@protocol SomeProtocol

-(void) aRequiredMethod;

@optional
-(void) anOptionalMethod;

@required
-(void) anotherRequiredMethod;

@end
```
```

Let’s create a protocol that we’ll use to define our delegate. First create a new header file in Xcode. Select the Classes folder in Groups & Files. Create a new file, and choose the template Mac OS X > Cocoa Class > Objective-C protocol. Name the file ActivityMonitorDelegate.h, and save it.

The first line of the file is @protocol followed by the name of the protocol, which is the same as the name of the file.⁴ Protocols are lists of method declarations. There are no imports, no classes, and no instance variables, so we don’t need any curly braces. Here we declare applicationDidLaunch: and applicationDidTerminate: in our protocol. Notice that these methods take a parameter of type CurrentApp.

```
`Download Protocols/HelloApplication7/ActivityMonitorDelegate.h`
```

```
```objective-c
@class CurrentApp;

@protocol ActivityMonitorDelegate

@optional
-(void)applicationDidLaunch: (CurrentApp *) app;
-(void)applicationDidTerminate: (CurrentApp *) app;

@end
```
```

Now let’s use this protocol in the ActivityController class. You’ll need to add an import statement to the top of ActivityController.h. You’ll also have to add the declaration that ActivityController conforms to the protocol by adding ActivityMonitorDelegate in angle brackets after the name of ActivityController’s superclass NSObject.

⁴. The protocol and filename could have different name, but by convention they are the same.