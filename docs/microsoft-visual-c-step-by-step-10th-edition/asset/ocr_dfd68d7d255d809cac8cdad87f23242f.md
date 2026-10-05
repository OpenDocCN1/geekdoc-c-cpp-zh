When a variable can be accessed at a particular location in a program, the variable is said to be in scope at that location. The calculatedValue variable has method scope; it can be accessed throughout the calculateClick method but not outside that method. You can also define variables with different scope—for example, you can define a variable outside a method but within a class, and a variable can be accessed by any method within that class. Such a variable is said to have class scope.

To put it may, the scope of a variable is simply the region of the program in which that variable is usable. Scope applies to methods as well as variables. Scope of an identifier (of a variable or method) is linked to the location of the declaration that introduces the identifier in the program, as you will learn next.

# Defining local scope

The opening and closing braces that form the body of a method define the scope of the method. Any variables you declare inside the body of a method are scoped to that method; they disappear when the method ends and can be accessed only by code running in that method. These variables are called local variables because they are local to the method in which they are declared; they are not in scope in any other method.

The scope of local variables means that you cannot use them to share information between methods. Consider this example:

Click here to view code image

```
class Example
{
    void firstMethod()
    {
        int myVar;
        ...
    }

    void anotherMethod()
    {
        myVar = 42; // error - variable not in scope
        ...
    }
}
```