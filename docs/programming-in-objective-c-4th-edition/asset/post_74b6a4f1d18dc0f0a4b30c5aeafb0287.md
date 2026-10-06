
# Program 9.5. Exception Handling

```objc
#import "Fraction.h"

int main (int argc, char * argv [])
{
    @autoreleasepool {
        Fraction *f = [[Fraction alloc] init];

        @try {
            [f noSuchMethod];
        }
        @catch (NSException *exception) {
            NSLog("Caught %@@@", [exception name], [exception reason]);
            NSLog("Execution continues!");
        }
    }
    return 0;
}
```

# Program 9.5. Output

*** -[Fraction noSuchMethod]: unrecognized selector sent to instance 0x103280
Caught NSInvalidArgumentException: -[Fraction noSuchMethod]: unrecognized selector sent to instance 0x103280
Execution continues!

When the exception occurs, the @catch block gets executed. An NSException object that contains information about the exception passed as the argument into this block. As you can see, the name method retrieves the name of the exception, and the reason method gives the reason (which the runtime system previously printed automatically).

After the last statement in the @catch block is executed (we have only one here), the program continues execution with the statement immediately following the block. In this case, execute NSLog call to verify that execution has continued and has not been terminated.

This is a very simple example to illustrate how to catch exceptions in a program. An @finally block can be used to include code to execute whether or not a statement in a @try block throws an exception.

An @throw directive enables you to throw your exception. You can use it to throw a specific exception, or inside a @catch block to throw the same exception that took you into the block like this:

```objc
@throw;
```

You might want to do this after handling an exception yourself (perhaps after performing cleanup work, for example). You can then let the system handle the rest of the work for you.

You can have multiple @catch blocks that are sequenced to catch and handle different type of exceptions.

In general, you don't want exceptions to occur while your program is running. So it is considered better programming practice to test for errors before they occur rather than catch them after they occur. It's also better to test for an error in a method and return some value as an error indicator than to throw an exception. Throwing exceptions use a lot of system resources, and, as such, Apple generally recommends against their unnecessary use (e.g., you don't want to throw an exception simply because you can't open a file).

# Exercises

- 1. What will happen if you insert the message expression `[compResult reduce];` to Program 9.1 after the addition is performed? Try it and see.
- 2. Can the id variable dataValue, as defined in Program 9.2, be assigned a Rectangle object as you defined it in Chapter 8? That is, the statement `dataValue = [[Rectangle alloc] init];` Why or why not?
- 3. Add a print method to your XYPoint class defined in Chapter 8. Have it display the point in the format (x, y). Then modify Program 9.2 to incorporate an XYPoint object. Have the modified program create an XYPoint set, set its value, assign it to the id variable dataValue, and then display its value.
- 4. Based on the discussions about argument and return types in this chapter, modify add methods in the Fraction and Complex classes to take and return id objects. Write a program that incorporates the following code sequence:

```objc
result = [dataValue1 add: dataValue2];
[result print];
```
Here, result, dataValue1, and dataValue2 are id objects. Make sure you set dataValue1 and dataValue2 appropriately in your program.

# Note

You'll have to change the name of the methods to something other than add:. That's because the system's NSObject class also has an add: method. As noted earlier in this chapter in the “Arguments and Return Types with Dynamic Typing" section, if multiple methods of the same name exist in different classes and the type of the receiver isn't known at compile time, the compiler will perform a consistency check to make sure the arguments and return types are consistent among the similarly named methods.

- 5. Given the Fraction and Complex class definitions having been used in this text and the following definitions:

```objc
Fraction *fraction = [[Fraction alloc init];
Complex *complex = [[Complex alloc init];
id number = [[Complex alloc init];
```
Given determine the return value from the following message expressions. Then type them into a program to verify the results.

```objc
[fraction isMemberOfClass:[Complex class]];
[complex isMemberOfClass:[NSObject class]];
[complex isKindOfClass:[NSObject class]];
[fraction isKindOfClass:[Fraction class]];
[fraction respondsToSelector:@selector (print)];
[complex respondsToSelector:@selector (print)];
[Fraction instancesRespondToSelector:@selector (print)];
[number respondsToSelector:@selector (print)];
[number isKindOfClass: [Complex class]];
[[number class] respondsToSelector: @selector (alloc)];
```

# 10. More on Variables and Data Types

In this chapter, we go into more detail about variable scope, initialization methods for objects, and data types.

The initialization of an object deserves some special attention, which we give it here.

We talked freely about the scope of instance variables as well as static and local variables in Chapter 7 "More on Classes." We talk more about static variables here and introduce the concept of global and external ones. In addition, you can give certain directives to the Objective-C compiler, to more precisely control the scope of your instance variables. We cover these directives in this chapter as well.

An enumerated data type enables you to define the name for a data type to be used only to store a specified list of values. The Objective-C language's typedef statement lets you assign your own name to a built-in or derived data type. Finally, in this chapter, we describe in more detail the precise steps the Objective-C compiler follows when converting data types in the evaluation of expressions.

# Initializing Objects

You've seen the pattern before: You allocate a new instance of an object and then initialize it, using a familiar sequence like this:

```objc
Fraction *myFract = [[Fraction alloc] init];
```

We didn't write our own init method; we use the one inherited from the parent class, which is NSObject.

After these two methods are invoked, you typically assign some values to the new object, like this:

```objc
[myFract setTo: 1 over: 3];
```

The process of initializing an object followed by setting it to some initial values is often combined into a single method. For example, you can define a initWith:over: method that initializes a fraction and sets its numerator and denominator to the supplied arguments.

A class that contains many methods and instance variables commonly has several initialization methods as well. For example, the Foundation framework's NSArray class contains the following initialization methods:

```objc
initWithArray:
initWithArray:copyItems:
initWithContentsOfFile:
initWithContentsOfURL:
initWithObjects:
initWithObjects:count:
```

An array might be allocated and then initialized with:

```objc
myArray = [[NSArray alloc] initWithArray:otherArray];
```

It's common practice for all the initializers in a class to begin with init. As you can see, NSArray's initializers follow that convention. You should adhere to the following strategies when writing initializers:

```objc
(id)init
{
    self = [super init];
    if (self) {
        // Initialization code here.
    }
    return self;
}
```
