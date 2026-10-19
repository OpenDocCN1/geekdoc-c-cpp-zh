# A Set of CheckBoxes versus a Single ListBox

When do you use a set of ListBoxes rather than a ListBox to select multiple items from a list? Again, the guideline is to use a ListBox if the list is large and/or dynamic. A list is dynamic when the content of the list or the number of items in the list is likely to change. Thus, a ListBox is preferable to select multiple ingredients for a pizza, if the list of ingredients is dynamic.

# SelectionMode Property

To enable selection of multiple items, the SelectionMode property shown in Figure 6-21 needs to be set to MultiSimple or MultiExtended. The two settings are similar, except that the MultiExtended setting makes it easier to select a set of consecutive items using the shift key.

Figure 6-21: SelectionMode property of ListBox

![](bbox=[0.12, 0.33, 0.46, 0.49])

You already used ListBoxes to display output by adding text to the Items collection using the Add method, as in

```
lstDisplay.Items.Add ("Total Price: " + lblAmtDue.Text);
```

Similar to the ComboBox, the Add method adds a new item to the ListBox.

You also may add a list of items to the ListBox by storing the items in an array and then using a loop to add the items to the ListBox. For example, the following code stores a list of pizza toppings in an array named toppings, and adds them to a ListBox named lstToppings using a foreach loop.

```
string[] toppings = {"Pepperoni", "Sausage", "Onion", "Green Pepper", "Mushrooms", "Xtra Cheese", "Ham", "Anchovies"};
foreach (string topping in toppings) // Add toppings to ListBox
    lstToppings.Items.Add(topping);
```

To better understand the use of ListBoxes, let’s look at a pizza order form that lets the user select the size of pizza and the toppings, compute the total price, and display the total price and the toppings selected, as shown in Figure 6-22.