# 596 Exploring Common XAML Controls

![](bbox=[0.265, 0.125, 0.5, 0.363])

Figure 2-18:
All the basic input controls.

# List-based controls

The List-based controls (referred to as Item controls) add an incredible amount of flexibility. As I discuss in Chapter 1 of this minibook, the list-based controls no longer have to rely on data tricks or other magic to make the content meaningful to the user who can be templated to show greater details about the Items contained.

Data binding is covered in great detail in Chapter 3 of this minibook, but the controls don't do unless you have something to show. The ComboBox, ListBox, and DataGrid control will be bound to a class that represents a Person. IList<Person>. See the Person class:

```
public class Person
{
    public string Name { get; set; }
    public string Address { get; set; }
    public string City { get; set; }
    public string State { get; set; }
    public string Zip { get; set; }
}
```

Here are the list-based controls:

+   * ComboBox and ListBox: The ListBox and the ComboBox in the sample below use a DataTemplate to create the contained items. The main difference between the two controls is that the ComboBox displays a single item with a drop-down selector (see Figure 2-18), and the ListBox shows the entire list of items up to the allowed space and scrolls the rest (see Figure 2-19). The ComboBox can be set up to allow selecting items that are not in the list, as well as editing the items in the list.