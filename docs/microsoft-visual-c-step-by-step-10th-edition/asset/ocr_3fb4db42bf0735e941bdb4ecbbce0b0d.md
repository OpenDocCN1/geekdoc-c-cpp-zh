Inheritance is a powerful feature that makes it possible for you to extend the functionality of a class by creating a new class that derives from it. However, sometimes using inheritance is not the most appropriate mechanism for adding new behaviors, especially if you need to quickly extend a type without affecting existing code.

For example, suppose you want to add a new feature to the int type, such as a method named Negate that returns the negative equivalent value that an integer currently contains. (Of course, you could use the unary minus operator [-] to perform the same task, but bear me...) One way to achieve this is to define a new type named Int32 that inherits from System.Int32 (int is an alias for System.Int32) and adds the Negate method:

Click here to view image

```
class Neg32 : System.Int32
{
    public int Negate()
    {
        ...
    }
}
```

The theory is that Neg32 will inherit all the functionality associated with the System.Int32 type in addition to the Negate method. There are two reasons why you might not want to follow this approach, however:

+   - This method applies only to the Neg32 type. If you want to use it with existing variables in your code, you must change the definition of every int variable to the Neg32 type.

+   - The System.Int32 type is actually a structure, not a class, and you cannot use inheritance with structures.

This is where extension methods become very useful. Using extension method, you can extend an existing type (a class or structure) with additional static methods. These static methods become immediately available to your code in any statements that refer to data of the type being extended.

You define an extension method in a static class and specify the type to which the method applies as the first parameter to the method, along with the this keyword. Here's an example showing how you can implement the Negate extension method for the int type: