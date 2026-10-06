```
-(id) initWithCoder:(NSCoder *) decoder
{
    bookName = [[decoder decodeObjectForKey:@"AddressBookName"];
    book = [decoder decodeObjectForKey:@"AddressBook"];

    return self;
}

// Method for NSCopying protocol

-(id) copyWithZone:(NSZone *) zone
{
    id newBook = [[self class] allocWithZone:zone] init;

    [newBook setBookName:bookName];

    // The following will do a shallow copy of the address book

    [newBook setBook:book];

    return newBook;
}
@end
```