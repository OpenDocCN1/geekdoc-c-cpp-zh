referenced by the instance variable because they reference the same object. Reread that last sentence to make sure you understand that point. Also realize that a completely new object does not cause this problem. The problem occurs only if one or more characters of the string are modified in some way.

The solution to this particular problem is to make a new copy of the string inside the setter you want to protect and make it completely independent of the setter's argument. This is why you chose to make a copy of the name and email members in the setName: and setEmail AddressCard methods in Chapter 15.

# An Autorelease Example

Let's take a look at one last program in this chapter to ensure that you really understand how reference counting, retaining, and releasing/autorelease objects work. Examine Program 17.6, which defines a dummy class called Foo with one instance methods inherited.

Program 17.6

```
@import <Foundation/Foundation.h>

@interface Foo: NSObject
    int x;
@end

@implementation Foo
@end

int main (int argc, char *argv[]) {
    AutoreleasePool *pool = [[AutoreleasePool alloc] init];
    Foo *myFoo = ([Foo alloc] init];
    NSLog("@myFoo retain count = %lx", (unsigned long) [myFoo retainCount]);

    [pool drain];
    NSLog("@@after pool drain = %lx", (unsigned long) [myFoo retainCount]);

    pool = [[AutoreleasePool alloc] init];
    [myFoo autorelease];
    NSLog("@@after autorelease = %lx", (unsigned long) [myFoo retainCount]);

    [myFoo retain];
    NSLog("@@after retain = %lx", (unsigned long) [myFoo retainCount]);

    [pool drain];
    NSLog("@@after second pool drain = %lx", (unsigned long) [myFoo retainCount]);
}
```