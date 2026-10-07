The code sets the ListBox.ItemsSource attribute to {Binding}. This rather odd syntax makes the control bind to whatever is in its DataContext. In this case, that means the StudentsDataTable.

The ListBox.ItemTemplate property element defines a template to use when displaying the items in the DataContext. In this example, it simply displays the FirstName and LastName fields separated by a space. (Note that the binding sources are simply the names of the database fields. There's plenty of hard stuff in WPF, but this is part easy.)

# # Displaying Student Details

When you click on an entry in the student list, the program displays the corresponding address and phone data in the mobile controls

Displaying the data in the TextBox is easy. Recall that the TextBoxes inherit the window's DataContext, so their DataContexts also map to the DataSet. All TextBox needs to be bound to the appropriate field in the StudentsDataTable.

The following code shows how the program makes its Street TextBox. The other TextBoxes are defined similarly.

```
<TextBox Grid.Row="0" Grid.Column="1" Margin="3"
Text={Binding Path=Tables[Students]/Street}"/>
```

When you click on a student in the list, the Tables[Students] DataTable's current item changes, and the Street TextBox displays the newly selected record's value.

The State ComboBox is trickier than the TextBox because the name of the field uses both the students and the State looks up. The following code shows how the program makes its State ComboBox:

```
<ComboBox Grid.Row="2" Grid.Column="1" Margin="3"
IsSynchronizedWithSelectedItem="True"
ItemsSource={Binding Path=Tables[States]}
DisplayMemberPath="State"
SelectedValue="State"
SelectedValue={Binding Path=Tables[Students]/State}/>
```

![](bbox=[0.08, 0.568, 0.14, 0.615])

![](bbox=[0.8, 0.695, 0.95, 0.715])

This control uses attributes to define the values that it represents and displays. The following-list describes these properties:

+   - ItemsSource — This gives the source that the control uses to build its list of choices. In this example, the control displays items from the StatesDataTable.

+   - DisplayMemberPath — This gives the path in the ItemsSource to the value that is displayed by the control. In this program, the ComboBox displays the state names, not their abbreviations, so DisplayMemberPath is StateName, the name of the field in the States DataTable that holds the state names.