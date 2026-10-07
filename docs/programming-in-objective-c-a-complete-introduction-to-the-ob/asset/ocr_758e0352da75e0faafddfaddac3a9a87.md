# Array Objects 347

Because you've made a couple of changes to your interface file, Program 15.12 shows it again with the new removeCard: method. It's followed by the implementation of your new method.

# Program 15.12 Addressbook.h Interface File

```
#import "AddressCard.h"
@interface AddressBook : NSObject
{
    NSString *bookName;
    NSMutableArray *book;
}

- (id) initWith:(NSString *)name;
- (void) addCard:(AddressCard *)theCard;
- (void) removeCard:(AddressCard *)theCard;

- (AddressCard *) lookup:(NSString *)theName;
- (int) entries;
- (void) list;

@end
```

Here's the new removeCard: method:

```
- (void) removeCard:(AddressCard *)theCard
{
    [book removeObjectIdenticalTo:theCard];
}
```

For purposes of what's considered an identical object, it's an object with the same location in memory. So the removeObjectIdenticalTo: method does not consider two address cards that contain the same information but are located in different places in memory (which might happen if you made a copy of an AddressCard, for example) to be identical.

Incidentally, the removeObjectIdenticalTo: method removes all objects identical to its argument. However, that is an issue only if you have multiple occurrences of the same object in your arrays.

You can get more sophisticated with your approach to equal objects by using the removeObject: and writing your own isEqual: method for testing whether two objects are equal. If you use addObject: the system automatically invokes isEqual: for each element in the array, giving it the two elements to compare. In this case, because your address book contains AddressCard objects as its elements, you would have to add an isEqual: method to that class (which would be overriding the method that class inherits from NSObject).The method could then decide for itself how to determine equality. It would make sense to compare the two corresponding