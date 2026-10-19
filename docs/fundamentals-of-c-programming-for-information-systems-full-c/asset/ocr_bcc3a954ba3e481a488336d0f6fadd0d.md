# 6.7 Working with ListBoxes

![](bbox=[0.157, 0.073, 0.405, 0.239])

In this ListBox, Items[0] is the first item in the list (Pepperoni), but, SelectedItems[0] is the first selected item (Sausage).

Now, let’s look at the code to compute the price based on the size selected and the number of toppings. Figure 6-25 shows the code, except for the statements to compute the total price and display selected items, which are left for you to complete.

**Line 33** checks whether the user selected a size:

```csharp
if (rdbDefault.Checked == true),
```

If the default RadioButton is selected, that means none of the other RadioButtons that represent the size are selected.

**Line 40** calls the GetPrice method, shown in Figure 6-25, to get the base price of the pizza with no toppings and the cost per topping:

```csharp
GetPrice(ref basePrice, ref costPerTopping);
```

Note that the GetPrice method returns the two values using reference parameters. You may split this method to two value returning methods named BasePrice that returns the base price, and ToppingPrice that returns the cost per topping. The statement in line 40 will have to be replaced by two statements that invoke these methods.

+   **Step 1-26:** Add the missing code in line 43 to compute the total price (base price + cost per toppings x number of toppings).
+   
+   **Hint:** Count property of SelectedItems collection gives the number of selected items.
+   
+   Add the missing code in lines 54 and 55 to display the selected toppings in the ListBox, lstDisplay. You may use a foreach loop to access each item in the SelectedItems collection.