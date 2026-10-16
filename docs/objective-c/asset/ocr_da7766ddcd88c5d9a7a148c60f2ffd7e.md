usually more code than you need. But in these kinds of conditions it enables you to write code that is more dynamic and also enables you to reduce the number of places in your code where you have to represent the information about the attributes of your objects. When you can query an object about its attributes, you don’t have to commit that information to as many places in code. That’s always a good thing — the most bug-free code is code that isn’t written.

# Working with key paths

In order to use key value coding, you must first figure out which key paths you can construct and what you can access with those keep paths.

You can think of working with KVC accessors like using a dictionary. The keys to the dictionary are strings. The strings themselves are the names of the attributes on the object on which you are operating. Because of this requirement, a certain number of rules have to be followed in terms of your key and thus attribute naming. First, your keys must use ASCII encoding. This means that you cannot have keys that use unusual characters that would not normally be usable in an attribute name. Secondly, your keys must begin with a lowercase letter. Underscores are also allowed for this first letter, but no numbers, and no uppercase. Finally, your key cannot contain any whitespace.

Thankfully, because the attribute that you’re accessing has to be a valid symbol name anyway, most of these rules are rules that you are probably already following in the first place.

Listing 6.5 shows some examples of valid key paths and invalid key paths.

# Listing 6.5

# Valid and invalid key paths.

```
// valid
[foo valueForKeyPath:@"someMember"];
[foo valueForKeyPath:@"someMember.someAttributeOnMember"];
[foo valueForKeyPath:@"someOtherMember"];

// invalid
[foo valueForKeyPath:@"4fun"];
[foo valueForKeyPath:@"kermit the frog"];
[foo valueForKeyPath:@"SomethingWickedThisWayComes"];
[foo valueForKeyPath:@"THISWONTWORK"];
[foo valueForKeyPath:@"thisAlsoWon'tWork"];
```