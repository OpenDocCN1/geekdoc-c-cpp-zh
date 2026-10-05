```
{
  this.LastError = response.ReasonPhrase;
}
catch (Exception e) {
  this.LastError = e.Message;
}
finally {
  this.OnPropertyChanged(nameof(CustomerListCount));
  this.IsBusy = false;
}
```

This method is similar to the GetDataAsync method that you implemented previously. The main differences are as follows:

+   * This method takes a Customer object as its parameter. This object will contain the search criteria provided by the user.
* The code calls the GetAsync method of the HttpClient object to send a request to the /api/customers/find endpoint of the web service. The parameters passed to the request are retrieved from the Customer object. If any field is null, the wildcard character % is sent instead.

+   9. After the FindCustomerAsync method, define the Search method as follows:

Click here to view code image

```
private void Search()
{
  Customer searchPattern = new Customer { CustomerID = 0 };
  this.customers.Insert(currentCustomer, searchPattern);
  this.IsSearching = true;
  this.OnPropertyChanged(nameof(Current));
}
```

This method creates a new Customer object and makes it the current customer in the Customers list before putting the ViewModel into search mode. This action causes the customer to be displayed on the page. The user can provide values and populate the Customer object using the page.

+   10. Create the View method shown next, after the Search method:

Click here to view code image