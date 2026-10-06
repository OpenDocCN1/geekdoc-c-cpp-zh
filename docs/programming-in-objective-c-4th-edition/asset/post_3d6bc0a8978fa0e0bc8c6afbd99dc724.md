
```objc
"@one", @"two", @"three", @"four",
nil];
NSMutableArray *dataArray2;
// simple assignment
dataArray2 = dataArray;
[dataArray2 removeObjectAtIndex: 0];
NSLog("@dataArray: " ");
for ( NSString *elem in dataArray )
    NSLog("@%@", elem);
NSLog("@dataArray2: " ");
for ( NSString *elem in dataArray2 )
    NSLog("@%@", elem);
// // try a copy, then remove the first
// element from the copy
dataArray2 = [dataArray mutableCopy];
[dataArray2 removeObjectAtIndex: 0];
NSLog("@dataArray: " ");
for ( NSString *elem in dataArray )
    NSLog("@%@", elem);
NSLog("@dataArray2: " ");
for ( NSString *elem in dataArray2 )
    NSLog("@%@", elem);
}
```

```objc
return 0;
}
```

# Program 18.1. Output

```
dataArray:
two
three
four
dataArray2:
two
three
four
dataArray:
two
three
four
dataArray2:
three
four
```

The program defines the mutable array object dataArray and sets its elements to the string objects @"one", @"two", @"three", and @"four". As we've discussed, the assignment

```objc
dataArray2 = dataArray;
```

simply creates another reference to the same array object in memory. When you remove the first object from dataArray2 and subsequently print the elements from both array objects, it's no surprise that the first element (the string @"one") is gone from both array object references.

Next, you create a mutable copy of dataArray and assign the resulting copy to dataArray2. This creates two distinct mutable arrays in memory, both containing three elements. Now when you remove the first element from dataArray2, it has no effect on the contents of dataArray, as verified by the last output for dataArray.

Note that making a mutable copy of an object does not require the object being copied be mutable. The same applies to immutable copies: You can make an immutable copy of a mutable object.

# Shallow Versus Deep Copying

Program 18.1 fills the elements of dataArray with immutable strings (recall that constant string objects are immutable). Program 18.2, you'll fill it with mutable strings instead so that you can change one of the strings in the array. Take a look at Program 18.2 and see whether you understand its output.

# Program 18.2

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSMutableArray *dataArray = [
            [NSMutableArray arrayWithObjects:
                [NSMutableString stringWithString:@"one"],
                [NSMutableString stringWithString:@"two"],
                [NSMutableString stringWithString:@"three"],
                nil
        ];
```

```objc
nil
];
NSMutableArray *dataArray2;
NSMutableString *mStr;

NSLog("@dataArray: %@");
for (NSString *elem in dataArray)
    NSLog("%@", elem);

// make a copy, then change one of the
// strings

dataArray2 = [dataArray mutableCopy];
mStr = [dataArray objectAtIndex: 0];
[mStr appendString: @"ONE"];

NSLog("@dataArray: %@");
for (NSString *elem in dataArray)
    NSLog("%@", elem);

NSLog("@dataArray2: %@");
for (NSString *elem in dataArray2)
    NSLog("%@", elem);
}
return 0;
}
```

# Program 18.2. Output

dataArray:
one
two
three

```
dataArray:
  one
  two
  three
dataArray2:
  one
  two
  three
```

You retrieved the first element of dataArray with the following statement:

```objc
mStr = [dataArray objectAtIndexIndex: 0];
```

Then you appended the string @"ONE" to it with this statement:

Notice the value of the first element of both the original array and its
copy: Both were modified. Perhaps you can understand why the first
element of dataArray was changed but not why its copy was
well. When you get an element from a collection, you get a new
reference to that element, but not a copy. So when the
objectAtIndex: method is invoked on dataArray, the returned
object points to the same object in memory as the first element in
dataArray. Subsequently modifying the string mStr has the
side effect of also changing the first element of dataArray, as you
see from the output.

But what about the copy you made? Why is its first element changed
as well? This has to do with the fact that copies, by default,
shallow copies. Thus, when the array was copied with the
mutableCopy method, space was allocated for a new object
in memory and the individual elements were copied into the new
array. But copying each element in the array from the original to a
new location meant just copying the reference from one element of
the array to another. The net result was that the elements of both arrays referenced the same strings in memory. This is no different from assigning one object to another, which we covered at the beginning of this chapter.

To make distinct copies of each element of the array, you must perform a deep copy. This means making copies of the contents of each object in the array, not just copies of the references to the objects (and think about what implies if an element of an array is itself an array object). But deep copies are not performed by default when you use the copy or mutable methods with the Foundation classes. In Chapter 19, “Archiving,” we show you how to use the Foundation’s archiving capabilities to create a deep copy of an object.

When you copy an array, a dictionary, or a set, for example, you get a new copy of those collections. However, you might need to make your own copies of individual elements if you want to make changes to one collection but not to copy. For example, if you wanted to change the first element of dataArray but not dataArray in Program 18.2, you could make a new string (using a method such as stringWithString:) and store it into the first location of dataArray2, as follows:

```objc
mStr = [NSMutableString stringWithString:[dataArray2 objectAtIndex: 0]];
```

Then you could make the changes to mStr and add it to the array using the replaceObject:atIndex:withObject: method, as follows:

```objc
[mStr appendString:@"ONE"];
[dataArray2 replaceObjectAtIndex: 0 withObject:mStr];
```

Hopefully you realize that even after replacing the object in memory, mStr and the first element of dataArray2 refer to the same

# Implementing the <NSCopying> Protocol

If you try to use the copy method on your own classes—example, on your address book, as follows

```objc
NewBook = [myBook mutableCopy];
```

you'll get an error message that looks like this:

> *** -AddressBook copyWithZone:]: not recognized
*** Uncaught exception:
*** -AddressBook copyWithZone:]: not recognized

As noted, to implement copying with your own classes, you have to implement one or two methods. 

We now show how you can add a copy method to your Fraction class, which you used extensively in Part I, "The Objective-C Language." Note that the techniques we describe here for copying strategies will work fine for your own classes. If those are subclasses of any of the Foundation classes, you might need to implement more sophisticated copying strategy. You'll have to account for the fact that the superclass might have already implemented its copying strategy.

Recall that your Fraction class contains two instance variables, called numerator and denominator. To make a copy of one of these objects, you must allocate space for a new fraction and simply copy the values of the two integers into the new fraction.

When you implement the <NSCopying> protocol, your class must implement the copyWithZone: method to respond to a copy message. (The copy message just sends a copyWithZone: message to your class with an argument of nil.) If you want to make a distinction between mutable and immutable copies, as we noted, you'll also need to implement the mutableCopyWithZone: method according to the <NSMutableCopying> protocol. If you implement both methods, copyWithZone: should return an immutable copy and mutableCopyWithZone: should return a mutable one. Making a copy of an object does not require the object copied be mutable (and vice versa); it's perfectly reasonable to want to make a mutable copy of an immutable object (consider a string object, for example).

Here's what the @interface directive should look like:

```objc
@interface Fraction NSObject <NSCopying>
```

Fraction is a subclass of NSObject and conforms to the NSCopying protocol.

In the implementation file Fraction.m, add the following definition for your new method:

```objc
- (id) copyWithZone: (NSZone *) zone {
    Fraction *newFract = [[Fraction allocWithZone: zone] init];
    [newFract setTo:numerator over:denominator];
    return newFract;
}
```

The zone argument has to do with different memory zones that you can allocate and work with in your program. You need to deal with
