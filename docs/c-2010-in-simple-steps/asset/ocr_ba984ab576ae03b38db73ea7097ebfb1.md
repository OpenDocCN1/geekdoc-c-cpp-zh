![](bbox=[0.19, 0.12, 0.76, 0.38])

**Fig.C#-10.15**

+   17. Select Build → Build Solution from the menu bar to build the application.

+   18. Add the code given in Listing 10.11 to the Load event of Form1:

**Listing 10.11:** Showing Code to Add for the Form1_Load Event of the LINQtoSQL Application

```
```csharp
MyClassDataContext dc = new MyClassDataContext();
var query = dc.Products;
foreach (Product item in query)
{
    listView1.Items.Add(item.ProductID.ToString() + "  " + item.ProductName);
}
```
```

+   19. Press the F5 key to run the application.

The output of the LINQtoSQL application appears, as shown in Fig.C#-10.16:

![](bbox=[0.25, 0.64, 0.75, 0.845])

**Fig.C#-10.16**

In Fig.C#-10.16, the **ProductID** and the **ProductName** properties of all the products in the **Product** table have been displayed inside the ListView control in the **Form1** form.

Now, let's learn about LINQ to DataSet programming in the next section.