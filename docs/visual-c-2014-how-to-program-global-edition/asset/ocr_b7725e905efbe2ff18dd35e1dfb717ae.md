22.9 Address Book Case Study 973

```
// when the form loads, fill it with data from the database
private void Contacts_Load(object sender, EventArgs e)
{
    RefreshContacts(); // fill binding with data from database
}
```

**Fig. 22.42** | Calling RefreshContacts to fill the TextBox when the app loads.

# Method addressBindingNavigatorSaveItem_Click

MethodBindingNavigatorSaveItem_Click (Fig. 22.43) saves the changes to the database when the BindingNavigator's Save Data button is clicked.(Remember to enable this.) The Address database requires values for the first name, last name, phone number and e-mail. If a field is empty when you attempt to save, a DbEntityValidation exception occurs. We call RefreshContacts (line 72) after saving to re-sort the data and move back to the first element.

```
// Click event handler for the Save Button in
// BindingNavigator saves the changes to the data
private void addressBindingNavigatorSaveItem_Click(
    object sender, EventArgs e)
{
    Validate(); // validate input fields
    addressBindingSource.EndEdit(); // complete current edit, if any
    // try to save
    try {
        dbcontext.SaveChanges(); // write changes to database file
    } catch (DbEntityValidationException) {
        MessageBox.Show("Columns cannot be empty",
        "Entity Validation Exception");
    }
    RefreshContacts(); // change back to updated unfiltered data
}
```

**Fig. 22.43** | Saving changes to the database when the user clicks Save Data.

# Method FindButton_Click

MethodFindButton_Click (Fig. 22.44) uses LINQ query syntax (lines 81–85) to select only people whose last name start with the characters in the TextBox. The query sorts the results by name, first name. In LINQ to Entities, you cannot bind a LINQ query directly to a BindingSource.DataSource. So, line 88 gets the object's ToList to get a List representation of the filtered data and assigns the List to the BindingSource.DataSource. When you convert the query to a List, any changes to existing records in the DbContext are tracked by the DbContext—any records