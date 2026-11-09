
## Cocoa messaging and notifications

Cocoa includes a separate messaging system with more sophisticated features. *Notifications* are like an internal e-mail or chat service. You can use them to pass information between applications or between objects within an application. Objects can sign up to receive notifications and can post them through a notification center. Notifications can include complex data. They’re a system-level feature, while Objective-C messaging is a language-level feature. The two messaging systems are unrelated and are used in different ways.

## Objective-C syntax

Now that you’ve seen some of the ways in which messaging is used in Cocoa, you may be curious about messaging code. Objective-C uses square brackets to indicate messages. For example:

```objective-c
[anObject doSomething];
```

triggers the `doSomething` method in anObject.

The messaging syntax can pass parameters.

```objective-c
[anObject doSomethingWith: anInt];
```

triggers `doSomethingWith:` and passes it an int. Parameter fields can have descriptive name strings. For example, in

```objective-c
[anObject doSomethingWith: anInt andABoolToo: YES];
```

`doSomethingWith:` and `andABoolToo:` are part of the message syntax. They’re effectively code-based tooltips, included for clarity and legibility, and they don’t affect execution.

![](img/2b293e29fc15b0797f113b85dd429b6e_57_0.png)

> **CAUTION**
>
> Objective-C treats `aMethod` and `aMethod:` (that takes a parameter) as completely different entities. It’s good practice in your own code to keep method names as distinct as possible. Some Cocoa method names don’t do this; you’ll occasionally see an identical method name followed by a number of different parameter groupings. Objective-C understands the difference, but you may find it harder to remember.

This idiom is often used in Cocoa classes to include hints about the purpose of each field. For example

```objective-c
[aWindow setHasShadow: YES];
```

enables a drop shadow effect for aWindow. Replacing YES with NO turns off the drop shadow. This feature helps make Cocoa code easy to read. But sometimes it gets out of hand. Objective-C is chatty rather than terse, and some Cocoa methods have very long names. The full syntax for the `dragImage:` method built into Cocoa’s `NSWindow` window object is

```objective-c
[aWindow dragImage: anImage
          at:aPoint
          offset:anOffset
          event:anEvent
          pasteboard:aPasteboard
          source:anObject
          slideBack:aBool];
```

This isn’t quite so easy to remember — and if the field names were more descriptive, the method would be even harder to parse. Unfortunately long method names are unavoidable in Objective-C and Cocoa.

![](img/2b293e29fc15b0797f113b85dd429b6e_58_0.png)

> **TIP**
>
> It’s good practice to split very long method names across multiple lines to make them more legible, putting each field on its own line.

Fortunately, you hardly ever have to type a long method name by hand. Xcode includes code automation that autocompletes method names for you. You can also copy and paste long method names directly from the documentation and fill in the fields with property names used in your code.

Messages can be nested, and the return from one message can be used as the input for another. A standard example is

```objective-c
MyClass *thisInstance = [[MyClass alloc] initWithData:
    initialData];
```

This idiom is used throughout Cocoa. The alloc method — short for allocate — is sent to MyClass and returns an instance of an object. The returned object is immediately initialized with initial data in the initWithData: method. A pointer to the initialized memory area is passed to thisInstance and used as the object reference.

### Objects and asterisks

Objective-C objects are referenced with named pointers defined with asterisks. Objective-C uses C’s asterisk convention for pointers, so you’ll see asterisks everywhere in Objective-C code. A standard idiom for creating a new object is

```objective-c
NSClass *myObject = [...aCreationMessage...];
```

The left-hand side of the assignment specifies that myObject is a pointer to an instance of NSClass. You can also declare pointers and reference them later in the usual C-like way:

```objective-c
NSClass *myObject; //Declares myObject as a pointer to an instance of NSClass
[...otherCode...]
myObject = [...aCreationMessage...]; //Creates an instance of NSClass and assigns it to myObject
```

Until you create and assign an object to a pointer, it remains NULL — but it still has a type.

