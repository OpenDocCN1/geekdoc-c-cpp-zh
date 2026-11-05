
### Example 10-3

```csharp
ReturnsSimpleString saying3 = new ReturnsSimpleString(EndStatement);
```

![](img/e33ae760e23d89eac66541252ad65de8_577_0.png)

The constructor for a **delegate** of the **delegate class** always takes just one parameter. This is because you are sending the name of a method for the constructor to reference.

Notice that the `EndStatement` argument does not include the parentheses, even though `EndStatement` is a method. A reference to the address of the method is sent as an argument. The address stored is the entry point in memory where the method begins when it is called.

## Using Delegates

After completing the instantiation in Example 10-3, the **delegate** identifier `saying3` references the `EndStatement()` method. Any use of `saying3()` calls the `EndStatement()` method. Example 10-4 illustrates this.

### Example 10-4

```csharp
MessageBox.Show(saying3());
```

A call to the `Show()` method of the MessageBox class calls the **delegate** instance, `saying3()`, which calls the `EndStatement()` method to display “in 10 years.” Calling the `EndStatement()` method in the `Show()` method produces the same output. This is a simple example, but illustrates how a **delegate** is used to call a method. Example 10-4 did not directly call the `EndStatement()` method; however, the statements from its body were those executed.

The program in Example 10-5 illustrates defining a single **delegate** type, instantiating three **delegate** instances, and calling up the three delegates. Without looking closely, the arguments to the `Show()` method appear to be normal method calls. In reality, the methods are called through the delegates. Notice that the **delegate** instance name and a set of parentheses form the argument to the `Show()` method.

### Example 10-5

```csharp
// DelegateExample.cs          Author: Doyle
// After defining a delegate class, three delegate
// instances are instantiated. Delegates are
// used as arguments for the Show() method.
using System;
using System.Windows.Forms;

namespace DelegateExample
{
    delegate string ReturnsSimpleString( );
    class DelegateExample
    {
        static void Main ( )
        {
            int age = 18;
            ReturnsSimpleString saying1 =
                new ReturnsSimpleString(AHeading);
            ReturnsSimpleString saying2 =
                new ReturnsSimpleString(
                    (age + 10).ToString);
            ReturnsSimpleString saying3 =
                new ReturnsSimpleString(EndStatement);
            MessageBox.Show(saying1( ) +
                saying2( ) + saying3( ));
        }
        // Method that returns a string.
        static string AHeading( )
        {
            return "Your age will be ";
        }

        // Method that returns a string.
        static string EndStatement( )
        {
            return " in 10 years.";
        }
    }
}
```

The signatures for the methods and the `delegate class` match.

> Notice that the second instance of the `delegate`, `saying2`, is associated with a .NET predefined method of the `object` class. Remember that the `ToString( )` method takes no arguments and returns a `string`. Its signature matches the `ReturnsSimpleString( )` delegate.

The methods are said to be wrapped by the `delegate`. When the `delegate` is used, it passes a method, instead of data, as an argument to the `Show( )` method. Figure 10-1 shows the output produced when you execute the program from Example 10-5.

![](img/e33ae760e23d89eac66541252ad65de8_579_0.png)

**Figure 10-1** Output from delegate example

It is possible to have the **delegate wrap** more than one method, so that when a **delegate** is used, multiple methods are called, one after the other. This type of **delegate** is called a **multicast delegate**. The += and -= operators are used to add or remove methods to and from the **delegate** chain or invocation list. One requirement for multicast delegates is that the **return** type be **void**.

The real advantage or power of the **delegate**, however, is that the same **delegate** can call different methods during run time. When the program is compiled, the method or methods that will be called are not determined. This is why delegates work so well in an event-driven arena, where you do not know, for example, which event occurs first or which control gets attention first.

![](img/e33ae760e23d89eac66541252ad65de8_579_1.png)

If the console application template is selected as the type of application, you will see the black command window displayed in the background when you run the program. Remove it by first selecting the project in the **Solution Explorer** window and then select the icon representing Properties in the **Solution Explorer** window. Using the pull-down menu, select **Windows Application** as the **Output type**.

## Relationship of Delegates to Events

Think about what the word *delegate* means in the English language; you associate it with something or someone who acts as a bridge between two things. A delegate serves as a bridge with event-driven applications. It acts as an intermediary between objects that are raising or triggering an event, and the object that captures the event and responds to it. You can think of events as special forms of delegates in C#, because they enable you to place a reference to event-handler methods inside a *delegate*. After this reference is made, or the event is registered, the *delegate* is used to call the event-handler method when an event, such as a button click, is fired.

This behind-the-scenes plumbing is dealt with in C# without much programmer intervention. In fact, if you are using Visual Studio, all of the code, with the exception of the statements that appear in the event-handler methods, is automatically generated for you when you identify the events about which your program must receive notification.

## EVENT HANDLING IN C#

In Chapter 9, you wrote program statements for methods that were executed when a button was clicked. The Form Designer in Visual Studio did much of the work for you. Two things were added to your program when you double-clicked on a Button control object during design (or selected its click event from the Event list in the Properties window). First, the button click event was registered as being of interest, and second, an event-handler method heading was generated. This process is called event wiring. You associate a method in your program to an event, such as the user clicking the button. Then, this method is automatically called when the event occurs.

Now that you know about delegates, if you examine the Windows Forms Designer generated code region, which is generated by Visual Studio, you understand how the delegate is used to register the event. The code that appears in Example 10-6 is generated when you double-click a button in the Form Designer. System.EventHandler is a delegate type. This code associates the two methods, button1_Click( ) and button2_Click( ), with that delegate.

### Example 10-6

```csharp
this.button1.Click += new
    System.EventHandler(this.button1_Click);
this.button2.Click += new
    System.EventHandler(this.button2_Click);
```

> The keyword this is added to all code generated by Visual Studio. This keyword is used to indicate the current instance of a class. For the Windows applications you are developing in this chapter, think of this as the current instance of the form. So, for Example 10-6, when you notice this.button1.Click, you should mentally associate that with “the current form’s” button1.Click.

When Visual Studio adds the event-handler method heading, the body of the method is empty. You add the program statements to the body of the method indicating what actions to perform when the button is clicked. Example 10-7 shows the event-handler method for button1_Click.

### Example 10-7

```csharp
private void button1_Click(object sender, System.EventArgs e)
{
}
```

> These methods have a return type of void with two parameters; the delegate System.EventHandler( ) has a return type of void and two parameters. Their signatures match.
