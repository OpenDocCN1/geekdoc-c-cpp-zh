```
AddressBook *myBook = [AddressBook
alloc]
initWithName:
@"Linda's Address Book";
AddressCard *myCard;
```

```
// Now set up four address cards

[card1 setName: aName andEmail: aEmail];
[card2 setName: bName andEmail: bEmail];
[card3 setName: cName andEmail: cEmail];
[card4 setName: dName andEmail: dEmail];
```

```
// Add some cards to the address book

[myBook addCard: card1];
[myBook addCard: card2];
[myBook addCard: card3];
[myBook addCard: card4];
```

```
// Try another lookup

NSLog (@"Haibo Zhang");
myCard = [myBook lookup: @"Haibo Zhang"];
```