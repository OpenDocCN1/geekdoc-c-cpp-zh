# Array Objects 351

Because you are doing a string comparison of the two names from the address book, you can use the NSString compare: method to do the work for you.
If you add the sort method to the AddressBook class and the compareNames: method to the AddressCard class, you can write a test program to test it (see Program 15.13).

# Program 15.13 Test Program

```
#import "AddressBook.h"

int main (int argc, char *argv[]) {

NSAutleasePool *pool = [NSAutleasePool alloc] init];

NSString *aName = @"Julia Kochan";
NSString *aEmail = @"jewls337@axlc.com";
NSString *bName = @"Tony Iannino";
NSString *bEmail = @"Tony.Iannino@techfitness.com";
NSString *cName = @"Stephen Kochan";
NSString *cEmail = @"steves@classroom.com";
NSString *dName = @"Jamie Baker";
NSString *dEmail = @"jbaker@classroom.com";

AddressCard *card1 = [[AddressCard alloc] init];
AddressCard *card2 = [[AddressCard alloc] init];
AddressCard *card3 = [[AddressCard alloc] init];
AddressCard *card4 = [[AddressCard alloc] init];

AddressBook *myBook = [AddressBook alloc];

// First set up four address cards
[card1 setName:aName aEmail:aEmail];
[card2 setName:bName bEmail:bEmail];
[card3 setName:cName cEmail:cEmail];
[card4 setName:dName dEmail:dEmail];

myBook = [myBook initWithName:@Linda's Address Book];

// Add some cards to the address book
[myBook addCard:card1];
[myBook addCard:card2];
[myBook addCard:card3];
[myBook addCard:card4];

// List the unsorted book
[myBook list];

// Sort it and list it again
[myBook sort];
[myBook list];n
```