I've spent some time now explaining why finalizers are not a good solution. But yet, you still need to free resources. You address these issues using the IDisposable interface and the standard dispose pattern. (See Item 17 later in this chapter).

To close, remember that a managed environment, where the Garbage Collector takes the responsibility for memory management, is a big plus: Memory leaks and a host of other pointer-related problems are no longer your problem. Nonmemory resources force you to create finalizers to ensure proper cleanup of those nonmemory resources. Finalizers can have a serious impact on the performance of your program, but you must write them to avoid resource leaks. Implementing and using the IDisposable interface avoids the performance drain on the Garbage Collector that finalizers introduce. The next section moves on to the specific items that will help you create programs that use this environment more effectively.

# Item 12: Prefer Member Initializers to Assignment Statements

Classes often have more than one constructor. Over time, it's easy for the member variables and the constructors to get out of sync. The best way to make sure this doesn't happen is to initialize variables where you declare them instead of in the body of every constructor. You should utilize the initializer syntax for both static and instance variables.

Constructing member variables when you declare that variable is natural in C#. Just initialize the variable when you declare it:

```
public class MyClass
{
    // declare the collection, and initialize it.
    private List<string> labels = new List<string>();
}
```

Regardless of the number of constructors you eventually add to the MyClass type, labels will be initialized properly. The compiler generates code at the beginning of each constructor to execute all the initializers you have defined for your instance member variables. When you add a new constructor, labels get initialized. Similarly, if you add a new member variable, you do not need to add initialization code to every constructor; initializing the variable where you define it is sufficient. Equally important, the initializers are added to the compiler-generated default constructor.