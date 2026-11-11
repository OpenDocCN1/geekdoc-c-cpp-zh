object referenced by myAdder that takes one parameter, in this case the literal 7, would appear as follows:

```
`[myAdder add1: 7];`
```

If a method takes two parameters and has only one part to its name, a colon follows the first parameter and the second parameter follows that. No other punctuation is used between the two parameters. If there are more parameters, this pattern is repeated. For example, if add1 takes three parameters and has no other parts to its name, it could be called with the following:

```
`[myAdder add1: 7 : 5 : 3];`
```

A method could have multiple parameters and multiple parts to its name, as in the previous example:

```
`-(int) meth2: (int) x second: (float) y;`
```

An example call to this method follows:

```
`[myObject meth2: 7 second: 3.2];`
```

Constructors in Objective-C are called **initializers**; they only provide initial values. They can be given any name, and as a result they must be explicitly called. Constructors return a reference to the new object, so their type is always a pointer to the class name. They use a **return** statement that returns `self`, a reference to the current object.

An object is created in Objective-C by calling **alloc**. Typically, after calling **alloc**, the constructor of the class is explicitly called. These two calls can be and usually are cascaded, as in the following statement, which creates an object of `Adder` class with **alloc** and then calls its constructor, `init`, on the new object, and puts the address of the new object in `myAdder`:

```
`Adder *myAdder = [[Adder alloc]init];`
```

All class instances are heap dynamic and are referenced through reference variables.

C programs nearly always import a header file for input and output functions, `stdio.h`. In Objective-C, a header file is usually imported that has the prototypes of a variety of often required functions, including those for input and output, as well as some needed data. This is done with the following:

```
`#import <Foundation/Foundation.h>`
```

Nearly all of the code in the `main` function of a program usually is placed in a compound statement that follows `@autoreleasepool`. Any objects that are created in the compound statement are automatically released at the end of the compound statement.