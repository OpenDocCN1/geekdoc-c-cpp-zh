Because we already discussed the code in Chapter 9, we will not add the code for the two pages, but will focus on using tab control related features.

Next, we create the code to set focus to cboProdNumber, when the user selects Look Up Price page, and set focus to txtPrice, when the user selects Display Products page. This is done by coding the SelectedIndexChanged event of the TabControl, which is triggered when the user selects a tab page.

Step 2-6: Create the SelectedIndexChanged event handler of the TabControl (Select the TabControl by clicking the header area. Select events in Properties window and double click SelectedIndexChanged). Add the code from Figure 10-13 to the event handler.

# Figure 10-13: SelectedIndexChanged event handler of tabProductPrices

```
19 |
20 |     private void tabProductPrices_SelectedIndexChanged(object sender, EventArgs e)
21 |     {
22 |         if (tabProductPrices.SelectedIndex == 0)
23 |             cboProdNumber.Focus();
24 |         else if (tabProductPrices.SelectedIndex == 1)
25 |             txtPriceLimit.Focus();
26 |     }
```

Step 2-7: Run the form. Click the page Display Products. The TextBox should have the focus. Click the tab page Look up Price. The ComboBox should have the focus.

# Review Question

10.5 What is the difference between using multiple tab pages to do different tasks on a single form versus using multiple forms?

# Exercises

# Exercise 10-1

Modify ComputePrice_Click event procedure in the ListViewApp form so that the name of the selected show and the total price are displayed in the Label lblAmtDue, as in

Les Miserables: $140.00

# Exercise 10-2

Add a button on the ListViewApp form, and add the necessary code to the Click event handler to display all shows that start with the letter “M.” Display the names of such shows in a ListBox.