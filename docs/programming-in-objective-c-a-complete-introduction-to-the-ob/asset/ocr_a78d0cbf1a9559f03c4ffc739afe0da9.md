Scope Revisited

# Static Variables

The example just shown goes against the notion of data encapsulation and good object-oriented programming techniques. However, you might need to work with variables whose values are shared across different method invocations. Even though it might make sense to make globalVar an instance variable in the Foo class, a better approach might be to "hide" it within the Foo class by restricting access to setter and getter methods defined for that class.

You now know that any variable defined outside a method is not only a global variable, but an external one as well. Many situations in you want to define a variable to be global but not external. In other words, you want to define a global variable to be local to a particular module (file). It would make sense to define a variable this way if no methods other than those contained inside a particular class needed access to the particular variable. You can accomplish this by defining the variable as static inside the file that contains the implementation for the particular class.

If made outside (or function), the following statement makes the value of globalVar accessible from any subsequent point in the file in which the definition appears, but not from methods or functions contained in other files:

```
static int globalVar;
```

Recall that class methods do not have access to instance variables (you might want to think about why that's the case again). However, you might want a class method to be capable of setting and accessing variables. A simple example is a class method that you want to keep track of the number of objects it has allocated. You would accomplish this task by setting a static variable inside the implementation file for the class. The allocation method could access this directly because it would not be an instance variable. The users of the class would not need to know about this variable. Because it defined as a static variable in the implementation file, its scope would be restricted to that file. Users would not have direct access to it, and the concept of data encapsulation would not be violated. You could write a method to retrieve the value of this variable if access was needed from outside the class.

Program 10.2 defines the Fraction class with the addition of two new methods. The alloc method allocates a new Fraction and keeps track of how many Fractions has allocated, whereas the count method returns count. Note that this latter is also a class method. It could have been implemented as an instance method as well, but it makes more sense to ask the class how many instances it has allocated instead of sending the message to a particular instance of the class.

These are the declarations for the two new class methods to be added to the Fraction.h header file:

```
+(Fraction *) allocF;
+(int) count;
```