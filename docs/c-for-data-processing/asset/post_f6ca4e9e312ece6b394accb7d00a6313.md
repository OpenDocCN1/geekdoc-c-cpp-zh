
This is my account editor class. At the moment it can only edit the name, but I will add other edit methods later. The class keeps track of the account it is editing. I pass it a reference to this account when I construct it. I would use the name editor as follows:

```csharp
CustomerAccount a = new CustomerAccount("Rob", 50);
AccountEditTextUI edit = new AccountEditTextUI(a);
edit.EditName();
```

This code creates an instance of a customer account. It then creates an editor object and asks it to edit the name of that account.

Note that the editor class is passed a reference to the Account interface, not a reference to the account class. This means that anything which behaves like an account can be edited using this class. Note also that the editor remembers the account class that is being edited so that when I call EditName it can work on that reference.

### Programmer's Point: Get used to passing references around

It is important that you get used to the idea of passing references between methods. If I want to "give" a class something to work on I will do this by calling a method in that class and passing the reference as a parameter to this method. You will use this technique when you create different editing forms.

## 5.3.2 A Text Based Edit System

We now have a single method in our editor class which can be used to edit the name of a bank account. What we really want is a menu system which takes a command from the user and performs that function:

```text
Editing account for Pete
    Enter name to edit name
    Enter pay to pay in funds
    Enter draw to draw out funds
    Enter exit to exit program
Enter command :
```

The user types in the name of the command that is required and then the program selects that function. My edit class contains a method which does this:

This is my edit method which repeatedly reads commands and dispatches them to the appropriate method. I've extended the account class to manage the account balance and added edit methods which pay in funds and withdraw them. Note that I trim the command string and convert it to lower case before using it to drive the switch construction which selects the command.

The edit method is passed a reference to the account which is being edited. It then passes that reference to the service methods which will do the actual work.

```csharp
public void DoEdit (CustomerAccount account)
{
    string command;
    do
    {
        Console.WriteLine ( "Editing account for {0}", account.GetName() );
        Console.WriteLine ( "    Enter name to edit name" );
        Console.WriteLine ( "    Enter pay to pay in funds" );
        Console.WriteLine ( "    Enter draw to draw out funds" );
        Console.WriteLine ( "    Enter exit to exit program" );
        Console.Write ( "Enter command : " );
        command = Console.ReadLine();
        command = command.Trim();
        command = command.ToLower();
        switch ( command )
        {
            case "name":
                EditName(account);
                break;
            case "pay":
                PayInFunds(account);
                break;
            case "draw":
                WithDrawFunds(account);
                break;
        }
    } while ( command != "exit" );
}
```

### Programmer's Point: Every Message Counts

You should remember that every time your program sends text to the user you may have a problem with language. The menu for my bank account edit method sample code prints out text which is hard wired to English. In a properly written program this would be managed in terms of message numbers to make it easier to change the text which is output.

As a general rule in a production system you should never write out straight text to your user (this includes the names of commands that the user might type in). Everything should be managed in terms of message numbers. The only exception to this is the situation where the customer has assured you that the program will only ever be written for use in a particular language. The C# libraries contain a set of resources which help you manage the internationalization of your programs.

### BANK NOTES: MORE THAN ONE USER INTERFACE

The bank may have a whole range of requirements for editing account details. These will range from an operator in a call centre, an operator on a dial up terminal, a customer on a mobile phone and a customer at a cash machine. I hope that you can see that the only way we can manage all these different ways of interacting with the bank account is to separate the business object (the account itself) from the input/output behaviour.

Note that we never do things like allow the user interface code to decide what constitutes a valid name. This question is not the responsibility of the front end. The only thing that can decide on the validity of a name is the account object itself. The user interface must always work on the basis that it will use the business object to perform this kind of validation.

## 5.4 A Graphical User Interface

It should come as no surprise that a graphical user interface on the screen is represented by objects. When we are dealing with windows on the screen our program is actually calling methods in the objects to make them do things like change size and colour.

### 5.4.1 Creating a Form

If I want a form on the screen for the user to interact with, I need to create an instance of an object to do this for me. The object that I create is a Form. This class can be found in the System.Windows.Forms namespace. I can create an instance of this class and ask it to do things for me.

```csharp
using System.Windows.Forms;

class FormDemo
{
    public static void Main ()
    {
        Form f = new Form();
        f.ShowDialog();
    }
}
```

The Form class provides a method called ShowDialog. This asks the form to show itself and pause the program until the form is closed. If I run the program above the following appears on the screen:

![](img/c654620410a83b786d7196f7d03d0886_152_0.png)

When the window is closed with the red button, it disappears and the program ends.

### Adding Components to a Form

A form is a container. It can contain a number of graphical components which are used to build the user interface. We must create the components and add them to the form to make our user interface. For example, to add a label to the form we can do the following:

```csharp
using System.Windows.Forms;

class FormDemo
{
    public static void Main ()
    {
        Form f = new Form();
        Label title = new Label();
        title.Text="Hello";
        f.Controls.Add(title);
        f.ShowDialog();
    }
}
```

This creates a label, sets the text property of the label to "Hello" and then adds it to the controls which are contained by the frame. The result of this code is a form which looks like this:

![](img/c654620410a83b786d7196f7d03d0886_152_1.png)

I can fiddle with the properties of a component to move it around on the screen and do lots of interesting things:

```csharp
using System.Windows.Forms;
using System.Drawing;

class FormsDemo
{
    public static void Main ()
    {
        Form f = new Form();
        Label title = new Label ();
        title.Text="hello";
        title.Top=50;
        title.Left=50;
        title.ForeColor = Color.Red;
        title.BackColor = Color.Yellow;
        f.Controls.Add(title);
        f.ShowDialog();
    }
}
```

The position on the screen is given in pixels (a pixel being an individual dot on the screen). The origin (i.e. the pixel at 0,0) is in the top left hand corner of the screen.

The Color class is found in the System.Drawing namespace. It provides a whole set of static colour values and also lets you create your own colours by setting the intensity of the red, green and blue components. The program above would display a form as below:

![](img/c654620410a83b786d7196f7d03d0886_153_0.png)

By adding a number of labels on the form and positioning them appropriately we can start to build up a user interface.

### Editing Text with a TextBox Component

Displaying labels is all very well, but what I want to do is provide a way that the name text can be edited. The Windows Forms library provides a TextBox component which is used for this. This is a component just like a label, but it provides text edit behaviour. I can set the text property of the TextBox to the text I want to have edited. The user can then enter text into the textbox and modify it. I can then read the text property back when I want the updated value.

The TextBox gives me a great deal of functionality for very little effort on my part. It lets the user cut and paste text in and out of the box using the Windows clipboard. It lets the user type in huge amounts of text and scrolls the text around to make it fit in the box. In short, it behaves like every text field you've ever used in a Windows screen. This is because it is actually the same thing as every text field you've ever used.

I can create and use a TextBox in my program as follows:
