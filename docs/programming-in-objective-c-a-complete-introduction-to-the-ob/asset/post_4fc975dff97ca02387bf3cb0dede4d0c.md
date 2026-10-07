
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

```
// Equality test
if ([set1EqualTo:set2] == YES)
NSLog("@set1 equals set2");
else
  NSLog("@set1 is not equal to set2");

// Membership test
if ([set1 containsObject:TOBJ(10)] == YES)
NSLog("@set1 contains 10");
else
  NSLog("@set1 does not contain 10");

if ([set2 containsObject:TOBJ(10)] == YES)
NSLog("@set2 contains 10");
else
  NSLog("@set2 does not contain 10");

// add and remove objects from mutable set1

[set1 addObject:TOBJ(4)];
[set1 removeObject:TOBJ(10)];
NSLog("@set1 after adding 4 and removing 10: ");
[set1 print];

// get intersection of two sets

[set1 intersectSet:set2];
NSLog("@set1 intersect set2: ");
[set1 print];

// union of two sets

[set1 unionSet:set3];
NSLog("@set1 union set3: ");
[set1 print];

[pool drain];
return 0;
```

# Program 15.16 Output

```
set1:
{ 3 10 1 5 }
set2:
{ 100 3 -5 5 }
set1 is not equal to set2
set1 contains 10
set2 does not contain 10
set1 after adding 4 and removing 10:
{ 3 1 5 4 }
set1 intersect set2:
{ 3 5 }
set1 union set3:
{ 12 3 5 200 }
```

# Chapter 15 Numbers, Strings, and Collections

The print method uses the fast enumeration technique previously described to retrieve each element from the set. You also defined a macro called INTBOJ to create an object from an integer value. This enables you to make your program more concise and saves some unnecessary typing. Of course, your print method is not general because it works only with sets that have members in them. But it's a good reminder of how to add methods to a class through a category: (Note that the C library's printf routine is used in the print method to display elements of set on a single line.) setWithObjects: creates a new set from a nil-terminated list of objects. After creating three sets, the program displays the first two using your print method. isEqualSet: method tests whether set is equal to set2—it's.

The containsObject: method tests whether the integer 10 is in set and whether it is in set2. The Boolean value the method returns verify that it is in the first set, not in the second.

The program next the addObject: and removeObject: methods to add and remove 4 and 10 from set, respectively. Displaying the contents of the set that the operations were successful.

You can use the intersect: and union: methods to calculate the intersection and union of two sets. In both cases, the result of the operation replaces the receiver of the message.

The framework also provides a class called NSCountSet. These sets represent more than one occurrence of the same object; however, instead of adding multiple times in the set, a count of times is maintained. The first time an object is added to the set, its count is 1. Subsequently adding the object to the set increments the count, while removing the object decrements the count. If it reaches zero, the actual object is removed from the set. countFor: retrieves the count for a specified object in a set.

One application for a counted set could be a word counter application. Each time a word is found in some text, it can be added to the counted set. When the text is complete, each word is retrieved from the set along with its count, which indicates the number of times the word appeared in the text.

We have just shown some basic operations with sets. Tables 15.9 and 15.10 summarize commonly used methods for working with immutable and mutable sets,.. NSMutableSet is a subclass of NSSet, it inherits its methods.

In Tables 15.9 and 15.10, obj, obj, obj2 are any objects; nset is an NSSet or NSMutableSet object; and size is an NSInteger integer.

> A more general method could invoke each object's description method for displaying each member of the set. That would allow sets containing any types of objects to be displayed in a readable format. Also note that you can display the contents of any collection with a single call to NSLog, using the the "print object" format characters "%@".

# Table 15.9 Common NSSetMethods

