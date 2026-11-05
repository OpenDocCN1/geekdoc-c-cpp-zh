
## DATA

Table 10-6 lists the data field members needed for the `Order` class.

**TABLE 10-6 Order class data fields**

| Data description | Type | Identifier |
|---|---|---|
| Entree selection | `string` | `entree` |
| Water preference | `bool` | `waterSelection` |
| Drink preference | `string` | `drinkSelection` |
| Special requests | `string` | `specialRequest` |
| Entree price | `decimal` | `entreePrice` |
| Drink price | `decimal` | `drinkPrice` |

© 2013 Cengage Learning

A second `class`, `OrderGUI`, is created for the user interface. This `class` allows the user to select an entree and a drink, enter special requests, and request water. During design, a prototype is developed to determine which controls would be most appropriate for each selection.

Drink selections are constant and include "Milk", "Juice", "Soda", "Lemonade", "Tea", and "Coffee". Menu options may change occasionally and should not be statically placed on the graphical user interface. Current options are: "Chicken Salad", "Ham and Cheese", "Turkey", "Vegetable Wrap", "Tuna Salad", "Avocado and Cheese", "Club", "Peanut Butter & Jelly", "Grilled Cheese", and "Reuben".

## DESIGN A SOLUTION

The desired output is to produce a graphical user interface that allows a user to pick from a number of selections while placing an order. According to the problem definition, menu options should be available to clear the entire order or just part of it. After the items are selected, the total price and items selected should be displayed. These options can also appear as selections from the menu bar. Figure 10-25 shows a prototype of the form that illustrates the types of objects to be used and approximates their placement.

![](img/36e48639a06772bcb0fa1ea2525b33a3_688_0.png)

**FIGURE 10-25** Prototype for DinerGUI example

During design, determine which object types will be used to create the interface. The MenuStrip object was selected rather than a number of buttons so that the screen does not become cluttered. Menus offer the advantage of requiring less real estate on your screen. The entrees are displayed in a ListBox object. A scroll bar is automatically added when the number of entries exceeds the available space. The text selections for the ListBox object are loaded at run time to enable the diner manager to change the menu options in the class that deals with the business logic and keep that separate from the actual display.

Special requests are stored in a ComboBox object because it enables users either to choose from a list of options or to type a new entry. The water selection is a yes/no format; thus, a CheckBox object is used. RadioButton objects are used for drink selection. The buttons are placed in a GroupBox so that only one drink is selected.

Menu options include the following features:

### File

- Place Order—Displays the current order and the total price of the order
- Clear Order—Deselects all options on the GUI and sets all of the individual selections back to their defaults
- Display Order—Displays the current order
- Exit—Closes all windows and exits the application

### Edit

- **Entree**—Displays a message indicating that the entree selection is cleared, clears the entree selection, and deselects the selected entree
- **Drink**—Displays a message indicating that the drink selection is cleared, clears the drink selection, and deselects the selected drink
- **Special Request**—Displays a message indicating that the special request selection is cleared, clears the special request selection, and deselects the selected special request, or clears the text area if a value is typed

### Help

- **About**—Displays the name of the application along with the version number.

The Order class has both data and behavior characteristics that can be identified. The major actions or behaviors of an Order object are to set instance variables using the selection from the GUI objects, determine the individual prices, and determine the overall charge for the order. Class diagrams are used to help design and document these characteristics. Figure 10-26 shows the class diagrams for the DinerGUI example.

![](img/36e48639a06772bcb0fa1ea2525b33a3_690_0.png)

**FIGURE 10-26** Class diagrams for DinerGUI example

The class diagrams do not show the properties of the local variables that may be required for specific class methods. They do not show which event-handler methods are associated with particular objects.

> **NOTE** There are a number of ways to document collaboration between objects using an object-oriented approach. They include sequence, collaboration, state transition, and activity diagrams. Systems analysts often use these diagrams to design an application. Development of these types of models is beyond the scope of this book; however, you are encouraged to research and learn about them.

During design, it is important to develop algorithms showing the step-by-step process for the business logic of the application. Pseudocode for the Order class method is shown in Figure 10-27.

![](img/36e48639a06772bcb0fa1ea2525b33a3_691_0.png)

**FIGURE 10-27** Pseudocode for the Order class for the DinerGUI example

Many of the objects on the interface must be registered with event-handler methods. It is important that you spend time thinking about what should happen when each event is fired. Figures 10-28, 10-29, and 10-30 show pseudocode for the event handlers of the GUI class.

```
Form1_Load()
{Raised when the form is initially loaded}
    Create an Order object
    Fill the Entree Selections Listbox with entree items from the entree
        array in the order class

lstBoxEntree_SelectedIndexChanged()
{Raised when the ListBox object for the Entree selection is changed}
    Get the selection from the entree list box
    Assign the value to the entree instance of the order class

cmboBoxSpecial_SelectedIndexChanged()
{Raised when ComboBox object for the Special Requests is changed}
    Get the selection from the special requests combo box
    Assign the value to the special requests instance of the order class

cmboBoxSpecial_KeyPress()
{Raised when text typed in text area for ComboBox object for Special Requests}
    Retrieve the characters typed into the combo box for the special requests using
        the Text property
    Assign the value to the special requests instance of the order class

Drink_CheckedChanged()
{Raised when any RadioButton objects changed. NOTE: one method wired to all
 radio button objects}
    Using a nested if statement, determine which radio button is checked (use
        Checked property of the RadioButton class)
    Assign the text of the button to the drink selection instance of the order class
        [use Text property of the RadioButton class]

chkBoxWater_CheckedChanged()
{Raised when the CheckBox object for the Water is changed}
    Using Checked property of CheckBox class, determine if water checked
    If it is checked, assign true to waterSelection instance of the order class —
        otherwise assign false
```

**FIGURE 10-28** Pseudocode for RadioButton, CheckBox, ListBox, and ComboBox object event handlers

```
menuPlaceOrder_Click()
{Raised when the Place Order option under the File menu is clicked}
    Display a message showing information about the current order
        including what the total charges are
    Use properties and methods of the order class

menuDisplayOrder_Click()
{Raised when the Display Order option under the File menu is clicked}
    Display a message showing information about the current order.
    Use properties and methods of the order class

menuEditEntree_Click()
{Raised when the Edit Entree option under the Edit menu is clicked}
    Display a message indicating user should select a new entree
    Assign spaces to the entree instance of the order class
    Clear the selection of the list box [Use ClearSelected() method of the ListBox class]

menuEditSpecial_Click()
{Raised when the Edit Special Requests option under the Edit menu is clicked}
    Display a message indicating special request cleared
    Assign spaces to the special requests instance of the order class
    Clear the selection of the combo box [Use the SelectedIndex property of the
        ComboBox class]

menuAbout_Click()
{Raised when the About option under the Help menu is clicked}
    Display a message with the application name and version number

menuExit_Click()
{Raised when the Exit option under the File menu is clicked}
    Use the Exit() method of the Application class to close all windows
```

**FIGURE 10-29** Pseudocode for menu object event handlers
