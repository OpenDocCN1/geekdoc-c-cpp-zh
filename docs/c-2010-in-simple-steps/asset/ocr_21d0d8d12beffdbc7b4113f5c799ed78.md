```
{
    new Order {key = 1, OrderNumber = "Number 1"},
    new Order {key = 2, OrderNumber = "Number 2"},
    new Order {key = 3, OrderNumber = "Number 3"},
    new Order {key = 4, OrderNumber = "Number 4"},
    new Order {key = 5, OrderNumber = "Number 5"}
};
var q = from c in customers
join o in orders on c.Key equals o.Key
select new { c.Name, o.OrderNumber };
foreach (var i in q)
{
    listView1.Items.Add(i.OrderNumber.ToString() + " " + i.Name);
}
}
```

In Listing 10.6, the Customer data and the Order data are joined by using the Join clause.

+   8. Press the F5 key to run the application.
+   9. Click the Join Data button, as shown in Fig.C#-10.7:

![](bbox=[0.35, 0.35, 0.6, 0.52])

Fig.C#-10.7

Now, let's discuss the grouping operators.

# The Grouping Operators

The grouping operators in LINQ are used to arrange data into groups so that the elements in each group share a common attribute. The group clause is the grouping operator used in LINQ. This clause returns a sequence of the IGrouping<TKey, TElement> objects that contain zero or more items matching the key value for the group.

Now, let's create a Windows application, GroupingOperator, where you can use the group clause. For this, perform the following steps:

+   1. Repeat steps 1 to 3 shown earlier while creating the LINQQuery application in the Explaining LINQ Queries and their Execution section of this chapter.
+   2. Enter GroupingOperator in the Name text box to specify the name of the application, and enter an appropriate location for the application in the Location combo box.
+   3. Click the OK button. The GroupingOperator application is created.
+   4. Add a ListView control and a Button control to Form1 and change the Text property of the button1 to Group Data.
+   5. Change the Location and Size property of the ListView control to 12, 12 and 260, 164, respectively.
+   6. Click the Smart Tag of the ListView control and select the Tile option from the View drop-down list, as shown in the JoinOperator example.