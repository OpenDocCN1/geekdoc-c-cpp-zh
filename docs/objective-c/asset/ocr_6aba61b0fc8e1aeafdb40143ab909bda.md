# Listing 12.4

# Using format strings

```
NSString *str;

NSString *cardName = @"Ace";
NSString *cardSuit = @"Spades";

str = [NSString stringWithFormat:@"The winning card is %@ of %@.",
    cardName, cardSuit];
// str is "The winning card is Ace of Spades."

str = [NSString stringWithFormat:@"You have %ld gold!",
    [player goldAmount]];
// str is "You have 1000 gold!"

str = [NSString stringWithFormat:@"Your change is: $%.2f.", change];
// str is "Your change is $2.43
```

Notice that the arguments passed when working with format strings are passed using an unusual syntax. The format string allows you to pass a variadic argument list to the +stringWithFormat method. The count of arguments is determined by how many format specifiers are provided.

# NOTE

To ensure your code is 64-bit safe, it's generally considered a best practice to use the %ld format specifier when working with integers. When using NSInteger as the type for your integers, it will automatically change with the architecture from 32-bit to 64-bit. Using %ld for your format specifier insures that the format string will work with either 32-bit or 64-bit NSIntegers, regardless of their size.

# Working with Other NSString Methods

Using format strings allows you to create strings in a much more flexible fashion than if you simply had to append them together. Various applications for format strings are available aside from simply constructing new strings. For example, you can also append a formatted string, as shown in Listing 12.5.