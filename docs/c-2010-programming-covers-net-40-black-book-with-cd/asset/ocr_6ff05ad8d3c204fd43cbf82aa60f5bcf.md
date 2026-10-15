int data type and assigned the value 100 to it. The values assigned to these constants do not change throughout the execution of the entire program. If you try to assign another value to a constant and compile the program, will display an error stating that the left-hand side of an assignment must be a variable, property, or indexer.

Constants and variables can be accessed only within the specific scope. The scope of a variable determines the region within the program where the variable can be accessed and referenced. The scope is of two types, block and class. When you declare a variable within a code block, the variable gets a local scope or a block scope therefore, it is known as local variable. The variable having a local scope cannot be used outside a code block in which it is declared. If you declare a variable outside the code block (or before defining the Main() method), the variable is said to have a class scope and known as global variable. Such a variable can be used throughout the program. Listing 2.1 shows an example to illustrate the scope of variables:

# Listing 2.1: Showing an Example for the Scope of Variables

```
class Scope
{
public void Scope1()
{
    int i = 0;
    i = i + 1;
}
public void Scope2()
{
    Console.WriteLine(i);
}
}
```

In Listing 2.1, variable i is declared and initialized within the Scope1() method. Now when you try to access variable i outside the Scope1() method, a compile-time error occurs stating that the name i does not exist in the current context. This is due to the reason that the i variable is a local variable of the Scope1() method and can be accessed only within this method.

The class scope uses the access modifiers, such as private and public, to specify the scope of a variable. The private keyword makes a variable local to a class and specifies that the variable cannot be used and accessed outside the class in which it is declared. You can make the variable global in the class by declaring it as public. This makes the variable to be used in any class within the entire program. Listing 2.2 shows an example to understand the scope of a class:

# Listing 2.2: Showing an Example for the Scope of a Class

```
public class LocalScope1
{
    int i = 0;
}
public class LocalScope2
{
    void Scope()
    {
        Console.WriteLine(i);
    }
}
```

In Listing 2.2, you can see that the variable i is declared in class LocalScope1. If you attempt to access i outside the LocalScope1 class, the same compile-time error occurs stating that the name i does not exist in the current context. The error has occurred because the i variable is declared in the LocalScope1 class and is private by default. Therefore the variable cannot be accessed in the LocalScope2 class.

C# supports a rich and varied selection of data types, from built-in types, such as integers or strings, to user defined types, such as enumerations, structures, and classes. The C# language provides a rich set of built-in data types. When dealing with these data types, you must remember the following points:

+   - All variables, whether user-defined or intrinsic (built-in), can be used as objects anywhere in a program
+   - All variables in a program are automatically initialized to default values by the system when they are declared