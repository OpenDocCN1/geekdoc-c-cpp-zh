instantiates the `ReturnsSimpleString` delegate with the `EndStatement()` method as the argument.

# EXAMPLE 10.3

```
`ReturnsSimpleString saying3 = new ReturnsSimpleString(EndStatement);`
```

> **NOTE** The constructor for a `delegate` of the `delegate` class always takes just one parameter. This is because you are sending the name of a method for the constructor to reference.

Notice that the `EndStatement` argument does not include the parentheses, even though `EndStatement` is a method. A reference to the address of the method is sent as an argument. The address stored is the entry point in memory where the method begins when it is called.

# Using Delegates

After completing the instantiation in Example 10-3, the `delegate` identifier `saying3` references the `EndStatement()` method. Any use of `saying3()` calls the `EndStatement()` method. Example 10-4 illustrates this.

# EXAMPLE 10.4

```
`MessageBox.Show(saying3());`
```

A call to the `Show()` method of the `MessageBox` class calls the `delegate` instance, `saying3()`, which calls the `EndStatement()` method to display “in 10 years.” Calling the `EndStatement()` method in the `Show()` method produces the same output. This is a simple example, but illustrates how a `delegate` is used to call a method. Example 10-4 did not directly call the `EndStatement()` method; however, the statements from its body were those executed.

> **NOTE** Recall that you must add a reference to `System.Windows.Forms` in order to use the `MessageBox.Show()` method. You access the **Reference Manager** from the **Solution Explorer** window. To avoid fully qualifying the name with your program statements, you should also add another `using` statement,
> 
> `using System.Windows.Forms;`

The program in Example 10-5 illustrates defining a single `delegate` type, instantiating three `delegate` instances, and calling up the three delegates. Without looking closely,