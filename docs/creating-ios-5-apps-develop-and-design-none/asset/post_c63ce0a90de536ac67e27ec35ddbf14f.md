
## METHODS

Once all the bells and whistles are stripped away, an Objective-C method is simply a C function. Therefore, everything we learned about functions applies equally to methods. There is one important difference, however. When we call a C function, the function and its arguments are connected at compile time (static binding). In contrast, in Objective-C we are not actually calling the method; we are sending a message to the object, asking it to call the method. The object then uses the method name to select the actual function. This connection of selector, function, and arguments is done at runtime (dynamic binding).

This has a number of practical implications. First and foremost, you can send any method to any object. After all, we may dynamically add the method's implementation at runtime, or we may forward the method to another object altogether.

More commonly, we use this feature along with the object identifier type id, which can refer to any object (including Class objects). Notice that we do not use an asterisk when declaring id variables. The id type is already defined as a pointer to an object.

```
id myString = @"This is a string";      // This is an NSString.
id myStringClass = [myString class];    // This is a class object.
```

The one-two punch of id types and dynamic binding lets us avoid a lot of the complex, verbose constructions that statically bound languages ordinarily require, but it's not just about running around naked and free; as developers, we typically know more about our application than the compiler does.

For example, if we put only NSString objects into an array, we know that all the objects in that array will respond to the length message. In C++ or Java, we would need to convince the compiler to let us make that call (usually by casting the object). Objective-C (for the most part) trusts that we know what we're doing.

Still, it's not all Wild West shooting from the hip. Xcode's compiler and static analyzer do an excellent job of analyzing our code and finding common errors (like misspelled method names), even when writing highly dynamic code.

## SENDING MESSAGES TO NIL

In Objective-C it is perfectly legal to send messages to nil. This often comes as a shock to people from a Java background. In Java, if you call a method on null (null and nil are identical, a pointer with a value of 0—basically a pointer that points to nothing), your application will crash. In Objective-C, the method simply returns 0 or nil (depending on the return type).

Newcomers to Objective-C often argue that this hides errors. By crashing immediately, Java prevents the program from continuing in a bad state and possibly producing faulty output or crashing inexplicably at some later point in the application. There is a grain of truth to this. However, once you accept the fact that you can send messages to nil, you can use it to produce simple, elegant algorithms.

Let’s look at one of the more common design patterns. Imagine an RSS reader that must download a hundred different feeds. First you call a method to download the XML file. Then you parse the XML. Due to potential networking problems, the first method is likely to be highly unreliable. In Java, we would need to check and make sure that we received a valid result.

```
XML xml = RSS.getXMLforURL(myURL);
// Make sure we have a valid xml object.
if (xml != null) {
    xml.parse();
    ...
}
```

In Objective-C, those checks are unnecessary. If the XML is nil, the method call simply does nothing.

```objectivec
XML* xml = [RSS getXMLforURL:myURL];
[xml parse];
...
```

Also, let’s face it, null pointers are a common source of bugs in Java applications. Java’s null pointer violates the language’s otherwise strict static typing. If you can assign it to an object variable, you should be able to treat it just like any other object. That includes calling instance methods and receiving reasonable results.

## CALLING METHODS

Objective-C methods are called using square brackets. Inside the brackets, we have the receiver and the message. The receiver can be any variable that evaluates to an object (including self), the super keyword, or a class name (for class methods). The message is the name of the method and any arguments.

```
[receiver message]
```

In C, the method's arguments are all grouped together in parentheses after the function's name. Objective-C handles them somewhat differently. If the method doesn't take any arguments, the method name is simply a single word (usually a camel-case word with a lowercase first letter).

```
[myObject myFunctionWithNoArguments];
```

If the method takes a single argument, the name ends in a colon (:) and the argument immediately follows it.

```
[myObject myFunctionWithOneArgument:myArgument];
```

Multiple arguments are spread throughout the method name. Usually, the method name will give a clue about the type of argument expected in each position.

```
[myObject myFunctionWithFirstArgument:first
                secondArgument:second
                thirdArgument:third];
```

When referring to the method, we typically concatenate all the parts of its name without spaces or arguments. For example, the above method is named `myFunctionWithFirstArgument:secondArgument:thirdArgument:`.

While this style may seem awkward at first, it can be a great aid when coding. It's almost impossible to accidentally place the arguments in the wrong order (something I do all the time in C-like languages). Interleaving the method name and arguments also encourages the use of longer, more expressive method names, and—for my money—that's always a good thing.

Methods are normally declared in the class's `@interface` block and defined in the `@implementation` block. Like C functions, the declaration is simply the method signature followed by a semicolon. The definition is the method signature followed by a block of code within curly brackets.

## CLASS METHODS

Class methods are called on the class (using the class name), not on individual objects. We have already seen class methods in action; alloc is an example of a class method—we call [NSString alloc], not [myStringObject alloc].

Most class methods are convenience methods that simplify the creation of new objects. Others encapsulate useful utility functions related to the class. For example, NSString defines a class method named availableStringEncodings. You can call this method to get a nil-terminated list of all the string encodings supported by the NSString class.

Method signatures start with either a + or - character. The - is used for instance methods, while the + is used for class methods. Next we have the return type in parentheses, and then the method name. Arguments are defined in place within the name. Simply follow the colon with the argument type in parentheses and the argument's name.

    - (void)simple;                       // No arguments, no return
                                         // value.
    - (int)count;                        // No arguments, returns an
                                         // integer.
    - (NSString*) nameForID:(int)id;     // Takes an integer argument.
                                         // Returns a string object.
                                         // Class method with multiple
                                         // arguments.
    + (NSString*) fullNameGivenFirstName:(NSString*)first
                                  middleName:(NSString*)middle
                                     lastName:(NSString*)last;

Objective-C methods always have two hidden arguments: self and _cmd. The _cmd argument is the method’s selector. The selector is a unique identifier of type SEL that is used to look up methods at runtime. You can create a SEL from a method's name using @selector(). You can also get the string representation of a SEL using NSStringFromSelector().

The connection between C functions and Objective-C methods really becomes clear when you start dynamically adding methods to an object, as shown:

```objc
// Defined before the @implementation block.
void myFunction(id self, SEL _cmd) {
    NSLog(@"Executing my method %@ on %@",
          NSStringFromSelector(_cmd),
          self);
}
// Defined inside the @implementation block.
+ (void)addMethod {
    SEL selector = @selector(myMethod);
    class_addMethod(self, selector, (IMP)myFunction, "v@:");
}
```

Running the class method addMethod will add myMethod to the current class at runtime. You can then call [myObject myMethod], and it will call the function myFunction(myObject, @selector(myMethod)).

## INITIALIZERS

We've already discussed an object's two-step instantiation. Now let's look at the initializer methods themselves. These are just methods like any other method we may write; however, there are a few conventions we need to follow to get everything right.

First, there's the name. All the initializers traditionally start with init. Do yourself (and anyone who might maintain your code in the future) a huge favor and always follow this naming convention.

Next, there are two methods that require special attention: the class's designated initializer and the superclass's designated initializer.
