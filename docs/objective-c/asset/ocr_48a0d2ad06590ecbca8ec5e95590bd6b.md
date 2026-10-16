that under the 64-bit runtime is possible to declare properties that do not have member variables associated with them. In these cases, the only way to initialize and deallocate as member variables is by using their accessors.

In my code, I use accessors for initializing and deallocating member variables unless I know that doing so in a given circumstance will cause a problem. Also, when I implement a key value observer I ensure that the observer can properly handle nil values and I try to minimize any side effects.

If you feel that this is a risk worth taking, then feel free to write your initializers and dealloc method by using your accessors. Just be aware of the potential hazards involved, so that if and when you do encounter a problem, you know immediately where to look.

On the other hand, if you don’t feel that you can ensure this with your observers, follow Apple’s advice and do not use accessors in initializers and destructors unless you must.

# Applying Key Value Observing

Now that you understand all the details of Key Value Coding and Key Value Observing, take a look at a small example application with a few classes. One of those classes will observe the other classes, and as it receives notifications of changes to the attributes on the observed classes, it will print out those changes to the console.

Listing 6.20 shows the first class in this application. This simple point class has a couple of properties, x, and y. Just put the interface into the interface file, and the implementation in an implementation file.

```
```objc
// Interface - goes in MyPoint.h
#import <Cocoa/Cocoa.h>

@interface MyPoint : NSObject
{
    CGFloat x;
    CGFloat y;
}
@property CGFloat x;
@property CGFloat y;

@end
```
```