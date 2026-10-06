```
{
  return [name compare: [element name]];
}
```

Because you are doing a string comparison of the two names from the address book, you can use the NSString compare: method to do the work for you.

If you add the sort method to the AddressBook class and the compareNames: method to the AddressCard class, you can write a test program to test it (see Program 15.13).

# Program 15.13. Test Program

```
#import "AddressBook.h"

int main (int argc, char * argv[]) {

  @autoreleasepool {
    NSString *aName = @"Julia Kochan";
    NSString *aEmail = @"jewls337@axlc.com";
    NSString *bName = @"Tony Iannino";
    NSString *bEmail = @"tony.iannino@techfitness.com";
    NSString *cName = @"Stephen Kochan";
    NSString *cEmail = @"steve@classroomM.com";
    NSString *dName = @"Jamie Baker";
    NSString *dEmail = @"jbaker@classroomM.com";

    AddressCard *card1 = [[AddressCard alloc] init];
    AddressCard *card2 = [[AddressCard
```