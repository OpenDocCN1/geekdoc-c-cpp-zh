
```csharp
// Event handler that gets raised when the edit menu
// is clicked to change the entree.
private void menuEditEntree_Click
                 (object sender, System.EventArgs e)
{
    MessageBox.Show("Please select a new Entree");
    newOrder.Entree = "";
    this.lstBxEntree.ClearSelected( );
}

// Event handler that gets raised when the edit menu
// is clicked to change the drink.
private void menuEditDrink_Click
                 (object sender, System.EventArgs e)
{
    MessageBox.Show("Please select a new Drink");
    newOrder.DrinkSelection = "";
    this.ClearDrinks( );
}

// Clears selections for all drink radio buttons.
public void ClearDrinks( )
{
    this.radMilk.Checked = false;
    this.radJuice.Checked = false;
    this.radSoda.Checked = false;
    this.radLemon.Checked = false;
    this.radTea.Checked = false;
    this.radCoffee.Checked = false;
}

// Clears all selections so that a new order
// can be placed. Resets the Order object back
// to its default values.
private void menuClearOrder_Click
                 (object sender, System.EventArgs e)
{
    this.lstBxEntree.ClearSelected( );
    this.ckBxWater.Checked = false;
    this.cmboSpecial.SelectedIndex = -1;
    this.cmboSpecial.Text = "";
    this.ClearDrinks( );
    newOrder.DrinkSelection = "";
    newOrder.Entree = "";
    newOrder.SpecialRequest = "";
    newOrder.WaterSelection = false;
}

// Displays the values for the current instance of
// Order object members.
private void menuPlaceOrder_Click
                (object sender, System.EventArgs e)
{
    MessageBox.Show(newOrder.Entree + "\n" +
        newOrder.SpecialRequest + "\n" +
        newOrder.DrinkSelection + "\n" +
        newOrder.GetWaiterSelection() +
        "\n\n" + newOrder,
        "Placed Order");
}

// Event handler that gets raised when the edit menu
// is clicked to change the special request.
private void menuEditSpecial_Click
                (object sender, System.EventArgs e)
{
    MessageBox.Show("Special Request cleared.");
    newOrder.SpecialRequest = "";
    this.cmboSpecial.SelectedIndex = -1;
    this.cmboSpecial.Text = "";
    newOrder.SpecialRequest = "";
}

// Event handler that gets raised when the Help
// menu is clicked to show the About message.
private void menuAbout_Click
                (object sender, System.EventArgs e)
{
    MessageBox.Show("Student Union - " +
                    "Diner by the Valley" +
                    "\n\nVersion 1.0");
}

// Event handler that gets raised when
// Exit is clicked.
private void menuExit_Click
                (object sender, System.EventArgs e)
{
    Application.Exit();
}
}
}
```

Figure 10-31 shows the original user interface with the File menu selections. Notice that a new icon is used in the title bar. The icon was added by setting the Icon property for the OrderGUI form.

![](img/36e48639a06772bcb0fa1ea2525b33a3_714_0.png)

**FIGURE 10-31** Interface showing menu selections

> **NOTE**
>
> Any file that ends with an .ico extension can be used as the icon for the application.
> Many sources on the Internet contain free graphics. They are easily added to your Windows applications.

All that is required to add pictures to a form is to instantiate an **object** of the **PictureBox** class. If you are using Visual Studio, drag the PictureBox control **object** to your form. Set the **Image** property to the desired picture.

> **NOTE**
>
> You can select graphic file types such as *.bmp, *.gif, *.jpeg, *.jpg, *.png, and *.ico or metafile types such as *.emf or *.wmf for the **Image** property. Store the image in the `bin\debug` subdirectory of the current project.

The Form **object** also has a BackgroundImage property that can be set to display a picture on the background. To have a picture in the background, using Visual Studio select the form and then use the **Properties** window to select the BackgroundImage property. Browse to a location that contains a bitmap or metafile.

When the form is loaded, the `OrderGUI_Load` event is raised. At that time, an **object** of the **Order** class is instantiated. Using the entree array of the **Order** class, the list box is filled. With each click on the form, a different event is fired. Figure 10-32 shows the message displayed after several options were selected, including the **Place Order** menu option.

![](img/36e48639a06772bcb0fa1ea2525b33a3_715_0.png)

**FIGURE 10-32** Message displayed from Place Order menu option

