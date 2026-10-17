
<Rectangle Grid.Row="0" RowSpan="6" Grid.Column="1" Grid.ColumnSpan="7" ...>

<Rectangle.Fill>

  <LinearGradientBrush EndPoint="0.5,0.1" StartPoint="0.5,0.0">

    <GradientStop Color="#FF0E3899"/>

    <GradientStop Color="#FF141415" Offset="0.9"/>

  </LinearGradientBrush>

</Rectangle.Fill>

</Rectangle>

```
```csharp

public class Customer

{

    private int _customerID;

    public int CustomerID

    {

        get => _customerID;

        set { _customerID = value; }

    }

    private string _title;

    public string Title

    {

        get => _title;

        set { _title = value; }

    }

    private string _firstName;

    public string FirstName

    {

        get => _firstName;

        set { _firstName = value; }

    }

    private string _lastName;

    public string LastName

    {

        get => _lastName;

        set { _lastName = value; }

    }

    private string _email;

    public string Email

    {

        get => _email;

        set { _email = value; }

    }

    private string _phone;

    public string Phone

    {

        get => _phone;

        set { _phone = value; }

    }

}

```
```csharp

public MainPage()

{

    InitializeComponent();

    Customer customer = new Customer

    {

        CustomerID = 1,

        Title = "Mr",

        LastName = "Sharp",

        Email = "john@contoso.com",

        Phone = "111-1111"

    };

    this.DataContext = customer;

}

```
```csharp

using System.ComponentModel;

```
```csharp

public class Customer : INotifyPropertyChanged

{

    ...

}

```
```csharp

public class Customer : INotifyPropertyChanged

{

    ...

    private string _phone;

    public string Phone

    {

        get => this._phone;

        set { this._phone = value; }

    }

    public event PropertyChangedEventHandler PropertyChanged;

}

```
```csharp

class Customer : INotifyPropertyChanged

{

    ...

    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void OnPropertyChanged(string propertyName)

    {

        if (PropertyChanged is not null)

        {

            PropertyChanged(this,

                new PropertyChangedEventArgs(propertyName));

        }

    }

}

```
```csharp

PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));

```
```csharp

private string _lastName;

public string LastName

{

    get => this._lastName;

    set {

        this._lastName = value;

        this.OnPropertyChanged(nameof(LastName));

    }

}

private string _emailAddress;

public string EmailAddress

{

    get => this._emailAddress;

    set {

        this._emailAddress = value;

        this.OnPropertyChanged(nameof(EmailAddress));

    }

}

private string _phone;

public string Phone

{

    get => this._phone;

    set {

        this._phone = value;

        this.OnPropertyChanged(nameof(Phone));

    }

}

...

```
```csharp

public int CustomerID

{

    get { return this._customerID; }

    set

    {

        this._customerID = value;

        this.OnPropertyChanged("CustomerID");

    }

}

```
```xml

<ComboBox ... x:Name="title" ... SelectedValue="{Binding Title}" ... />

```
```xml

<ComboBox ... x:Name="title" ... >

    <ComboBoxItem Content="Mr"/>

    <ComboBoxItem Content="Mrs"/>

    <ComboBoxItem Content="Ms"/>

    <ComboBoxItem Content="Miss"/>

</ComboBox>

```
```csharp

public MainPage()

{

    this.InitializeComponent();

    List<string> titles = new List<string>

    {

        "Mr", "Mrs", "Ms", "Miss"

    };

    this.title.ItemsSource = titles;

    this.cTitle.ItemsSource = titles;

    Customer customer = new Customer

    {

        ...

    };

    this.DataContext = customer;

}

```
```xml

<Grid x:Name="customersTabularView" ...>

  ...

  <ComboBox Grid.Row="1" Grid.Column="3" x:Name="title" ...

  SelectedValue="{Binding Title, Mode=TwoWay}">

  </ComboBox>

</Grid>

<Grid x:Name="customersColumnarView" ...>

  ...

  <ComboBox Grid.Row="1" Grid.Column="1" x:Name="cTitle" ...

  SelectedValue="{Binding Title, Mode=TwoWay}">

  </ComboBox>

  ...

</Grid>

```
```csharp

class ViewModel

{

    private List<Customer> customers;

    public ViewModel()

    {

        this.customers = new List<Customer>

        {

            new Customer

            {

                CustomerID = 1,

                Title = "Mr",

                FirstName="John",

                LastName="Sharp",

                EmailAddress="john@contoso.com",

                Phone="111-1111"

            },

            new Customer

            {

                CustomerID = 2,

                Title = "Mrs",

                FirstName="Diana",

                LastName="Sharp",

                EmailAddress="diana@contoso.com",

                Phone="111-1112"

            },

            new Customer

            {

                CustomerID = 3,

                Title = "Ms",

                FirstName="Francesca",

                LastName="Sharp",

                EmailAddress="frankie@contoso.com",

                Phone="111-1113"

            }

        };

    }

}

```
```csharp

class ViewModel

{

    private List<Customer> customers;

    private int currentCustomer;

    public ViewModel()

    {

        this.currentCustomer = 0;

        this.customers = new List<Customer>

        {

            ...

        }

    }

}

```
```csharp

class ViewModel

{

    ...

    public ViewModel()

    {

        ...

    }

    public Customer Current

    {

        get => this.customers.Count > 0 ? this.customers[currentCustomer] : null;

    }

}

```
```csharp

public MainPage()

{

    ...

    this.cTitle.ItemsSource = titles;

    ViewModel = new ViewModel();

}

```
```csharp

...using System.ComponentModel;

namespace Customers

{

    public class ViewModel : INotifyPropertyChanged

    {

        ...

    }

}

```
```csharp

public class ViewModel : INotifyPropertyChanged

{

    ...

    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void OnPropertyChanged(string propertyName)

    {

        if (PropertyChanged is not null)

        {

            PropertyChanged(this,

                new PropertyChangedEventArgs(propertyName));

        }

    }

}

```
```csharp

public class ViewModel : INotifyPropertyChanged

{

    ...

    public ViewModel()

    {

        ...

    }

    private bool _isAtStart;

    public bool IsAtStart

    {

        get => this._isAtStart;

        set {

            this._isAtStart = value;

            this.OnPropertyChanged(nameof(IsAtStart));

        }

    }

    private bool _isAtEnd;

    public bool IsAtEnd

    {

        get => this._isAtEnd;

        set {

            this._isAtEnd = value;

            this.OnPropertyChanged(nameof(IsAtEnd));

        }

    }

    ...

```
```csharp

public ViewModel()

{

    this.currentCustomer = 0;

    this.IsAtStart = true;

    this.IsAtEnd = false;

    this.customers = new List<Customer>

    {

        ...

    }

}

```
```csharp

public class ViewModel : INotifyPropertyChanged

{

    public Customer Current

    {

        ...

    }

    private void Next()

    {

        if (this.customers.Count - 1 > this.currentCustomer)

        {

            this.currentCustomer++;

            this.OnPropertyChanged(nameof(Current));

            this.IsAtStart = false;

            this.IsAtEnd = (this.customers.Count - 1 == this.currentCustomer);

        }

    }

    private void Previous()

    {

        if (this.currentCustomer > 0)

        {

            this.currentCustomer--;

            this.OnPropertyChanged(nameof(Current));

            this.IsAtEnd = false;

            this.IsAtStart = (this.currentCustomer == 0);

        }

    }

    ...

}

```
```csharp

public class ViewModel : INotifyPropertyChanged

{

    private List<Customer> customers;

    private int currentCustomer;
