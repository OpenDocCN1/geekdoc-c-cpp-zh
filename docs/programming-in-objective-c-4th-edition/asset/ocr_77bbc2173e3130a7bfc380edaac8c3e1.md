There are sorting methods in the NSArray and NSMutableArray classes that take blocks as arguments for comparing elements in an array in lieu of selectors.

The general format of the NSArray method is:

+   - (NSArray *) sortedArrayUsingComparator:
(NSComparator) block

while that of the NSMutableArray method, which does the sort in place, looks like this:

+   - (void) sortUsingComparator:(NSComparator) block

NSComparator is defined this way as a typedef in one of the system header files:

```
typedef NSComparisonResult (^NSComparator)(id
obj1, id obj2);
```

Translating this into English, it says that NSComparator is a block that takes two objects as arguments and returns a value of type NSComparisonResult. This method, since it uses blocks, will probably run faster for sorting large arrays. So consider using it in your applications for that reason.

So the block takes the two objects to compare as its arguments and is expected to return an indicator of whether the first object should be considered, less than, equal to, or greater the second object. This is consistent with the method that gets called by the non-block versions of the array sort methods.

The block we supply as the argument to the sortUsingComparator: method can just call our compareNames: method to compare the address cards like so: