
## 3.1 Creating Objects

At the end of Chapter 1 we presented an overview of object-oriented concepts, including the basic relationship between classes and objects. Then in Chapter 2, in addition to discussing primitive data, we provided some examples of using objects for the services they provide. This chapter explores these ideas further.

In previous examples, we’ve used the println method many times. As we mentioned in Chapter 2, the println method is a service provided by the System.out object, which represents the standard output stream. To be more precise, the identifier out is an object variable that is stored in the System class. It has been predefined and set up for us as part of the Java standard class library. We can simply use it.

In Chapter 2 we also used the Scanner class, which represents an object that allows us to read input from the keyboard or a file. We created a Scanner object using the new operator. Once the object was created, we were able to use it for the various services it provides. That is, we were able to invoke its methods.

Let’s carefully examine the idea of creating an object. In Java, a variable name represents either a primitive value or an object. Like variables that hold primitive types, a variable that refers to an object must be declared. The class used to define an object can be thought of as the type of an object. The declarations of object variables have a similar structure to the declarations of primitive variables.

Consider the following two declarations:

```
int num;
String name;
```

The first declaration creates a variable that holds an integer value, as we’ve seen many times before. The second declaration creates a String variable that holds a reference to a String object. An object variable doesn’t hold an object itself, it holds the address of an object.

Initially, the two variables declared above don’t contain any data. We say they are uninitialized, which can be depicted as follows:

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_141_0.png)

As we pointed out in Chapter 2, it is always important to make sure a variable is initialized before using it. For an object variable, that means we must make sure it refers to a valid object prior to using it. In most situations, the compiler will issue an error if you attempt to use a variable before initializing it.

An object variable can also be set to `null`, which is a reserved word in Java. A null reference specifically indicates that a variable does not refer to an object.

Note that, although we’ve declared a String reference variable, no String object actually exists yet. The act of creating an object using the `new` operator is called instantiation. An object is said to be an instance of a particular class. To instantiate an object, we can use the `new` operator, which returns the address of the new object. The following two assignment statements give values to the two variables declared above:

```
num = 42;
name = new String("James Gosling");
```

After the `new` operator creates the object, a *constructor* is invoked to help set it up initially. A constructor is a special method that has the same name as the class. In this example, the parameter to the constructor is a string literal that specifies the characters that the string object will hold. After these assignments are executed, the variables can be depicted as:

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_142_0.png)

Since an object reference variable holds the address of the object, it can be thought of as a *pointer* to the location in memory where the object is held. We could show the numeric address, but the actual address value is irrelevant—what’s important is that the variable refers to a particular object.

After an object has been instantiated, we use the *dot operator* to access its methods. We’ve used the dot operator many times already, such as in calls to `System.out.println`. The dot operator is appended directly after the object reference, followed by the method being invoked. For example, to invoke the length method defined in the String class, we can use the dot operator on the name reference variable:

```
count = name.length()
```

The length method does not take any parameters, but the parentheses are still necessary to indicate that a method is being invoked. Some methods produce a value that is *returned* when the method completes. The purpose of the length method of the String class is to determine and return the length of the string (the number of characters it contains). In this example, the returned value is assigned to the variable count. For the string "James Gosling", the length method returns 13, which

### KEY CONCEPT

The `new` operator returns a reference to a newly created object.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_142_1.png)

**VideoNote**
Creating objects.

includes the space between the first and last names. Some methods do not return a value. Other String methods are discussed in the next section.

The act of declaring the object reference variable and creating the object itself can be combined into one step by initializing the variable in the declaration, just as we do with primitive types:

```
String title = new String("Java Software Solutions");
```

Even though they are not primitive types, character strings are so fundamental and so often used that Java defines string literals delimited by double quotation marks, as we’ve seen in various examples. This is a shortcut notation. Whenever a string literal appears, a String object is created automatically. Therefore the following declaration is valid:

```
String city = "London";
```

That is, for String objects, the explicit use of the new operator and the call to the constructor can be eliminated. In most cases, we will use this simplified syntax.

### Aliases

Because an object reference variable stores an address, a programmer must be careful when managing objects. First, let’s review the effect of assignment on primitive values. Suppose we have two integer variables, num1, initialized to 5, and num2, initialized to 12:

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_143_0.png)

In the following assignment statement, a copy of the value that is stored in num1 is stored in num2:

```
num2 = num1;
```

The original value of 12 in num2 is overwritten by the value 5. The variables num1 and num2 still refer to different locations in memory, and both of those locations now contain the value 5:

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_143_1.png)

Now consider the following object declarations:

```
String name1 = "Ada, Countess of Lovelace";
String name2 = "Grace Murray Hopper";
```

Initially, the references name1 and name2 refer to two different String objects:

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_144_0.png)

Now suppose the following assignment statement is executed, copying the value in name1 into name2:

```
name2 = name1;
```

This assignment works the same as the integer assignment—a copy of the value of name1 is stored in name2. But remember, object variables hold the address of an object, and it is the address that gets copied. Originally, the two references referred to different objects. After the assignment, both name1 and name2 contain the same address and therefore refer to the same object:

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_144_1.png)

The name1 and name2 reference variables are now aliases of each other because they are two names that refer to the same object. All references to the object originally referenced by name2 are now gone; that object cannot be used again in the program.

> KEY CONCEPT
> Multiple reference variables can refer to the same object.

One important implication of aliases is that when we use one reference to change an object, it is also changed for the other reference because there is really only one object. Aliases can produce undesirable effects unless they are managed carefully.

All interaction with an object occurs through a reference variable, so we can use an object only if we have a reference to it. When all references to an object are lost (perhaps by reassignment), that object can no longer contribute to the program. The program can no longer invoke its methods or use its variables. At this point the object is called garbage because it serves no useful purpose.

Java performs automatic garbage collection. When the last reference to an object is lost, the object becomes a candidate for garbage collection. Occasionally, behind the scenes, the Java environment executes a method that “collects” all the
