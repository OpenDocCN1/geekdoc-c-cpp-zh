```
```text
menuClearOrder_Click()
{Raised when the Clear Order option under the File menu is clicked}
    Clear the selection of the list box [use ClearSelected() method of the listbox class] for the entree.
    Uncheck the check box for Water [set Checked property to false]
    Clear the selection and text from combo box [set the SelectedIndex property to -1]
    Clear the selections from the radio buttons by calling ClearDrinks() to uncheck all button selections
    Set the drinkSelection, entree, and special request instances of the order class to blanks
    Set the waterSelection instance of the order class to false

menuEditDrink_Click()
{Raised when the Edit Drink option under the Edit menu is clicked}
    Display a message indicating user should select a new drink
    Assign spaces to the drink instance of the order class
    Clear the selections from the radio buttons by calling ClearDrinks() to uncheck all button selections

menuEditEntree_Click()
{Raised when the Edit Entree option under the Edit menu is clicked}
    Display a message indicating user should select a new entrée
    Assign spaces to the entrée instance of the order class
    Clear the selection of the list box [Use ClearSelected() method of the listbox class]

ClearDrinks()
{Method created to avoid duplicating code – called from menuEditDrink_Click() and menuEditEntree_Click()}
    Uncheck all radio button selections [set Checked property to false]
```
```

FIGURE 10-30  Pseudocode for menu object event handlers and the ClearDrinks( ) method

You should always desk check your design. Develop your test plan for testing the application. Walk through your logic, and ensure you have accounted for each of the events that need to be programmed. Reread the problem specification and ensure you have taken all issues into consideration.

After you implement your design, be sure to run and test your application using your test plan.

# CODE THE SOLUTION

After completing the design and verifying the algorithm’s correctness, you translate the design into source code. For this application, two separate files, one for each class, are created. Form Designer can generate much of the code for the user interface class. Control object’s property values are as shown in Table 10-7.