# Listing 8–1. Iterating through NSSet via enumerator.

```
1 NSSet *mySet = [NSSet initWithObjects:@"One", @"Two", @"Three", nil];
2 for (id value in mySet) {
3   NSLog("%@", value);
4 }
```

> NOTE: On line #3, the class of the value is id. Recall that an id is a generic type that represents any Objective-C class. The reason that id is used is that the value we store in the NSSet can be of any type. For example, if the NSSet were to contain a class called Animal and another class called Zoo, the code would fail because we don't have a class that is both Zoo and an Animal type. On the other hand, if the NSSet always had the same class, we could substitute for the id on line #3.

Another common method of accessing an NSSet, especially when programming for an iOS device capturing touches, is to use the following:

# Listing 8–2. Selecting any objects in the NSSet collection.

```
1 NSSet *mySet = [NSSet initWithObjects:@"One", @"Two", @"Three", nil];
2 NSString *value = [mySet AnyObject];
```

Line #3 calls the method AnyObject. This does exactly as it says; it returns any object from the set. The object returned is determined by the set's convenience so there can be no guarantee that the first item will be returned. Of course, using the AnyObject assumes that any object will do. Previously mentioned, when dealing with touches on an iOS device, sometimes that is necessary to know that at least one has touched the screen. Each touch to the screen is stored as an entry in the NSSet, one for each finger. Using AnyObject will return any one of the touches.

There are other ways to actually get objects from an NSSet—far too many to cover in this chapter.¹ However, there is one particular method that involves the next collection—the NSArray class.

# NSArray

The NSArray class is like any other class, in that it allows the programmer to manage a group of objects. The NSArray differs from the NSSet in that the NSArray allows any object to be retrieved by its index into the array. An index is the numeric position that an object would occupy in the NSArray. For example, if there are three elements in the

> ¹httpdeveloper.apple.com/library/mac/#Cocoa/Reference/Foundation/Classes/NSSet_Class/Reference/Reference.html