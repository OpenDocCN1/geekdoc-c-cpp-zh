So, let’s remove the instance variables backing our properties. First, let’s check your project settings. Open them from the menu bar with Project > Edit Project Settings. Choose the Build tab, set the Architectures setting to 64-bit Intel, and select the checkbox to build the active architecture only.

![](bbox=[0.136, 0.186, 0.776, 0.4])

Now you can remove the instance variables from the header file:

[Download Properties/HelloWorld/Greeter.h](download)

```
```objc
#import <Cocoa/Cocoa.h>

@interface Greeter : NSObject {
}
-(NSString *) greeting;
-(id) initWithName:(NSString *)name;
@property(copy) NSString *name;
@property(assign, readonly) NSInteger age;
@property(retain) Greeter *buddy;
@property(assign, getter=isUpperCase) BOOL upperCase;

@end
```
```

Click Build & Run, and the application should run exactly as before. If you get warnings after removing the instance variables, then check that you are running under 64-bit and that your project settings are correct.

You can remove the instance variables that back properties if you are developing for the iPhone,⁶ but not if you are developing on or for the 32-bit Mac OS X runtime.

6. At the time of this writing, you can remove the variables when targeting the iPhone, and your code will work on the device. The removal of variables is not yet supported on the simulator.