| Method | Description |
| --- | --- |
| +(id) setWithObjects:obj1,obj2,..., nil | Creates a new set from the list of objects |
| -(id) anyObject | Returns any object from the set |
| -(id) initWithObjects:obj1,obj2,..., nil | Initializes a newly allocated set with a list of objects |
| -(NSInteger) count | Returns the number of members in the set |
| -(BOOL) containsObject:obj | Determines whether the set contains obj |
| -(BOOL) member:obj | Determines whether the set contains obj (using the isEqual:method) |
| -(NSEnumerator) objectEnumerator | Returns an NSEnumerator for all the objects in the set |
| -(BOOL) isSubsetOf:nset | Determines whether every member of the receiver is present in nset |
| -(BOOL) intersectsSet:nset | Determines whether at least one member of the receiver appears in nset |
| -(BOOL) isEqualTo:nset | Determines whether the two sets are equal |

# Table 15.10 Common NSMutableSet Methods

| Method | Description |
| --- | --- |
| +(id) setWithObjects:obj1,obj2,..., nil | Creates a new set from the list of objects |
| -(id) anyObject | Returns any object from the set |
| -(id) initWithObjects:obj1,obj2,..., nil | Initializes a newly allocated set with a list of objects |
| -(NSInteger) count | Returns the number of members in the set |
| -(BOOL) containsObject:obj | Determines whether the set contains obj |
| -(BOOL) member:obj | Determines whether the set contains obj (using the isEqual:method) |
| -(NSEnumerator) objectEnumerator | Returns an NSEnumerator for all the objects in the set |
| -(BOOL) isSubsetOf:nset | Determines whether every member of the receiver is present in nset |
| -(BOOL) intersectsSet:nset | Determines whether at least one member of the receiver appears in nset |
| -(BOOL) isEqualTo:nset | Determines whether the two sets are equal |
| -(void) addObject:obj | Adds an object to the set |
| -(void) removeObject:obj | Removes an object from the set |
| -(void) intersectSet:nset | Keeps only objects that are also in nset |
| -(void) unionSet:nset | Adds all objects from nset to the set |
| -(void) subtractSet:nset | Removes all objects that are also in nset |

# NSIndexSet

This class is used to store ordered indexes into some data structure, typically an array. You can use this class, for example, to efficiently generate a list of numbers from an array where each object satisfies some criteria.You’ll want to note that there is no mutable versionAs an example, the NSArray method indexOfObjectsPassingTest takes a block as its argument. The block gets executed for each element in the array, passing in the array index, and a pointer to a BOOL variable. The code in the block will presumably test the element against some criteria and return YES if the array satisfies the criteria, and NO if it does not Even if the method returns YES, the method will continue processing the next element until all elements have been processed. You can stop processing at any time by setting the value the BOOL pointer reference to YES. (Refer back to Chapter 13, for a discussion on pointers.)

If the indexOfObjectsPassingTest finds a match (meaning you returned YES from your block at least one), it will return the lowest match from the set. If no match is found, it will return NSNotFound.

Here's a modified version of the lookup: method from our AddressBook class.

```
- (AddressCard *) lookup: (NSString *) *theName
```nNSInteger result = [block indexOfObjectsPassingTest:
^ (id obj, NSInteger idx, BOOL *stop)
{
    if ([[obj] caseInsensitiveCompare:theName] ==
NSOrderedSame) {
        *stop = YES; // found a match, one is enough
        return YES;
    }
    else
        return NO; // keep looking
}];
```

See if we found != NSNotFound

```
if (result != NSNotFound) // there should be only one element
    return [object objectAtIndex:result];
else
    return nil;
```

If you are looking to find all the matches in the array, you could store each match inside the block and never the stop pointer to YES. In that way the indexOfObjectsPassingTest method would examine all the elements in the array. Here's what a method might look like:

```
- (MutableArray *) lookupMatches: (NSString *) *theName
```nMutableArray *matches = [MutableArray array];

IndexSet *result = [block indexOfObjectsPassingTest:
^ (id obj, NSInteger idx, BOOL *stop)
{
```
