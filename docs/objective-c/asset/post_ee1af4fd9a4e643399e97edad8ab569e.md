
You can access individual elements of an NSDictionary by using the object method -objectForKey:, which retrieves the object associated with the given key. Listing 13.6 shows an example of this operation.

## Listing 13.6
### Accessing an individual elements of an NSDictionary

```
NSLog(@"%@", [dict objectForKey:@"one"]); // prints 'foo'

NSLog(@"%@", [dict objectForKey:@"two"]); // prints 'bar'
```

Just like when using the NSArray class, there are variants of this method which take as parameters, multiple keys to access multiple objects at once. One variant of these calls is the -objectsForKeys:notFoundMarker:, which calls for an object that will be returned in the event that a given key is not found. Listing 13.7 shows an example of this method in use.

## Listing 13.7
### Using the method -objectsForKeys:notFoundMarker:

```
NSArray *keys = [NSArray arrayWithObjects:@"one", @"ten", @"two"];

NSArray *items = [dict objectsForKeys:keys notFoundMarker:[NSNull null]];

// items now contains [@"foo", NSNull, @"bar"]
```

As is the case with NSArray, nil values, structures, and scalars cannot be stored as objects in an NSDictionary. You need to wrap them, instead, by using NSNull, NSValue, or NSNumber, respectively.

In addition to being able to access individual elements of an NSDictionary by key, you can also retrieve all keys in the dictionary or all objects in the dictionary by using the methods -allKeys or -allObjects, respectively. Both of these methods return an instance of NSArray which can then subsequently be used in the same patterns as NSArray for the purposes of enumeration. That is, you can enumerate over all of the keys, or all of the objects in an NSDictionary by enumerating over these arrays using a for loop, a while loop, and so on. Listing 13.8 shows an example of doing this.

## Listing 13.8
### Enumerating over the keys and objects in NSDictionary

```
// these two have the same output
// iterating the objects...
NSArray *objects = [dict allObjects];
for (NSString *obj in objects)
{
    NSLog(@"%@", obj);
}

// default is to iterate the keys
for (NSString *key in dict)
{
    NSLog(@"%@", [dict objectForKey:key]);
}
```

In addition to using the -allKeys method to get an array you can use iteration to loop over the dictionary's values using the -allObjects method. Just iterating using the dictionary itself as the iteration object as shown here allows you to loop over the keys as well.

Finally, you can also retrieve a sorted array of keys in an NSDictionary by using the method -sortedKeysUsingSelector:. I cover more about sorting collections shortly, so I won't discuss this method here other than to simply inform you that it exists.

Like NSArray, NSDictionary cannot contain nil keys or objects, and it cannot contain scalars or structs.

NSDictionary is usually implemented internally as a hash table. Therefore, access by key to a given object is typically going to be O(1). Again, this is not specified explicitly, so, your mileage may vary.

## Working with sets

The NSArray class provides a collection for use with an ordered collection of objects, and the NSSet provides a class for working with unordered collections of objects. Using an NSSet, you can store objects that do not have to be stored in a particular order. The fact that an NSSet is unordered enables it to be slightly faster when accessing individual elements, though they cannot be accessed by index or key.

Again, creating an NSSet is done by using either an initializer or one of the numerous NSSet class factory methods. Listing 13.9 shows how to create an NSSet using a factory method and how to manipulate the members of the set.

## Listing 13.9
### Creating an NSSet

```
NSSet *set = [NSSet setWithObjects:@"foo", @"bar", @"baz"];

NSLog(@"%@", [set member:@"foo"]); // outputs foo

NSLog(@"%@", [set anyObject]); // prints one of them, no idea which

NSLog(@"%@", [set allObjects]); // [@"foo", @"bar", @"baz"]

NSLog(@"%d", [set containsObject:@"baz"]); // prints '1'
```

Object stored in an NSSet must respond to the NSObject methods -isEqual: and -hash. If the -hash method of an object stored in an NSSet depends on the internal state of the object, the stored object must not change while it is in the set.

Accessing objects in the set can be done by using the methods -allObjects, which returns an array containing all of the objects in the set, -anyObject which returns a non-deterministic object from the set, or -member: which returns the member of the set that matches the passed in parameter determined by using the method -isEqual:. Finally, the method -anyObject returns a non-deterministic member of the set.

You can iterate over the objects of the NSSet by using fast enumeration or an NSEnumerator.

Listing 13.10 shows accessing objects in an NSSet and enumerating over an NSSet.

## Listing 13.10
### Operations on an NSSet

```
NSSet *set = [NSSet setWithObjects:@"foo", @"bar", @"baz"];

NSLog(@"%@", [set member:@"foo"]); // outputs foo

NSLog(@"%@", [set anyObject]); // prints one of them, no idea which

NSLog(@"%@", [set allObjects]); // [@"foo", @"bar", @"baz"]

NSLog(@"%ld", [set containsObject:@"baz"]); // prints '1'

for(NSString *item in set)
{
    NSLog(@"%@", item);
}

NSEnumerator *enumerator = [set objectEnumerator];
NSString *item = nil;
while((item = [enumerator nextObject]))
{
    NSLog(@"%@", item);
}
```

Foundation also provides a subclass of NSSet called NSCountedSet. This nifty class allows you to add the same object to the set multiple times. The NSCountedSet keeps track of how many times you added a given object, but only actually stores the object once. It keeps a running count of the number of times the given object is added to the set and requires an equal number of -removeObject: calls to actually remove the object.

NSCountedSet’s implementation of the -count method returns the number of distinct objects, not the total number of times all objects were added to the set. In order to access the count for a given object, you can use the method -countForObject:.

## Understanding mutability

Each of the collection classes that I’ve introduced you to so far have been immutable. After you create the collection, you cannot add objects to or remove objects from the collection. Collections wouldn’t be particularly useful if you were limited to adding or removing objects from them.

Therefore, Foundation also provides mutable versions of all of these classes. The names of the mutable versions of the classes are NSMutableArray, which corresponds to NSArray, NSMutableDictionary, corresponding to NSDictionary, and NSMutableSet that corresponds to NSSet. Each of these classes provides additional methods, in addition to the read-only methods of their immutable counterparts for the purposes of adding, removing, and replacing objects within the collections.

NSMutableArray provides the method -addObject: for placing an object at the end of the array, -insertObject:atIndex: for inserting an object at a specific index, -removeLastObject for removing the last object in the array, -removeObjectAtIndex: for removing an object at a given index, and -replaceObjectAtIndex:withObject: for replacing a given object at a specified index with another object. Listing 13.11 shows some examples of using these methods on an NSMutableArray.

## Listing 13.11
### Manipulating the elements of an NSMutableArray

```
NSMutableArray *array = [NSMutableArray array];

[array addObject:@"foo"];
[array addObject:@"baz"];
[array insertObject:@"bar" atIndex:1];
// now [@"foo", @"bar", @"baz"]

[array removeLastObject];
// now [@"foo", @"bar"]

[array removeObjectAtIndex:0];
// now [@"bar"]

[array replaceObjectAtIndex:0 withObject:@"boz"];
// now [@"boz"]
```

There are naturally plural forms of each of these methods that perform the same operations with arrays of objects or ranges of indexes.

Similarly, NSMutableDictionary provides methods for manipulating its contents as well. For example, to add an object into the dictionary, you use the method -setObject:forKey:. To remove an object, you use the method -removeObjectForKey:. Listing 13.12 shows an example of manipulating an NSMutableDictionary.
