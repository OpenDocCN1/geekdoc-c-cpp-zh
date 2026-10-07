# Set Objects

A *set* is a collection of unique objects, and it can be mutable or immutable. Operations include searching, adding, and removing members (mutable sets); comparing two sets; and finding the intersection and union of two sets.

In this section we'll take a quick look at three set classes: NSSet, NSMutableSet, and NSIndexSet. We'll also mention the class NSCountedSet in passing so you'll know when you might need or want to use that set.

Program 15.16 shows basic operations on sets. Say you want to display the contents of your set several times during execution of the program. You therefore decided to create a new method called print. You can add the print to the NSSet class by creating a new category Printing. NSMutableSet is a subclass of NSSet, so mutable sets can use the new method as well.

Program 15.16

```
#import <Foundation/Foundation.h>

// Create an integer object
#define OBJINT(v) [NSNumber numberWithInteger:v]

// Add a print method to NSSet with the Printing category

@interface NSSet (Printing)
-(void) print;
@end

@implementation NSSet (Printing)
-(void) print {
    for (NSNumber *element in self) {
        printf("%%li, %long [element integer]", (long)[element integerValue]);
    }
    printf("\n");
}
@end

int main (int argc, char *argv[]) {
AutoreleasePool *pool = [AutoreleasePool alloc];

NSMutableSet *set1 = [NSMutableSet setWithObjects:
    OBJINT(1), OBJINT(3), OBJINT(10), nil];
NSSet *set2 = [NSSet setWithObjects:
    OBJINT(-5), OBJINT(100), OBJINT(5), nil];
NSSet *set3 = [NSSet setWithObjects:
    OBJINT(12), OBJINT(200), OBJINT(3), nil];

NSLog("@set1: %@");
[set1 print];
NSLog("@set2: %@");
[set2 print];
```