Casts are widely used as “code tooltips” while passing parameters in messages to remind you which type of object to pass in a parameter field. For example:

```objective-c
...thisIsAParameterField: (NSClass *)myObject... //Reminds both you and the compiler that myObject should be an instance of NSClass
```

### Objective-C “objectification” with the @ character

Objective-C uses the @ character as an objectification operator that converts whatever follows into an object. This is most often used in text string definitions. In other languages, you delimit a string with quote marks. In Objective-C, you must also prepend the @ character to convert the string into an object. For example:

```objective-c
NSLog(@"This is a string");
```

This prints “This is a string” using Cocoa’s NSLog class, which logs output to a console window. You can also use the C-function equivalent:

```c
fprintf(stderr, "This is a string");
```

This line creates exactly the same result and is a functional synonym in conventional C without objectification.

In Objective-C, you must convert literal strings into objects wherever they appear. This is true whether they’re text strings, file and path elements, or used for some other purpose. If you leave out the @ character — which you often do, until you get used to typing it — the compiler won’t always report an error. In some circumstances, forgetting the @ can cause a crash.

## Managing data in Cocoa and Objective-C

Objective-C supports all the standard C data types, including arrays and custom structs. Cocoa adds its own collection of Cocoa objects that store and manage data. The most important objects are introduced in Table 2.5 and described in detail in Chapter 5.

**Table 2.5 Cocoa Data Objects**

| Data Objects | Description |
|---|---|
| NSArray | Stores a numbered list of objects. Supports enumeration. NSArray is much more complex than a simple C type array. |
| NSDictionary | Used throughout Cocoa. You must master NSDictionary to work with Cocoa successfully. Stores key-value pairs — pairs of named values — and can perform automatic lookup on a key to return its value. |
| NSSet | Stores an unordered collection of objects. NSSet is faster than NSArray when you need to test if an object is in a collection. |

Other languages support this. In Objective-C, this line compiles correctly, but it simply copies pointer values. After the assignment runs, you have two pointers to the same data instead of one. The data itself remains blissfully untroubled by the operation.

Objects are complex and may include other objects in a hierarchy or tree, so copying them may not be a simple process. Cocoa includes a set of standard NSCopying methods to support copying, but different objects implement a method called copyWithZone: with varying levels of intelligence and sophistication. When you create custom objects of your own, you must include code that implements the standard copy methods.

Many Cocoa objects include methods that create and initialize objects using the data in another object. This may seem counterintuitive when you encounter it for the first time because it looks redundant. In fact, it’s often the best way to copy data. For example, you can copy an array to a new array with

```objective-c
newArray = [NSArray arrayWithArray: oldArray];
```

If you need to copy objects, don’t look for direct copy methods in the documentation; if "copy" methods exist, they’re often disguised as initializations.

> **CAUTION**
>
> This code is slightly more complex than it looks because it's an example of class messaging in Cocoa. Instead of sending a message to an existing array, it sends a message to the NSArray class and passes the existing array as a parameter. Sometimes you copy objects by sending a message to an object, sometimes by sending a message to a class. There's little consistency in how Cocoa handles this; you must check the class documentation to find out which option to use.

### Comparing data objects

A related mistake is attempting to use a simple C comparison to compare objects:

```objective-c
if (anObject == anotherObject)...
```

You can do this in other languages to compare strings. In Objective-C, this code compiles and runs, but instead of comparing data, it compares pointer references, which are almost always different.

To compare the data, you must use a standard comparison method called isEqual:.

```objective-c
if ([anObject isEqual: anotherObject])...
```

isEqual: is available in typed variants for comparing specific objects, including isEqualToString: and isEqualToArray:. These variants are optimized and are more efficient than the generic comparison method. When you create a custom class, you'll need to implement a custom isEqual: method of your own if you want to compare instances.

> **CAUTION**
>
> Note the square brackets in the code. The brackets aren't optional; isEqual: is a message and not a function. You must include the brackets or the code won't compile.
