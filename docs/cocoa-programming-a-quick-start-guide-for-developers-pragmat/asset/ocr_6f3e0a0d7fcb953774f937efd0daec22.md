To see this work, you’ll have to add a call to this method from applicationDidFinishLaunching: like in the highlighted line here:

```
```objc
Download Properties/HelloWorld13/HelloWorldAppDelegate.m
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    Greeter *greeter = [self greeterFor:@"Maggie"];
    NSLog(@"Greeter: %@", greeter);
    NSTextField *label = [self labelWithText:[greeter greeting]];
    [self setUpperCasedName:greeter];
    [[self.window contentView] addSubview:label];
}
```
```

Click Build & Run, and you’ll see output like this:

```
```
The name was originally Maggie.
The name is now MAGGIE.
```
```

Now let’s introduce properties and start reducing and simplifying our code.

# ## 5.4 Converting the Accessors to Properties

Let’s take stock of where we are. We’ve exposed an attribute of the Greeter class named name that we can get and set. We’ve done this in three steps:

+   1. Declared an instance variable name in the header file.
+   2. Declared a getter and a setter named name and setName: in the header file.
+   3. Provided mostly boilerplate code to implement the methods in the implementation file.

Now we’ll use Objective-C 2.0 properties to make changes to these last two steps and in some cases eliminate the first step.

Replace the declarations of the getter and the setter with this:

```
```objc
Download Properties/HelloWorld14/Greeter.h
#import <Cocoa/Cocoa.h>

@interface Greeter : NSObject {
    NSString *name;
}
-(NSString *) greeting;
-(id)initWithName:(NSString *)name;
@property(copy) NSString *name;

@end
```
```