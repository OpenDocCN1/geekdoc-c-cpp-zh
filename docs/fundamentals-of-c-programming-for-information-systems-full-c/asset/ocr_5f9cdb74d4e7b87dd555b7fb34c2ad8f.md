Line 20: The variable, displayInvestment, is declared at the class level so that it can be used in multiple methods.

Lines 26–28: Creates an instance of the DisplayInvestment form and opens it.

Lines 31–53: Computes investment values and displays them in the ListBox lstDisplay. This is essentially the same as the code we discussed in Chapter 4, except that the ListBox is on the form DisplayInvestment.

So, the statements in lines 38, 40 and 52 that display results in the ListBox use the variable displayInvestment to access the ListBox, as in

```
displayInvestment.lstDisplay.Items.Add(string.Format(formatCode,
    "Year", "Investment Value"));
```

# Tutorial 1: Multi-form Financial Planning Application

Let’s develop a multi-form fianancial planning application.

+   Step 1-1: Open the project, project Ch11_MultiFormApps1.
+   Step 1-2: Open the form, FinancialPlanner.
+   Step 1-3: Add the missing code in lines 20, 26 and 28 from Figure 11-4, to open the DisplayInvestment form.
+   Uncomment the statements in lines 38, 40 and 52, which write data into the DisplayInvestment form.
+   Step 1-4: Open Program.cs and change the startup form to FinancialPlanner. Run the form and test the code.
+   Step 1-5: Click the “How Long” button multiple times, each time with a different set of input data for yearly investment, growth rate and target amount. Note that every time you click the button, a new instance of the DisplayInvestment form is displayed.

# Creating Multiple Instances of the Same Form

As observed in Step 1-5, every time you click the “How Long” button, the statements in line 26 and 28,

```
displayInvestment = new DisplayInvestment();
displayInvestment.Show();
```

will create and open a new instance of the DisplayInvestment form. This allows you to simultaneously display investment values for different sets of input data.

# Hiding versus Closing a Form

You may hide a form without closing it. Hiding a form keeps the form and its properties and settings in memory. You don’t lose the data entered/displayed in controls at runtime. It just is not visible.

You hide a form using the Hide method of the form. For example,

```
this.Hide()
```

hides the current form.

The following code within the FinancialPlanner form hides an instance of the DisplayInvestment form:

```
displayInvestment.Hide();
```