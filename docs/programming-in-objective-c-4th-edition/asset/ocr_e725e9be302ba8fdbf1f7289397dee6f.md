```
@interface AddressBook: NSObject

@property (nonatomic, copy) NSString *bookName;
@property (nonatomic, strong) NSMutableArray *book;

-(id) initWithName:(NSString *) name;
-(void) addCard:(AddressCard *) theCard;
-(int) entries;
-(void) list;

@end
```

The strong attribute for a property says to make an additional reference to the object whenever the setter method is used. It influences the life span of the object. It is described in more detail in [Chapter 17], "Memory Management and Automatic Reference Counting."

The initWithName: method sets up the initial array to hold the address cards and store the name of the book, whereas the addCard: method adds an AddressCard to the book. The entries method reports the number of address cards in your book, and the list method gives a concise listing of its entire contents. [Program 15.10] shows the implementation file for your AddressBook class.

# Program 15.10. AddressBook.m Implementation File

```
#import "AddressBook.h"

@synthesize bookName, book;
```