The ComboBox object allows special requests to be typed. Any new selections set new values for the instance of the Order class. When users type values in the text area of the ComboBox object, the `KeyPress()` event is fired. Figure 10-33 illustrates a typed entry for the ComboBox object. The `MessageBox.Show()` method is used to display messages from the menu options. Figure 10-33 is displayed from the **File**, **Display Order** option.

![](img/36e48639a06772bcb0fa1ea2525b33a3_715_1.png)

**FIGURE 10-33** Message displayed from Current Order menu option

When events are raised from the **Edit** menu, the event-handler methods display a message indicating the selections are being cleared. Then, the control on the form GUI is cleared and the Order instance data member is set back to its default value. Figure 10-34 shows the result of selecting the **Edit**, **Special Requests** menu option.

![](img/36e48639a06772bcb0fa1ea2525b33a3_716_0.png)

**FIGURE 10-34** Special Requests click event fired

Firing the **Clear Order** menu option (shown in Figure 10-35) deselects all entries on the form and resets the Order instance data members to their default values. The Windows application is in a Run state until the Exit menu option is fired or the **Close** button is clicked.

![](img/36e48639a06772bcb0fa1ea2525b33a3_717_0.png)

**FIGURE 10-35** Clear Order click event fired

A number of event-handler methods are wired to objects for this application. Table 10-8 lists the event-handler methods and their associated objects. These are all instantiated in the OrderGUI class.

**TABLE 10-8** OrderGUI events

| Event-handler method | Class | Object |
| --- | --- | --- |
| `ckBxWater_CheckedChanged` | `CheckBox` | `ckBxWater` |
| `cmboSpecial_KeyPress` | `ComboBox` | `cmboSpecial` |
| `cmboSpecial_SelectedIndexChanged` | `ComboBox` | `cmboSpecial` |
| `Drink_CheckedChanged` | `RadioButton` | `radTea`, `radSoda`, `radLemon`, `radMilk`, `radCoffee`, `radJuice` |
| `OrderGUI_Load` | `OrderGUI` | `this` |
| `lstBxEntree_SelectedIndexChanged` | `ListBox` | `lstBxEntree` |
| `menuAbout_Click` | `ToolStripMenuItem` | `menuAbout` |
| `menuClearOrder_Click` | `ToolStripMenuItem` | `menuClearOrder` |
| `menuDisplayOrder_Click` | `ToolStripMenuItem` | `menuDisplayOrder` |
| `menuEditDrink_Click` | `ToolStripMenuItem` | `menuEditDrink` |
| `menuEditEntree_Click` | `ToolStripMenuItem` | `menuEditEntree` |
| `menuEditSpecial_Click` | `ToolStripMenuItem` | `menuEditSpecial` |
| `menuExit_Click` | `ToolStripMenuItem` | `menuExit` |
| `menuPlaceOrder_Click` | `ToolStripMenuItem` | `menuPlaceOrder` |

## Coding Standards

As was discussed in the previous chapter, it is important to follow a consistent naming standard for controls added to a Windows form. Before you register events, such as button click events, name the associated control. Then when you register the event handler using Visual Studio, the code that is automatically generated uses the control's identifier as part of the identifier for the method. Naming the control first will make your code more readable and help reduce errors.

## Resources

Additional sites you might want to explore:

- Visual Studio 2012 – Getting Started Tutorials – http://msdn.microsoft.com/en-us/library/dd492171.aspx
- Visual C# Windows Forms Tutorials http://visualcsharptutorials.com/windows-forms
- Delegates and Events in C#/.NET – http://www.akadia.com/services/dotnet_delegates_and_events.html
- C# Programmers Reference: Delegates Tutorial – http://msdn.microsoft.com/en-us/library/aa288459(VS.71).aspx
- Geekpedia - ListBox and CheckedListBox – http://www.geekpedia.com/tutorial40_ListBox-and-CheckedListBox.html
- CodeGuru - Create a Dynamic Menu Using C# – http://www.codeguru.com/csharp/csharp/cs_misc/designtechniques/article.php/c15661/

## QUICK REVIEW

1. Delegates are special types of .NET classes whose instances store references (addresses) to methods.
2. A declaration for a delegate looks more like a method declaration than a class definition. Every delegate type has a signature, which may include zero or more parameters. The signature indicates what method signatures must look like if they are to be referenced by the delegate.
3. Multicast delegates are wired to multiple methods, all of which are executed, one after the other, when an event is raised.
