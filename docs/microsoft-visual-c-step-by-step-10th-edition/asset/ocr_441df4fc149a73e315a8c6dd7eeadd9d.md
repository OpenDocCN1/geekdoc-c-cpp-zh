This works if Mammal has a public default constructor. However, not all classes have a public default constructor. For example, remember that the compiler generates a default constructor only if you don't write any nondefault constructors. In this case, forgetting to call the correct base-class constructor results in a compile-time error.

# Assigning classes

Previous examples in this book show how to declare a variable by using a class and how to use the new keyword to create an object. There are also examples of how the type-checking rules of C# prevent you from assigning an object of one type to a variable declared as a different type. For example, given the definitions of the Mammal, Horse, and Whale classes shown here, the code that follows these definitions is illegal:

Click here to view code image

```
class Mammal
{
    ...
}

class Horse : Mammal
{
    ...
}

class Whale : Mammal
{
    ...
}

Horse myHorse = new Horse(...);
Wale myWhale = myHorse; // error - different types
```

However, it's possible to refer to an object from a variable of a different type as long as the type used is a class that is higher up the inheritance hierarchy. So, the following statements are legal:

Click here to view code image