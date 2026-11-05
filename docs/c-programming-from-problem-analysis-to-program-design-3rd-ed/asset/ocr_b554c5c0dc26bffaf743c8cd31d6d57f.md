# ### Example 10-3

```
```csharp
ReturnsSimpleString saying3 = new ReturnsSimpleString(EndStatement);
```
```

![](bbox=[0.173, 0.178, 0.235, 0.228])

The constructor for a **delegate** of the **delegate class** always takes just one parameter. This is because you are sending the name of a method for the constructor to reference.

Notice that the `EndStatement` argument does not include the parentheses, even though `EndStatement` is a method. A reference to the address of the method is sent as an argument. The address stored is the entry point in memory where the method begins when it is called.

# ## Using Delegates

After completing the instantiation in Example 10-3, the **delegate** identifier `saying3` references the `EndStatement()` method. Any use of `saying3()` calls the `EndStatement()` method. Example 10-4 illustrates this.

# ### Example 10-4

```
```csharp
MessageBox.Show(saying3());
```
```

A call to the `Show()` method of the MessageBox class calls the **delegate** instance, `saying3()`, which calls the `EndStatement()` method to display “in 10 years.” Calling the `EndStatement()` method in the `Show()` method produces the same output. This is a simple example, but illustrates how a **delegate** is used to call a method. Example 10-4 did not directly call the `EndStatement()` method; however, the statements from its body were those executed.

The program in Example 10-5 illustrates defining a single **delegate** type, instantiating three **delegate** instances, and calling up the three delegates. Without looking closely, the arguments to the `Show()` method appear to be normal method calls. In reality, the methods are called through the delegates. Notice that the **delegate** instance name and a set of parentheses form the argument to the `Show()` method.

# ### Example 10-5

```
```csharp
// DelegateExample.cs          Author: Doyle
// After defining a delegate class, three delegate
// instances are instantiated. Delegates are
// used as arguments for the Show() method.
using System;
using System.Windows.Forms;
```
```