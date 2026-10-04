
# Events

The final important topic that needs to be discussed in this chapter is events. ASP.NET is an event-driven environment, which means that code can execute based on certain events that occur in your application. Events are raised by objects in the application and handled by others. Many objects in the .NET Framework are capable of raising an event, and you can add your own events to classes that you write.

To handle an event raised by an object, you need to write an event handler, which is basically a normal method with a special signature. You can wire up this event handler to the event using event wiring, as VS takes care of writing that code for you most of the time. When an object, such as a control in a web page, raises an event, it may have the need to pass additional information to the event handler, to inform about relevant data that caused or influenced the event. You can send this information using an event arguments class, which is the SystemEventArgs class or any class that inherits it.

To see all these fits together, consider what happens when you click a button in a web page. When you click it, the client-side button in the browser causes a postback. At the server, the button control sees it was clicked in the browser and then raises its Click event. It says then "Oh, look, everyone. Interested, there are some details." Usually, the code that is interested in the button's Click event is your own page, which needs to have an event handler to handle the click. You can create an event handler for the Button by double-clicking it in the designer, or you can wire it up using Markup View as seen in Chapter 4. Alternatively, you can double-click the relevant event on Events of the Properties Grid. You open this by clicking the button with the lightning bolt on the toolbar of the Properties Grid (see Figure 5-9).

If you double-click the event handler in Design View or the event name in the Properties Grid, VS writes the code for the handler for you. The following snippet shows the handler for a Button control's Click event in VB.NET and C#:

VB.NET

```
Protected Sub Button1_Click(sender As Object, e As EventArgs) _
    Handles Button1.Click
End Sub
```

C#

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
}
```

In the VB.NET example, you see a standard method with some arguments, followed by Handles Button1.Click. This is the event wiring code that hooks up the Button control's Click event to the Button1_Click method. Now, whenever the button is clicked, the code inside Button1_Click is executed.

![](img/9e033e3b9560597824f8b22941d6d8bb_227_0.png)

The C version doesn't have this Handles keyword. Instead, with C# you'll find that VS has added the following bold code to the Button control in the markup of the page:

```xml
<asp:Button ID="Button" runat="server" Text="Button" OnClick="Button1_Click" />
```

With this piece of markup, the compiler generates the necessary code to link the Button_Click method to the Click event of the button. At run time you'll see the exact same behavior: when you click the button, the code in Button_Click is executed. If you write up an entry in Markup View in VB.NET, you get the same behavior as in C#: names like Handles keyword is omitted from the Code Behind there's already an On handler in Markup View.

You can also see that this Button_Click event handler has two parameters: an Object sender and an EventArgs class e. This is a standard .NET naming scheme and is followed by all objects that generate event. The sender contains a reference to the object that triggered the event, Button in this enables you to find out who triggered an event in case you used multiple events to the same event.

The second parameter is an instance of the EventArgs class and supplies additional arguments to the event. With a button's click, there is no additional data to submit, so the plain and empty EventArgs class is used. However, in later chapters (for example, Chapter 9, which deals with data-driven Web Forms), you see some examples of classes that fire with richer information.

With concepts of event, you will have to come to the end of the section on object orientation. This section should have familiarized you with the most important terms used in object-oriented programming. You will see practical examples of these concepts in the remainder of this book.

# PRACTICAL TIPS ON PROGRAMMING

The following list presents practical tips for programming:

- Always define your variables meaningful names. For simple loop counters you can use i, although loopCount probably describes the purpose of the variable much better. Don't prefix variables with the word var. All variables are variables, so adding var noise to your code. Consider useful names such as _firstName and _categoryId as opposed to strName, varFirstName or names like FirstName and Person for properties and classes, respectively.

- Experiment and experiment. Even so more to learn how to program is actually doing it. Just type in some code and hit Ctrl+F5 to see how the code behaves. The compiler will tell you at when you something is wrong, providing you with useful hints on how to fix it. Don't be afraid to mess anything up; just keep trying until the code does what you want it to. If you can't make your code work, check out Chapter 18, which deals with debugging. You'll find useful tips to locate and fix many of the errors that may occur in your code.

- When writing functions or subroutines, try to minimize the number of lines of code. Usually, more than 40 or 50 lines of code are a sign of bad design. Even if a method is used only once, keeping a chunk of code in a separate method can significantly increase the readability and organization of code.

- When writing comments in your code, try to describe the general purpose of the code instead of explaining obvious statements. For example, this comment (seen many times in real) is completely useless and only adds noise:
```vb
Dim loopCount As Integer = 0 ' Declare loopCount and initialize it to zero
```

# SUMMARY

Although programming can get really complex, the basics that you need to understand are relatively easy to grasp. The fun thing about programming is that you don't have to be an expert to make useful programs. You can start with a simple Hello World example and work from there, each time expanding your view on code a little.

This chapter covered two main topics. First, you got an introduction to programming in .NET using either C# or VB.NET. You saw what data types and variables are and learned about operators, decision making, and loops. You also saw how to write organized code using functions, subs, and namespaces and how to add comments to your code.

The final section of this chapter dealt with object orientation. Though object orientation in itself is a very large subject, the basics are easy to pick up. In this chapter you learned the basic elements of OO programming: classes, methods, properties, and constructors.

In the next chapter, which deals with creating consistent-looking web pages, you see inheritance when you create a BasePage class that serves as the parent for the Code Behind classes in the Planet Wrox project.

# EXERCISES

- 1. Considering the fact that the oldest person in the world lived to be 122, what's the best numeric data type to store a person's age? Bonus points if you come up with an even better alternative to store someone's age.

- 2. What does the following code do?

VB.NET
```vb
DeleteButton.Visible = Not DeleteButton.Visible
```

#
```csharp
DeleteButton.Visible = !DeleteButton.Visible;
```
