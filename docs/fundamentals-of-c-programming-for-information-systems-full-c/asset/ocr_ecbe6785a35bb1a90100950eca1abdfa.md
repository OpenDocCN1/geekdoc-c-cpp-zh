# Tutorial 1: Looking Up Sales Data Using a List

Let’s look at an example, similar to the one discussed in Chapter 8, to look up sales data for a specified product number. The product number and sales for quarters 1–4 are read from the text file, Sales.txt, shown in Figure 9-1. The first data item in each row is the product number, which is followed by sales for quarters 1–4.

Figure 9-1: Sales.txt File

```
1033, 16, 32, 23, 40
1009, 144, 182, 169, 205
1014, 54, 49, 72, 63
1005, 38, 62, 55, 77
1001, 7, 9, 8, 15
1025, 98, 110, 105, 130
```

In Chapter 8, we used a 2-D array to store the data. In this application, you will use a generic List to store the data and to help find the total annual sales for a specified product. The product number is selected from a ComboBox, and the total sales displayed in a ListBox, as shown in Figure 9-2.

Figure 9-2: The GenericList form

![](bbox=[0.1, 0.48, 0.64, 0.65])

The coding for this form consists of three parts:

+   1. Create a List named sales.
+   2. Read each row from Sales.txt, split it and store it in a temporary array, and add the array to the List. Add the product number to the ComboBox. Both tasks are done in the Load event handler of the form.
+   3. When the user selects a product number from the ComboBox, find the corresponding item from the List. This is done in the SelectedIndexChanged event of the ComboBox.

# Creating the List

Step 1-1: Open the project Ch9_Collections from Tutorial_Starts folder. Open the form GenericList, shown in Figure 9-2.