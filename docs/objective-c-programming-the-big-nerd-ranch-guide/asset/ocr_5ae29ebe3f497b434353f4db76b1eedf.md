The nil at the end is how you tell the method to stop. Thus, this colors array would only have three strings. (If you forget the nil, it will probably crash your program.)

Most beginning programmers are surprised by the existence of *NSArray*. Why would anyone want a list that can’t be changed? There are two reasons:

+   You don’t trust the people you work with. That is, you want to let them look at an array, but you don’t want them to be able change it. A gentler approach is to give them an *NSMutableArray*, but *tell* them it is an *NSArray*. For example, imagine the following method:

```
// Returns an array of 30 odd numbers
- (NSArray *)odds
{
static NSMutableArray *odds = [[NSMutableArray alloc] init];
int i = 1;
while ([odds count] < 30) {
[odds addObject:[NSNumber numberWithInt:i]];
i += 2;
}
return odds;
}
```

Anyone calling this method assumes it is returning an immutable *NSArray*. If the caller tries to add or remove items from the returned object, the compiler will issue a stern warning – even though, it is, in fact, an instance of *NSMutableArray*.

+   The other reason is performance: an immutable object never needs to be copied. With a mutable object, you might make a private copy so that you know that no other code in the system can change it from underneath you. This is unnecessary for immutable objects. In fact, while the *copy* method of *NSMutableArray* makes a new copy of itself and returns a pointer to the new array, the *copy* method of *NSArray* does nothing – it just returns a pointer to itself.

As a result, immutable objects are fairly common in Objective-C programming. In Foundation, there are many classes that create immutable instances: *NSarray*, *NSString*, *NSAttributedString*, *NSData*, *NSCharacterSet*, *NSDictionary*, *NSSet*, *NSIndexSet*, and *NSURLRequest*. All of these have mutable subclasses: *NSMutableArray*, *NSMutableString*, *NSMutableAttributedString*, etc. *NSDate* and *NSNumber*, on the other hand, are immutable but don’t have mutable subclasses.

# Sorting

There are several ways to sort an array, but the most common way is to use an array of *sort descriptors*. *NSMutableArray* has the following method:

```
- (void)sortUsingDescriptors: (NSArray *)sortDescriptors;
```

The argument is an array of *NSSortDescriptor* objects. A sort descriptor has the name of a property of the objects contained in the array and whether that property should be sorted in ascending or descending order. Why do we pass an array of sort descriptors? Imagine you said, “Sort this list of doctors by last name in ascending order.” What if two doctors have the same last name? You can specify “Sort by last name ascending, and if the last names are the same, sort by first name ascending, and if the first and last names are the same, sort by zip code.”