# Listing 6.2

# Accessing the attributes of our classes using KVC accessors

```
Foo *foo = [[Foo alloc] init];
[foo setValue:@"blah blah" forKey:@"stringOnFoo"];
NSString *string = [foo valueForKey:@"stringOnFoo"];
[foo setValue:@"The quick brown fox." forKeyPath:@"bar.stringOnBar"];
NSString *string2 = [foo valueForKeyPath:@"bar.stringOnBar"];
```

So, as you can see, literally speaking, you can specify the name of the attribute that you want to access using a string, and you can read its value or you can write its value. You can even, as shown in the case where you are accessing the attributes of the Bar class, traverse a relationship between two objects and access the attributes of child objects of the primary object that you are accessing.

This may seem a bit confusing at first, and you may wonder why you need to know this. For most of your day-to-day coding, using Key Value Coding methods to set and access your properties probably will wind up being more typing, and more error-prone than simply accessing the setters and getters on your class directly. However, a small number of edge cases where being able to access these attributes dynamically, using values that can change at runtime rather than at compile time, can be incredibly powerful.

Listing 6.3 shows an example of a class that needs to serialize a pen object into a database table. In the first example shown, the serialization routine iterates over each of the fields of the table. As it iterates it needs a complex if statement to determine what accessor to call on the object that it is attempting to serialize so it can get the value to be serialized into the given field.

# Listing 6.3

# Serializing a table without KVC.

```
-(BOOL)serializeToTable:(Table *)inTable
{
    Row *row = [inTable addRow];
    for(Column *column in row)
    {
        if([[column name] isEqualToString:@"firstName"])
            [column setValue:[self firstName]];

```