```
set
{
    this._firstName = value;
}
private string _lastName;
public string LastName
{
    get => this._lastName;
    set {
        this._lastName = value;
    }
}
private string _emailAddress;
public string EmailAddress
{
    get => this._emailAddress;
    set {
        this._emailAddress = value;
    }
}
private string _phone;
public string Phone
{
    get => this._phone;
    set {
        this._phone = value;
    }
}
```

You might be wondering why the class doesn't define automatic properties, or why the property setters are not implemented as expression-bodied members, given that all they do is set the value in a private field. The answer to both of these questions is that you will add code to these properties in a later exercise.

+   6. In Solution Explorer, in the Customers project, double-click the MainPage.xaml file to display the user interface for the application in the Design View window.