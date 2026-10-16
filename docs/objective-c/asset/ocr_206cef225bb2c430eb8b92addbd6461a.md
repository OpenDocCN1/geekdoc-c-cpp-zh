```
```objective-c
// implementation - goes in MyPoint.m
#import "MyPoint.h"
@implementation MyPoint
@synthesize x;
@synthesize y;
@end
```
```

Listing 6.21 shows the Observer class. This class will simply take a MyPoint and add itself as an observer. Nothing to it.

# Listing 6.21

The Observer class

```
```objective-c
// Interface - goes in Observer.h
#import <Cocoa/Cocoa.h>
#import "MyPoint.h"

@interface Observer : NSObject
{
    MyPoint *point;
}
@property (retain) MyPoint *point;
- (id)initWithPoint:(MyPoint *)inPoint;
@end
```
```

```
```objective-c
// Implementation - goes in Observer.m
#import "Observer.h"

@implementation Observer
@synthesize point;

- (void)dealloc
{
    [point removeObserver:self forKeyPath:@"x"];
    [point removeObserver:self forKeyPath:@"y"];
    [point release];
}
```
```