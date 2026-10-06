implementing a copy method for the AddressCard class, which contains name and email members, the following implementation for copyWithZone: would suffice:

```
- (AddresssCard *) copyWithZone: (NSZone *) zone {
AddressCard *newCard = [[AddressCard] allocWithZone: zone] init];

[newCard assignName: name andEmail: email];
return newCard;
}

-(void) assignName: (NSString *) andEmail: (NSString *) theEmail {
name = theName;
email = theEmail;
}
```

the setName:andEmail: method isn’t used here to set the instance variables because method makes new copies of its arguments, which would defeat the whole purpose of this exercise. Instead, you just assigned the two variables using a new method called assignName:andEmail.

Realize that you can get away with assigning the instance variables here (instead of making complete copies of them) because the owner of the copied card can't affect the name and email members of the original card (those contain immutable string objects). Because our two instance variables are "strong" variables by default, doing a simple assignment to them creates another reference to the object, as explained in more detail in Chapter 17.

# Exercises