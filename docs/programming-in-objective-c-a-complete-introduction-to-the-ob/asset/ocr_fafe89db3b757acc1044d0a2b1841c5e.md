# Chapter 15 Numbers, Strings, and Collections

As an example, the NSArray method indexOfObjectsPassingTest takes a block as its argument. The block gets executed for each element in the array, passing in the array index, and a pointer to a BOOL variable. The code in the block will presumably test the element against some criteria and return YES if the array satisfies the criteria, and NO if it does not Even if the method returns YES, the method will continue processing the next element until all elements have been processed. You can stop processing at any time by setting the value the BOOL pointer reference to YES. (Refer back to Chapter 13, for a discussion on pointers.)

If the indexOfObjectsPassingTest finds a match (meaning you returned YES from your block at least one occasion), it will return the lowest match from the set. If no match is found, it will return NSNotFound.

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
    if ([[obj] caseInsensitiveCompare:theName] ==
NSOrderedSame) {
```
```