collections that contain both keys and objects which must be associated to each other. To access a given element of the collection, you request the element by asking for the object associated with a given key.

Often, instances of `NSString` are used as the keys for the dictionary. This is not a requirement. The objects used as keys can be of any type, provided they implement the `NSCopying` protocol and are unique. The dictionary determines uniqueness via the `NSObject` method `isEqual:` versus other keys in the dictionary, and will throw an exception if you attempt to create a dictionary with two keys that are the same.

Like `NSArray`, `NSDictionary` can be initialized either by using an initializer or by using one of the numerous `NSDictionary` class factory methods. Listing 13.5 shows several examples of how to create instances of `NSDictionary`.

# Listing 13.5

# Creating instances of NSDictionary

```
NSDictionary *dict;

// normal initializer...

dict = [[NSDictionary alloc] initWithObjects:@"foo", @"bar", @"baz"
                             forKeys:@"one", @"two", @"three"
                              count:3];

// factory method

dict = [NSDictionary dictionaryWithObjects:@"foo", @"bar", @"baz"
                              forKeys:@"one", @"two", @"three"
                               count:3];

// this one reads in a plist file and uses it to create the dict...

dict = [NSDictionary dictionaryWithContentsOfFile:@"something.plist"];

// just like the NSArray...

dict = [NSDictionary dictionaryWithObjectsAndKeys:
        @"foo", @"one",
        @"bar", @"two",
        @"baz", @"three",
        nil];
```