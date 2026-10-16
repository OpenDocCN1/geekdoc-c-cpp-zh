
## CAUTION

Calling -setObject:forKey: with a key that already exists in the dictionary will replace the old object with the new one.

## Listing 13.12

## Manipulating the elements of an NSMutableDictionary

```
NSMutableDictionary *dict = [NSMutableDictionary dictionary];

[dict setObject:@"foo" forKey:@"one"];
[dict setObject:@"bar" forKey:@"two"];
[dict setObject:@"baz" forKey:@"three"];

// dict now contains all three objects and keys

[dict removeObjectForKey:@"two"];

// dict now only has foo and baz in it
```

Finally, NSMutableSet provides similar functionality with the methods -addObject:, and -removeObject:. Additionally, it also provides specialized methods for adding and removing groups of objects. -unionSet:, for example adds all the objects from another set to the receiver. Similarly, -minusSet: removes a set of objects from the receiver.

## Understanding Collections and Memory Management

You have to be careful when working with collections in a non-garbage collected memory environment. When an object is removed from the collection, it is released. This has several implications for you as a developer.

First and foremost, because the collection will be retaining objects that are added to it, you do not need to retain those objects outside of the collection if you don’t have some other good reason to do so. You can assume that by placing the object into the collection, that the collection then owns it. When the collection is deallocated, it sends a release to each of the objects in the collection, so you do not need to be concerned about the potential for memory leaks, because the collection fulfills that part of the memory management contract.

Secondly, because objects are released when removed from a collection, the possibility that a given object that you intend to continue to use but which is being removed from a collection, may be released without your being aware of it. Listing 13.13 shows an example of this problem when using an NSMutableArray.

## Listing 13.13

## Error when removing an object from an NSMutableArray

```
NSMutableArray *array = [NSMutableArray arrayWithObjects:@"foo", @"bar", @"baz", nil];

NSString *item = [array objectAtIndex:1];

[array removeObjectAtIndex:1]; // item is released here.

NSLog(@"%@", item); // error!!
```

The error in this code occurs because although you have retrieved the object from the array, you have not retained it. As long as you do not remove the object from the array, it is still retained by the array and therefore can be manipulated at will. However, if you remove the object from the array, it is immediately released. Therefore, accessing the method on the object as shown here causes an error.

The correct way to write this code is to retain the object that you have retrieved from the array prior to removing it from the array. Listing 13.14 shows the same code corrected.

## Listing 13.14

## The correct way to remove an object you wish to continue using

```
NSMutableArray *array = [NSMutableArray arrayWithObjects:@"foo", @"bar", @"baz", nil];

NSString *item = [array objectAtIndex:1];

[item retain]; // keep it around!

[array removeObjectAtIndex:1]; // item is released here.

NSLog(@"%@", item); // OK

[item release]; // remember to release it since you retained it!
```

Obviously, when working in a garbage collected environment, these types of problems do not occur.

## Using specialized collections

A few collection classes serve specific narrow purposes. Although they are rarely used, it’s nice to know that they exist, if you need them; these are NSPointerArray, NSHashTable, and NSMapTable. They are primarily used in garbage collected environments for specialized collections requiring weak relationships.

Each of them provides an interface that is similar to, but does not inherit from a specific type of collection. NSPointerArray for NSArray, NSHashTable for NSSet, and NSMapTable for NSDictionary.

Because of their similarity of purpose and their rarity of use, I won’t belabor this subject by going into a great amount of detail on every one of these, however, it can be useful to look at one of these three, NSPointerArray, for the purposes of example since the design pattern used in its construction is similar enough to the other two as to not require additional explanation.

The class NSPointerArray is probably one of the most powerful of these specialized collection classes. It specifies an NSArray like interface but allows for the insertion of null values and arbitrary pointers. Additionally, by specifying certain options when creating an instance of NSPointerArray, you can configure your array to have specific memory management policies with regard to the objects stored within it. For example, you can specify that objects that get reclaimed by the garbage collector get replaced by a NULL value. To do this, you create a zeroing weak memory configuration by using the NSPointerFunctionsZeroingWeakMemory option.

You specify the options for your instance of NSPointerArray when you create it using the methods -initWithOptions: or -initWithPointerFunctions:. When using the method -initWithOptions:, you are specifying that the array that you are creating will obey the policies set forth by the options that you are passing as a parameter. The options, which are specified using a bitwise-or, set specific policies or “personalities” for the array. For example, to create an array to store standard C-style strings that require strcmp to compare them and malloc/free for memory management, you do something like Listing 13.15.

## Listing 13.15

## An NSPointerArray to store C strings

```
NSPointerArray *array = [[NSPointerArray alloc] initWithOptions:
    (NSPointerFunctionsCStringPersonality|
    NSPointerFunctionsMallocMemory)];
```

You can only specify one such personality option and one such memory option for a given instance.

Alternatively, for maximum flexibility, you can use the initializer -initWithPointerFunctions: that allows you to specify an instance of NSPointerFunctions as a parameter. This class encapsulates the functions that will be used by the array for operations, such as hashing, equality finding, storage, and deletion. Each of these different operations has a corresponding function that you can configure by using an instance of this class. When you pass this instance to the NSPointerArray, it will then use the functions that you have defined when objects are inserted, removed, and so on, in place of the normal retain, release, and other methods that would be used in a normal NSArray.

The cases when you actually need to use NSPointerArray are probably few and far between. However, it is available as a tool if you need it.

## Enumerating

The elements of a collection can be iterated over by using fast enumeration or by using an NSEnumerator. By using fast enumeration, you simply use a standard for loop. Enumerating in this way over an NSArray or NSSet enumerates over each element of the collection. Using fast enumeration on an NSDictionary enumerates over its keys.

Listing 13.16 shows each of these three collection types being enumerated.

## Listing 13.16

## Enumerating over collections using fast enumeration

```
NSMutableArray *array = [NSMutableArray arrayWithObjects:@"foo",
    @"bar", @"baz", nil];

for(NSString *item in array)
{
    NSLog(@"%@", item);
}
```

Alternatively, you can use “old style” enumeration, using NSEnumerator. In this method, you acquire an NSEnumerator for your collection and then call the NSEnumerator object method -nextObject repeatedly until you receive a nil, which indicates the end of the collection. This is shown in Listing 13.17.

## Listing 13.17

## Enumerating the collections using NSEnumerator

```
NSEnumerator *enumerator = [array objectEnumerator];
NSString *item = nil;
while((item = [enumerator nextObject]))
{
    NSLog(@"%@", item);
}
```

There is also a reverse enumerator that you can access, which will enable you to iterate over the elements of the container in reverse. This can actually be used both in the traditional while loop as well as using fast enumeration, as shown in Listing 13.18.

## Listing 13.18

## Enumerator Tricks

```
NSEnumerator *enumerator = [array reverseObjectEnumerator];
NSString *item = nil;
while((item = [enumerator nextObject]))
{
    NSLog(@"%@", item);
}
```
