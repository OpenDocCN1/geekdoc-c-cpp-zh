# CHAPTER 5 CONTENT CONTROLS

The following XAML code creates the GroupBox shown in Figure 5-16. The GroupBox contains the program's Label and TextBox controls. To save space, they are not in the following code:

```
<GroupBox HorizontalAlignment="Stretch" VerticalAlignment="Stretch"
Header="Customer Information" Margin="8" BorderBrush="#FFD5DFES">
<Grid Margin="5" />
</GroupBox>

>
```

![](bbox=[0.095, 0.262, 0.335, 0.396])

UseGroupBox

Figure 5-16

# ListView

The ListView displays a set of data items in several layouts. We can define new custom layouts for the control, but perhaps the most common standard layout is the grid-like view shown in Figure 5-17.

![](bbox=[0.395, 0.446, 0.858, 0.579])

Figure 5-17

Displaying a set of data in a grid with resizable columns may sometimes be useful, the real power of the ListView is its ability to display data from a data source such as a database or a list of objects.

Data binding is covered in greater detail in Chapter 18; this section covers only a few of the basics so you can see how ListView works.

The C# code shows how the UseListView example defines its BookInfo class. The class's constructor simply initializes the new object's four properties: Author, Title, Year, and Price. Since all are implemented in a very similar way, only the code for the Author property is shown here.

```
public class BookInfo
{
    // Initialize a new object's fields.
    public BookInfo(string new_Author, string new_Title,
        string new_Year, string new_Price)
}
```