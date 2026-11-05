
```csharp
using System;
using System.Windows.Forms;

public class AccountEditForm : System.Windows.Forms.Form
{
    private Label nameLabel;
    private TextBox nameTextBox;
    private Button finishButton;

    IAccount account;

    public AccountEditForm(IAccount inAccount)
    {
        this.account = inAccount;

        this.nameLabel = new Label();
        this.nameLabel.Text = "Name";
        this.nameLabel.Top = 50;
        this.nameLabel.Left = 0;
        this.Controls.Add(this.nameLabel);

        this.nameTextBox = new TextBox();
        this.nameTextBox.Top = 50;
        this.nameTextBox.Left = 100;
        this.nameTextBox.Text = this.account.GetName();
        this.Controls.Add(this.nameTextBox);

        this.finishButton = new Button();
        this.finishButton.Top = 80;
        this.finishButton.Left = 100;
        this.finishButton.Text = "Finished";
        this.finishButton.Click += new System.EventHandler(finishButton_Click);
        this.Controls.Add(this.finishButton);
    }

    private void finishButton_Click(object sender, System.EventArgs e)
    {
        string reply = account.ValidateName(nameTextBox.Text);
        if ( reply.Length > 0 )
        {
            System.Windows.Forms.MessageBox.Show(reply);
            return;
        }
        this.account.SetName( nameTextBox.Text );
        this.Dispose();
    }
}
```

The form will be passed a reference to the account instance which is being edited. It then gets the properties out of the form and displays them for editing. When the user presses the finish button the form must make sure that the name is valid. If it is, the name of the account class should be set and the form must then dispose of itself.

This code is the Windows equivalent of the AccountEditTextUI method that we created previously. All the form components are created in the constructor for the form.

The finishButton_Click method gets the name out of the text box and validates it. If the name is invalid it uses a static method in the Windows Forms system to pop up a message box and report an error:

![](img/c654620410a83b786d7196f7d03d0886_159_0.png)

This is how we tell the user that the name is not correct. There are a number of different forms of this Show method which you can use to get different forms of message box and even add extra buttons to it.

## Disposing of forms

The Dispose method is used when we have finished with this form and we want to get rid of it. All the components on the form are destroyed and the form is removed from the screen. Once we have disposed of a form we can never use it again. We will need to create a new form instead.

The Dispose method is important because we must explicitly say when we have finished with the instance. If we just removed a reference to the form object it will still remain in memory until the garbage collector gets around to noticing it.

## Using the Edit form

To use the edit form we must first construct an account instance. We then pass a reference to the account into the constructor of an AccountEditForm.

```csharp
Account a = new Account();
a.SetName("Rob");
AccountEditForm edit = new AccountEditForm(a);
edit.ShowDialog();
Console.WriteLine(" Name value : " + a.GetName());
```

This piece of test code creates an account and sets the name of the account holder to Rob. It then creates an edit form and uses that to edit the name value in the account.

## Modal Editing

The call of ShowDialog in the edit form is modal. This means that while the form is on the screen the rest of the system is paused. In the code above the WriteLine is not performed until after the edit form has been closed.

## Visual Studio and Form Editing

The Visual Studio application can take care of all the hard work of creating forms and adding components to them. It will also look after the creation of delegates for button actions. However, it is important to remember that although it automates a lot of the actions that I have performed by hand above, the fundamental principles that drive the forms it produces are exactly the same.

## Programmer's Point: Customers really care about the user interface

If there is one part of the system which the customer is guaranteed to have strong opinions about it is the user interface. The design of this should start at the very beginning of the product and be refined as it goes. Never, ever assume you know that the user interface should work in a particular way. I have had to spend more time re-working user interface code than just about any other part of the system. The good news is that with something like Visual Studio it is very easy to produce quite realistic looking prototypes of the front end of a system. These can then be shown to the customer (get them signed off even) to establish that you are doing the right thing.

## 5.5 Using Delegates

Events and delegates are a very important part of C#. Therefore you should read this text carefully and make sure you understand what is going on.

Delegates are useful because they let us manipulate references to methods. We can manage which particular method is going to be called in a given situation in terms of a lump of data which we can move around.

Delegates are an important part of how events are managed in a C# program. Events are things that happen which our program may need to respond to. They include stuff like people pressing buttons in our user interface, clocks going tick and messages arriving via the network. In each case we need to tell the system what to do when the event occurs. The way that C# does this is by allowing us to create instances of delegate classes which we give the event generators. When the event occurs (this is sometimes called the event "firing") the method referred to by the event is called to deliver the message.

I call a delegate "A way of telling a piece of program what to do when something happens". A posh description would have the form:

> A delegate is a type safe reference to a method in a class.

### 5.5.1 Type safe delegates

The phrase type safe in this context means that if the method accepts two integer parameters and returns a string, the delegate for that method will have exactly the same appearance and cannot be used in any other way. This word is used to distinguish a delegate from things like pointers which are used in more primitive languages like C.

In C you can create pointers to methods, but the C environment does not know (or even care) what the methods really look like. This means that you can call them in the wrong way and cause your program to explode. Don't worry about this too much. Just remember that delegates are safe to use.

### Using a Delegate

As an example, consider the calculation of fees in our bank. The bank will have a number of different methods which do this, depending on the type of customer and the status of that customer. It might want to have a way in which a program can choose which fee calculation method to use as it runs.

We have seen that things like overriding let us create methods which are specific to a particular type of object, for example we provided a custom withdrawFunds for the BabyAccount class which only lets us draw out a limited amount of cash. These techniques are very useful, but they are hard wired into the code that I write. Once I've compiled the class, the methods in it cannot change.

A delegate is a "stand in" for a method. If you call the delegate it calls the method it presently refers to. This means I can use it as a kind of method selector. A delegate type is created like this:

```csharp
public delegate decimal CalculateFee (decimal balance);
```

Note that I've not created any delegates yet. I've just told the compiler what the delegate type CalculateFee looks like. This delegate can stand in for a method which accepts a single decimal parameter (the balance on the account) and returns a decimal value (the amount we are going to charge the customer). An example of a method we might want to use with this delegate you could consider is this one:
