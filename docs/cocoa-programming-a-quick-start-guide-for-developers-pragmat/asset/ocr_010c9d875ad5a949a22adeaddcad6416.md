Click Build & Run, and you should see a more personal greeting.

# 4.12  Solution: Other Initializations

Add this declaration to the Greeter header file as we are adding a new initialization method to the public interface:

```
Download `Classes/HelloWorld11/Greeter.h`

```objective-c
#import <Cocoa/Cocoa.h>

@interface Greeter : NSObject {
    NSString * name;
}
-(NSString *) greeting;
-(id) initWithName:(NSString *)newName;
@end
```
```

For Greeter.m, add this method:

```
Download `Classes/HelloWorld11/Greeter.m`

```objective-c
-(id) initWithName:(NSString *) newName {
    if (self = [super init]) {
        name = newName;
    }
    return self;
}
```
```

Once you learn about properties in the next chapter, you'll use something a bit more robust than the following:

```
```objective-c
name = newName;
```
```

You'll use a property to set the value of the name and take care of the memory management while you're at it.

You can now refactor the init method to call initWithName: to eliminate the duplicated code:

```
Download `Classes/HelloWorld11/Greeter.m`

```objective-c
-(id) init {
    return [self initWithName:@"World"];
}
```
```

This method replaces greeter in HelloWorldAppDelegate.m:

```
Download `Classes/HelloWorld11/HelloWorldAppDelegate.m`

```objective-c
- (Greeter *) greeterFor:(NSString *) personName {
    return [[Greeter alloc] initWithName:personName];
}
```
```