
- 16. Wiring an event handler to multiple objects involves:
  - a. using the same method to handle the events fired for more than one object
  - b. selecting the same object's property for each event-handler method
  - c. creating multiple methods that do the same task
  - d. naming the object’s Event property with an ampersand
  - e. none of the above

- 17. The GroupBox provides more functionality for which type of objects?
  - a. ComboBox
  - b. ListBox
  - c. CheckBox
  - d. RadioButton
  - e. TextBox

- 18. Click() events are the default event for which type of object?
  - a. Button
  - b. RadioButton
  - c. MenuItem
  - d. CheckBox
  - e. all of the above

- 19. Which statement could be used in C# to set a ListBox object’s selection mode to MultiExtended if you did not have Visual Studio’s Properties window available? The name for the ListBox object is lstBox1.
  - a. lstBox1.SelectionMode = SelectionMode.MultiExtended;
  - b. lstBox1 = MultiExtended;
  - c. SelectionMode = MultiExtended;
  - d. SelectionMode.MultiExtended;
  - e. all of the above

- 20. Which property can be set for a form to enable the Enter key to function like a mouse click for a selected Button object?
  - a. Enter
  - b. Button_Click
  - c. EnterKey
  - d. AcceptButton
  - e. AcceptKey

- 21. Describe what is required to make a menu option clickable or a check box functional.

- 22. When is a RadioButton control preferred over a CheckBox control? When is a ComboBox control preferred over a ListBox control?

- 23. How is a **delegate** related to an event?

- 24. For the following table, identify which properties can be used to set the given values for the controls.

| Desired action | Property |
| --- | --- |
| Get the selected item from a ComboBox object | |
| Change the label over a group box | |
| Arrange the items in a list box in ascending order | |
| Change the color of the text in a label | |
| Change the text that appears in the title bar of a form | |
| Associate a Main menu to a form | |

© 2013 Cengage Learning

- 25. From the following partial code listing, identify the name(s) of event-handler method(s) that would need to be written. To what object(s) are they wired?

```csharp
public class Question : System.Windows.Forms.Form
{
    private System.Windows.Forms.Label label1;
    private System.Windows.Forms.TextBox txtBActivity;
    private System.Windows.Forms.CheckBox ckbxSwim;
    private System.Windows.Forms.CheckBox ckbxSnorkel;
    private System.Windows.Forms.TextBox txtBResult;
    :   // Colon indicates items missing.

    private void InitializeComponent()
    {
        this.label1 = new System.Windows.Forms.Label();
        this.ckbxSwim = new System.Windows.Forms.CheckBox();
        this.ckbxSnorkel = new
            System.Windows.Forms.CheckBox();
        this.lstBxEvents.SelectedIndexChanged += new
            System.EventHandler
            (this.lstBxEvents_SelectedIndexChanged);

        :    // Colon indicates items missing.

        this.label2.Size = new
            System.Drawing.Size(120, 24);
        this.txtBxResult.Location = new
            System.Drawing.Point(-2, 240);
        this.btnNew.Text = "Add New One";
        this.btnNew.Click +=
            new System.EventHandler(this.btnNew_Click);
        this.AutoScaleBaseSize = new
            System.Drawing.Size(8, 19);
        this.BackColor = System.Drawing.Color.FromArgb
            (((System.Byte) (128)), ((System.Byte) (128)),
            ((System.Byte) (255)));
        this.ClientSize =
            System.Drawing.Size(292, 273);
        this.Controls.AddRange(
            new System.Windows.Forms.Control[]
                                 {this.btnNew,
                                  this.txtBxNewAct,
                                  this.label3,
                                  this.label1,
                                  this.txtBxResult,
                                  this.label2,
                                  this.lstBxEvents } );

        :    // Colon indicates items missing.
    }
}
```

## PROGRAMMING EXERCISES

- 1. Create a graphical user interface that allows the users to enter personal information such as their names, e-mail addresses, and phone numbers. Include a menu that provides a minimum of four features. The first displays the information entered by the user in a message box. The second clears the entries so that new values can be entered. The third menu option displays information about the application such as who developed it and what version it is. Another menu option closes the application. Be creative and be sure to produce an aesthetically pleasing design using options from the Format menu if you are using Visual Studio.

- 2. Create a Windows application that can be used as a sign-up sheet for ski equipment for the Flyers Sports Club. The club has ski equipment that it makes available to members at a minimal charge. In an attempt to determine what type of equipment members might need for an upcoming trip, they have asked you to design and implement an equipment-needs form. Include CheckBox objects that allow users to select the type of gear they will need to purchase for the trip. Include selections of snow gloves, skis, goggles, earmuffs, and other items you feel are appropriate. Include at least one picture image on your application. After all selections are made, display a message indicating what items have been selected. You will probably want to include menu options to display and clear the order for the next user. Also include an option that enables the user to exit the application.

- 3. Create a graphical user interface that can be used by a community group to enable youths to sign up for different sporting events. Include radio buttons with five different sport names. Only one of these should be selectable. Program your event-handler method so that a message is displayed with each selection of a different sport. For example, if one of the sports is skiing, the message might say, “Bring warm clothes!” Also include a PictureBox `object` on the form to display pictures of the sporting event. When the particular sport is selected, make the PictureBox visible. You can find free graphics on the Internet to use in your application. Hint: One way to associate a file to the PictureBox control is to Import an image from the Image property.

- 4. Create a Message Displayer that has one ComboBox `object` with a list of at least four of your favorite sayings. In your design, include the capability of letting users enter their own sayings. When a selection is made or a new entry is typed, display the selection on a Label `object` on your form. Add a menu to the application that includes at least the menu options of Format and Help. Under the Format selection, include options of Font and Color. Wire the Font and Color options to the Windows predefined Font and Color dialog boxes so that when their values are changed, the text in the Label `object` displaying the saying is changed.

- 5. Create an order form that allows bags to be purchased. There are six different types: full decorative, beaded, pirate design, fringed, leather, and plain. Create a ListBox `object` for the different styles. Include a ComboBox for quantity. Quantities up to 10 should be provided. After the user makes a selection, display a message indicating which selection was made. Include an option to clear selections. Provide appropriate error messages when selections are not made.

- 6. Add to the application in Exercise 5 by including a control that allows the user to determine the type of shipping they desire. Include a set of radio buttons that contain shipping options of overnight, three day, and standard. Add the price for each bag to the listbox selection as follows: full decorative—$50.00; beaded—$45.00; pirate design—$40.00; fringed—$25.00; leather—$80.00; and plain—$20.00. Display the items sorted. Using methods of the string class, retrieve and use the price from the listbox. The shipping charges are based on the total purchase. The following percentages are used: overnight—10%; three day—7%; and standard—5%. Display in a message box the shipping charge along with the selection, quantity, and total cost.
