# Array Objects 343

```
NSString *aName = "@Julia Kochan";nNSString *aEmail = "@jewels33@aol.com";nNSString *bName = "@Tony_Iannino";nNSString *bEmail = "@Tony.ianninotechfitness.com";nNSString *cName = "@Stephen Kochan";nNSString *cEmail = "@steve@classroomM.com";nNSString *dName = "@Jamie Baker";nNSString *dEmail = "@jbaker@classroomM.com";
```

```
AddressCard *card1 = [[AddressCard alloc] init];nAddressCard *card2 = [[AddressCard alloc] init];nAddressCard *card3 = [[AddressCard alloc] init];nAddressCard *card4 = [[AddressCard alloc] init];
```

```
// Set up a new address book
```

```
AddressBook *myBook = [[AddressBook alloc]
initWithName:@Linda's Address Book];
```

```
NSLog(\@Entries in address book after creation: %i",n[myBook entries]);
```

```
// Set up four address cards
```

```
[card1 setName:aName andEmail:aEmail];n[card2 setName:bName andEmail:bEmail];n[card3 setName:cName andEmail:cEmail];n[card4 setName:dName andEmail:dEmail];
```

```
// Add the cards to the address book
```

```
[myBook addCard:card1];n[myBook addCard:card2];n[myBook addCard:card3];n[myBook addCard:card4];
```

```
NSLog(\@Entries in address book after adding cards: %i",n[myBook entries]);
```

```
// List all the entries in the book now
```

```
[myBook list];
```

```
[card1 release];
[card2 release];
[card3 release];
[card4 release];
[myBook release];
[pool drain];
return 0;
```

```
}
```