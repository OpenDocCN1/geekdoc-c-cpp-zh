
The following code displays the form referred to by the variable newUserForm modally.

```
newUserForm.ShowDialog();
```

The Show method displays the form non-modally. That means the form appears and the user can interact with it or with the program's other forms.

The following code displays the form referred to by the variable newUserForm non-modally:

```
newUserForm.Show();
```

The UserForms example program shown in Figure 9-3 displays a main form with a New User button. Each time you click the button, the program displays a new MakeUserForm non-modally. Figure 9-3 shows the main form and two MakeUserForms.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_176_0.png)

FIGURE 9-3

The following code shows how the UserForms program displays a new MakeUserForm when you click its button:

```
private void newUserButton_Click(object sender, EventArgs e)
{
    MakeUserForm newUserForm;
    newUserForm = new MakeUserForm();
    newUserForm.Show();
}
```

The code declares a variable to refer to the form, creates the new form instance, and displays the instance non-modally.

Each time you click the button, the event handler executes again. Each time it runs, the event handler creates a new version of the variable named newUserForm, makes a new instance of the MakeUserForm, and displays that instance, so each time you click the button, you get a new form.

## FLOOD OF FORMS

In Windows Forms applications, the startup form's type Form1 is just like any other form type, so a program can make new instances of it. That means you can create more forms that look just like the startup form if you want.

Although all forms look about the same to the user, the startup form has a special position in the application. The program keeps running only as long as the startup form exists. If you close that form, all of the others close, too.

To avoid confusion, you should generally make the startup form look different from other forms so the user knows that it's special.

By default, the windows in WPF applications run independently so if you close the main window, the others keep running. If you want all of the windows to close when the main window does, execute the following statement when the program starts, for example, in the main window's Loaded event handler:

```
Application.Current.ShutdownMode = ShutdownMode.OnMainWindowClose;
```

## CONTROLLING REMOTE FORMS

When you create a new form and make a variable to refer to it, you can later use that variable to manipulate the form. There's just one catch: the techniques described so far don't keep the new form variable around long enough to be useful.

For example, the following code defines the newUserForm variable, makes it point to a new form, and displays the form:

```
private void newUserButton_Click(object sender, EventArgs e)
{
    MakeUserForm newUserForm;
    newUserForm = new MakeUserForm();
    newUserForm.Show();
}
```

When the program finishes executing the event handler, the event handler stops running. If the user clicks the button again, the event handler springs back into action.

Unfortunately, when the event handler stops running, it loses its grip on the newUserForm variable. The next time the event handler runs, it creates a new variable named newUserForm and works with that one.

This is bad for a program that wants to manipulate the new form later. Because the variable is gone, it can't refer to it so it can't manipulate the form.

The good news is that this is fairly easy to fix. If you move the variable's declaration out of the event handler, the variable exists throughout the program's lifetime. The event handler can make the variable point to a new form, and it can then use the variable later to manipulate that form.

The RemoteForm example program shown in Figure 9-4 uses the following main form code to manage a secondary ColorForm:

```
// The remote form we will manipulate.
ColorForm remoteColorForm;

// Create and display the remote form.
private void Form1_Load(object sender, EventArgs e)
{
    remoteColorForm = new ColorForm();
    remoteColorForm.Show();
}

// Make the color form red.
private void redButton_Click(object sender, EventArgs e)
{
    remoteColorForm.BackColor = Color.Red;
    remoteColorForm.ForeColor = Color.Pink;
}
```

The code starts by declaring the variable remoteColorForm outside of any event handler.

When the program displays the main form, its Load event handler creates and displays a new ColorForm.

When the user clicks the main form's Red button, its event handler changes the remote form's BackColor and ForeColor properties to red and pink, respectively. The startup form also contains green and blue buttons that have similar event handlers.

The remoteColorForm variable is declared outside of the event handlers, so the event handlers have access to it. The form's Load event handler initializes the variable and displays the remote form. The redButton_Click event handler uses it. Because the variable is declared outside of the event handlers, they can all use it. (Lesson 13 has more to say about when and where variables are available to the code.)

In addition to modifying a remote form's properties, you can change the properties of the controls on that form. You refer to a control by using the form variable, followed by a dot, followed by the control's name.

For example, the bold line in the following code accesses the form referred to by the remote ColorForm variable. It locates that form's messageLabel control and changes its Text property to "I'm red!":

```
private void btnRed_Click(object sender, EventArgs e)
{
    color_form.BackColor = Color.Red;
    color_form.ForeColor = Color.Pink;
    color_form.lblMessage.Text = "I'm red!";
}
```

There's one small catch to this technique: by default the controls on a form are private so the code in other forms can't manipulate them. You can easily fix this by setting a control's Modifiers property to Public, either in the Form Designer or in code. Now other forms can see the control and change its properties.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_178_0.png)

FIGURE 9-4

> NOTE Controls on a form are private to prevent other pieces of code from accidentally messing them up. By making a variable public, you remove this safeguard. In technical terms, you have weakened the form’s encapsulation—its ability to hide its internal details from the outside world.
> 
> In this case, you want to allow access to this label’s Text property so marking the label as public is reasonable. However, by making the label public you make all of its properties, methods, and events public, not just its Text property.
> 
> A more restrictive approach would be to add a public SetCaption method to the ColorForm. Then other code would call that method instead of setting the label’s text directly. You learn how to build those kinds of methods in Lesson 20.

## TRY IT

In this Try It, you create an application similar to the one shown in Figure 9-5. When the user clicks the main form’s buttons, the program displays the other forms non-modally.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_179_0.png)

FIGURE 9-5

### Lesson Requirements

In this lesson, you:

- Create the forms shown in Figure 9-5.
- Declare the form variables outside of any event handler.
- In the main form’s Load event handler, add code to create the form instances but don’t display the forms.
- Add code to the main form’s Button event handlers to display the corresponding secondary forms non-modally.

> NOTE You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

### Hints

- Normally every form appears in the taskbar. To avoid cluttering the taskbar with all of the secondary forms, set their ShowInTaskbar properties to False.

### Step-by-Step

- Create the forms shown in Figure 9-5.
  1. Create the main form.
     a. Start a new project. In the Properties window, expand the main form’s Font property and set its Size subproperty to 12.
     b. Add the Buttons. Center them as a group and set their Anchor properties to None.
  2. Create the GettingThereForm.
     a. Open the Project menu and select Add Windows Form. Enter the form type name GettingThereForm and click Add.
     b. Set the form’s ShowInTaskbar property to False.
     c. Add the Label, ListBox, and Buttons. Set the ListBox’s Anchor property to Top, Bottom, Left. Set the Buttons’ Anchor properties to Bottom, Right.
  3. Create the GettingAroundForm.
     a. Repeat step 2 for the GettingAroundForm.
  4. Create the LodgingForm.
     a. Repeat step 2 for the LodgingForm.
