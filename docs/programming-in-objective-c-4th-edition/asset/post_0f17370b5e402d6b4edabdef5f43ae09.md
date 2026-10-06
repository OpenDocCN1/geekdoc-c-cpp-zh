
drawn is stored inside an id variable called currentObject, for example, you could paint it on the screen simply by sending it the draw message:

```
[currentObject draw];
```

You could even test it first to ensure that the object stored in currentObject actually responds to a draw method. You'll see how to do that later in this chapter, in the section called "Asking Questions About Classes."

# Compile Time Versus Runtime Checking

Because the type of object stored inside an id variable can be indeterminate at compile time, some tests are deferred until runtime—that is, while the program is executing.

Consider the following sequence of code:

```
Fraction *f1 = [[Fraction alloc] init];
[f1 setReal: 10.0 andImaginary: 2.5];
```

Recalling that the setReal:andImaginary: method applies to complex numbers and not fractions, the following message is issued when you compile the program containing this line:

```
'Fraction' may not respond to
'setReal:andImaginary':
```

The Objective-C compiler knows that f1 is a Fraction object because it has been declared that way. It also knows that when it sees the message expression

```
[f1 setReal: 10.0 andImaginary: 2.5];
```

the Fraction class does not have a setReal:andImaginary: method (and did not inherit one, either). Therefore, it issues the warning message shown previously.

Now consider the following code sequence:

```
id dataValue = [[Fraction alloc] init];
...
[dataValue setReal: 10.0 andImaginary: 2.5];
```

These lines do not produce a warning message from the compiler because the compiler doesn't know what type of object is stored inside dataValue when processing your source file (No, the compiler doesn't see that earlier a Fraction object was stored inside variable!)

No error message is reported until you run the program containing these lines. The program crashes, and the error contains a bunch of lines, one of which looks like this:

> [-Fraction setReal:andImaginary:]: unrecognized selector sent to instance 0x103f00

When the program is executing, the system first checks the type of object stored inside dataValue. Because dataValue has a Fraction stored in it, the runtime system looks for a method setReal:andImaginary: defined for the Fraction class. Because it can't find such a method, the error message shown previously is issued and the program is terminated.

# The id Data Type and Static Typing

If an id data type can be used to store any object, why don't just declare all your objects as type id? For several reasons, you don't want to get into the habit of overusing this generic class data type.

First, when you define a variable to be an object from a particular class, you are using what's known as static typing. The word static refers to the fact that the type of object that will be stored in the variable is being explicitly declared. So the class of the object stored in that type is predetermined, or static. When you use static typing, the compiler ensures, to the best of its ability, that the variable is used consistently throughout the program. The compiler can check to ensure that a method applied to an object is defined or inherited by that class; if not, it issues a warning message. Thus, when you declare a Rectangle variable myRect in your program, the compiler checks any methods you invoke on myRect are defined in the Rectangle class or are inherited from its superclass.

# Note

Certain techniques make it possible to invoke methods that are specified by a variable, in which case the compiler can't check that for you.

However, if this check is performed for you at runtime anyway, why do you care about static typing? You care because it's better to get your errors out during the compilation phase of your program than during the execution phase. If you leave it until runtime, you might not even be the one running the program when the error occurs. If your program is put into production, some poor unsuspecting user might discover when when running the program that a particular object does not recognize a method by having the program crash on her.

Another reason for using static typing is that it makes your programs more readable. Consider the following declaration:

```
id f1;
```

versus

```
Fraction *f1;
```

Which do you think is more understandable—that is, which makes the intended use of the variable f1 clearer? The combination of static typing and meaningful variable names (which we intentionally did not choose in the previous example) can go a long way toward making your program self-documenting.

# Argument and Return Types with Dynamic Typing

If you use dynamic typing to invoke a method, note the following rule: If a method with the same name is implemented in more than one of your classes, each method must agree on the type of each argument and the type of value it returns so that the compiler can generate the correct code for your message expressions.

The compiler performs a consistency check among each class declaration it has seen. If one or more methods conflict in either argument or return type, the compiler issues a warning message. For example, both the Fraction and Complex classes contain add: methods. However, the Fraction class takes as its argument and returns a Fraction object, whereas the Complex class takes returns a Complex object. if frac1 and myFract are Fraction objects, compl and myComplex are Complex objects, statements such as

```
result = [myFract add: frac1];
```

and

```
result = [myComplex add: compl];
```

do not cause any problems. This is because, in both cases, the receiver of the message is statically typed and the compiler can check for consistent use of the method as it is defined in the receiver's class.

If dataValue1 and dataValue2 are id variables, the statement
result = [dataValue1 add: dataValue2];

causes the compiler to generate code to pass the argument to
add: method and handle its returned value by making assumptions.
At runtime, the Objective-C runtime system will check the actual
class of the object stored inside dataValue1 and select the
appropriate method from the correct class to execute. However, in a
more general case, the compiler might generate the incorrect code
to pass arguments to a method or handle its return value. This would
happen if one method took an object as its argument and the other
took a floating-point value, for example. Or if one method returned
an object and the other returned an integer, for example. If the
inconsistency between two methods is just a different type of object
(for example, the Fraction's add: method takes a Fraction
object as its argument and returns one, and the Complex's add:
method takes and returns a Complex object), the compiler will still
generate the correct code because memory addresses (that is,
pointers) are passed as references to objects anyway.

# Asking Questions About Classes

As you start working with variables that can contain objects from
different classes, you might need to ask questions such as the
following:

- Is this object a rectangle?
- Does this object support a print method?
- Is this object a member of the Graphics class or one of its
descendants?

You can then use the answers to these questions to execute different
sequences of code, avoid an error, or check the integrity of your
program while it's executing.

Table 9.1 summarizes some of the basic methods that the NSObject class supports for asking these types of questions. In this table, class-object is a class object (typically generated with the class method), and selector is a value of type SEL (typically created with the @selector directive).

## 9.1. Methods for Working with Dynamic Types

| Method | Question or Action |
| --- | --- |
| -(BOOL) isKindOf:class-object | Is the object a member of class-object or a descendant? |
| -(BOOL) isMember:class-object | Is the object a member of class-object? |
| -(BOOL) respondsTo:selector | Can the object respond to the method specified by selector? |
| +(BOOL) instancesRespondTo:selector | Can instances of the specified class respond to selector? |
| +(BOOL) isKindOfClass:class-object | Is the object a subclass of the specified class? |
| -(id) performSelector:selector | Apply the method specified by selector. |
| -(id) performSelector:selector withObject:object | Apply the method specified by selector passing the argument object. |
| -(id) performSelector:selector withObject:object withObject:object | Apply the method specified by selector with the arguments object1 and object2. |

Other methods are not covered here. One enables you to ask whether an object conforms to a protocol (see Chapter 11, Categories and Protocols). Others enable you to ask about dynamically resolving methods (not covered in this text).

To generate a class object from a class name or another object, you send it the class message. To get a class object from a class named Square, you write the following:

```
[Square class]
```
