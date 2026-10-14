
## Note

The code that validates the EmailAddress and Phone properties performs regular expression matching by using the Regex class defined in the System.Text.RegularExpressions namespace. To use this class, you define a regular expression in a Regex object that specifies the pattern that the data should match, and then you invoke the IsMatch method of the Regex object with the data that you need to validate. For more information about regular expressions and the Regex class, see “The Regular Expression Object Model” on the Microsoft website at http://msdn.microsoft.com/library/30wbz966.

- **CopyCustomer** The purpose of this method is to create a shallow copy of a Customer object. You will use it when you create the EditCustomer command to make a copy of the original data of a customer before it is changed. If the user decides to discard the changes, the original data can simply be copied back from the copy made by this method.

- 4. In Solution Explorer, expand the Customers project and double-click the ViewModel.cs file to open it in the Code and Text Editor window.

- 5. The definition of the ServerUrl string variable near the top of the ViewModel class looks like this:

Click here to view code image

```
private const string ServerUrl =
"http://<webappname>.azurewebsites.net/";
```

Change this string and replace the text <webappname> with the name of the web service that you created in earlier in this chapter.

- 6. In the ViewModel.cs file, find the Methods For Fetching And Updating Data region (expand this region if necessary). In this region, above the ValidateCustomer method, create the Add method shown here:

Click here to view code image

```
// Create a new (empty) customer
// and put the form into Adding mode
private void Add()
{
    Customer newCustomer = new Customer { CustomerID = 0 };
    this.customers.Insert(currentCustomer, newCustomer);
    this.IsAdding = true;
    this.OnPropertyChanged(nameof(Current));
}
```

This method creates a new Customer object. It is empty apart from the

*CustomerID* property, which is temporarily set to 0 for display purposes. The real value for this property is generated when the customer is saved to the database, as described earlier. The customer is added to the customers list (the view uses data binding to display the data in this list), the ViewModel is placed in Adding mode, and the *PropertyChanged* event is raised to indicate that the *Current* customer has changed.

7. Add the following *Command* variable shown in bold to the list at the start of the *ViewModel* class:

Click here to view code image

```
public class ViewModel : INotifyPropertyChanged
{
    ...
    public Command LastCustomer { get; private set; }
    public Command AddCustomer { get; private set; }
    ...
}
```

8. In the *ViewModel* constructor, instantiate the *AddCustomer* command as shown here in bold:

Click here to view code image

```
public ViewModel()
{
    ...
    this.LastCustomer = new Command(this.Last, ...);
    this.AddCustomer = new Command(this.Add,
        () => { return this.CanBrowse; });
    ...
}
```

This code references the *Add* method that you just created. The command is enabled if the ViewModel has a connection to the web service and is in Browsing mode (the *AddCustomer* command will not be enabled if the ViewModel is already in Adding mode).

9. After the *Add* method in the Methods For Fetching And Updating Data region, create a private *Customer* variable called *oldCustomer* and define another method called *Edit*:

Click here to view code image

```
// Edit the current customer
// - save the existing details of the customer
//   and put the form into Editing mode
private Customer oldCustomer;

private void Edit ()
{
    this.oldCustomer = new Customer();
    this.CopyCustomer(this.Current, this.oldCustomer);
```

```
this.IsEditing = true;
}
```

This method copies the details of the Current customer to the oldCustomer variable and puts the ViewModel into Editing mode. In this mode, the user can change the details of the current customer. If the user subsequently decides to discard these changes, the original data can be copied back from the oldCustomer variable.

10. Add the following Command variable shown in bold to the list at the start of the ViewModel class:

Click here to view code image

```
public class ViewModel : INotifyPropertyChanged
{
    ...
    public Command AddCustomer { get; private set; }
    public Command EditCustomer { get; private set; }
    ...
}
```

11. In the ViewModel constructor, instantiate the EditCustomer command as shown in bold in the following code:

Click here to view code image

```
public ViewModel()
{
    ...
    this.AddCustomer = new Command(this.Add, ...);
    this.EditCustomer = new Command(this.Edit,
        () => { return this.CanBrowse; });
    ...
}
```

This code is similar to the statement for the AddCustomer command, except that it references the Edit method.

12. After the Edit method in the Methods For Fetching And Updating Data region, add a method named Discard to the ViewModel class, as shown here:

Click here to view code image

```
// Discard changes made while in Adding or Editing mode
// and return the form to Browsing mode
private void Discard ()
{
    // If the user was adding a new customer, then remove it
    if (this.IsAdding)
    {
        this.customers.Remove(this.Current);
        this.OnPropertyChanged(nameof(Current));
    }
```

```
// If the user was editing an existing customer,
// then restore the saved details
if (this.IsEditing)
{
    this.CopyCustomer(this.oldCustomer, this.Current);
}

this.IsBrowsing = true;
}
```

The purpose of this method is to enable the user to discard any changes made when the ViewModel is in Adding or Editing mode. If the ViewModel is in Adding mode, the current customer is removed from the list (this is the new customer created by the Add method), and the PropertyChanged event is raised to indicate that the current customer in the customers list has changed. If the ViewModel is in Editing mode, the original details in the oldCustomer variable are copied back to the currently displayed customer. Finally, the ViewModel is returned to Browsing mode.

13. Add the DiscardChanges Command variable to the list at the start of the ViewModel class, and update the constructor to instantiate this command, as shown here in bold:

Click here to view code image

```
public class ViewModel : INotifyPropertyChanged
{
    ...
    public Command EditCustomer { get; private set; }
    public Command DiscardChanges { get; private set; }
    ...
    public ViewModel()
    {
        ...
        this.EditCustomer = new Command(this.Edit, ...);
        this.DiscardChanges = new Command(this.Discard,
            () => { return this.CanSaveOrDiscardChanges; });
    }
    ...
}
```

Notice that the DiscardChanges command is enabled only if the CanSaveOrDiscardChanges property is true, the ViewModel has a connection to the web service, and the ViewModel is in Adding or Editing mode.

14. In the Methods For Fetching And Updating Data region, after the Discard method, add one more method, named SaveAsync, as shown in the code that follows. This method should be marked with the async modifier.

Click here to view code image

```
// Save the new or updated customer back to the web service
// and return the form to Browsing mode
private async void SaveAsync()
{
    // Validate the details of the Customer
    if (this.ValidateCustomer(this.Current))
    {
        // Only continue if the customer details are valid
        this.IsBusy = true;
        try
        {
            // Convert the current customer into HTTP request
            // format with a JSON payload
            var serializedData =
            JsonConvert.SerializeObject(this.Current);
            StringContent content =
                new StringContent(serializedData, Encoding.UTF8,
            "text/json");

            // If the user is adding a new customer,
            // send an HTTP POST request to the web service with
            // the details
            if (this.IsAdding)
            {
                var response =
                    await client.PostAsync("api/customers",
                content);
                if (response.IsSuccessStatusCode)
                {
                    // TODO: Display the details of the new
                    customer
                }
                // TODO: Handle POST failure
            }
            // The user must be editing an existing customer,
            // so send the details by using a PUT request
            else
            {
                string path =
                $"api/customers/{this.Current.CustomerID}";

                var response = await client.PutAsync(path,
                content);
                if (response.IsSuccessStatusCode)
                {
                    this.IsEditing = false;
                    this.IsBrowsing = true;
                }
                // TODO: Handle PUT failure
            }
        }
        catch (Exception e)
        {
            // TODO: Handle exceptions
        }
    }
}
```
