# Chapter 22

```
// If the cell content is not null and the year is less than 2000
// Set the background to red
if(e->Value != nullptr && safe_cast<DateTime^>(e->Value)->Year < 2000)
{
    e->CellStyle->BackColor = Color::Red;
    e->FormattingApplied = false;      // We did not format the data
}
}
```

If you rebuild the example, you should now see all the cells highlighted.

You should now have a good idea of how you can implement event handler for a DataGridView control. There are a multitude of other events, so you have huge scope for doing many more things dynamically to customize the control to your application needs.

# Using Bound Mode

In bound mode, the source of the data that a DataGridView control displays is specified by the value of its DataSource property, which in general you can set to be any ref class object of a type that implements any of the following interfaces:

| Interface | Description |
|---|---|
| System::Collections::IList | A class that implements this interface represents a collection of objects that can be accessed through a single index. All C++/CLI one-dimensional arrays implement this interface, so a DataGridView object can use any one-dimensional array as the source of the data that is displayed. The IList interface inherits the members of the ICollection and IEnumerable interface classes that are defined in the System::Collections namespace. |
| System::ComponentModel::IListSource | A class that implements this interface makes the data available as a list that is an IList object. The list can contain objects that also implement the IList interface. |
| System::ComponentModel::IBindingList | This interface class extends the IList interface class to allow more complex data binding situations to be accommodated. |
| System::ComponentModel::IBindingListView | Adds sorting and filtering capabilities to the IBindingList interface. The BindingSource class that you’ll meet a little later in this chapter defines a control that implements this interface. |