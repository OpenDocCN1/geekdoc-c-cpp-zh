
The GetDate() method takes in three reference parameters and uses them to return the day, month, and year.

If you pass in the day, month and year reference variables without initializing them, an error will occur:

``` 
//---Error: day, month, and year not initialized---
int day, month, year;
GetDate(ref day, ref month, ref year);
```

If your intention is to use the variables solely to obtain some return values from the method, you can use the out keyword, which is identical to the ref keyword except that it does not require the variables passed in to be initialized first:

``` 
public void GetDate(out int day, out int month, out int year)
{
    day = DateTime.Now.Day;
    month = DateTime.Now.Month;
    year = DateTime.Now.Year;
}
```

Also, the out parameter in a function must be assigned a value before the function returns. If it isn't, a compiler error results.

Like the ref keyword, you need to prefix the arguments with the out keyword when calling the function:

``` 
int day, month, year;
GetDate(out day, out month, out year);
```

## The this Keyword

The this keyword refers to the current instance of an object (in a nonstatic class; discussed later in the section Static Classes). In the earlier section on methods, you saw the use of this :

``` 
Console.WriteLine("{0} {1}", this.FirstName, this.LastName);
```

While the FirstName and LastName variable could be referenced without using the this keyword, prefixing them with it makes your code more readable, indicating that you are referring to an instance member.

However, if instance members have the same names as your parameters, using this allows you to resolve the ambiguity:

``` 
public void SetName(string FirstName, string LastName)
{
    this.FirstName = FirstName;
    this.LastName = LastName;
}
```

## Part I: C# Fundamentals

Another use of the this keyword is to pass the current object as a parameter to another method. For example:

``` 
public class AddressBook
{
    public void AddContact(Contact c)
    {
        Console.WriteLine(c.ID);
        Console.WriteLine(c.FirstName);
        Console.WriteLine(c.LastName);
        Console.WriteLine(c.Email);
        //---other implementations here---
        //...
    }
}
```

The AddContact() method takes in a Contact object and prints out the details of the contact. Suppose that the Contact class has a AddToAddressBook() method that takes in an AddressBook object. This method adds the Contact object into the AddressBook object:

``` 
public class Contact
{
    public int ID;
    public string FirstName;
    public string LastName;
    public string Email;

    public void AddToAddressBook(AddressBook addBook)
    {
        addBook.AddContact(this);
    }
}
```

In this case, you use the this keyword to pass in the current instance of the Contact object into the AddressBook object. To test out that code, use the following statements:

``` 
Contact contact1 = new Contact();
contact1.ID = 12;
contact1.FirstName = "Wei-Meng";
contact1.LastName = "Lee";
contact1.Email = "weimenglee@learn2develop.net";

AddressBook addBook1 = new AddressBook();
contact1.AddToAddressBook(addBook1);
```

```csharp
public string FirstName
{
    get
    {
        return _FirstName;
    }
    set
    {
        _FirstName = value;
    }
}
public string LastName
{
    get
    {
        return _LastName;
    }
    set
    {
        _LastName = value;
    }
}
public string Email
{
    get
    {
        return _Email;
    }
    set
    {
        _Email = value;
    }
}
```

Note that the public members (ID, FirstName, LastName, and Email) have been replaced by properties with the set and get accessors.

The set accessor sets the value of a property. Using this example, you can instantiate a Contact class and then set the value of the ID property, like this:

```csharp
Contact c = new Contact();
c.ID = 1234;
```

In this case, the set accessor is invoked:

```csharp
public int ID
{
    get
    {
        return _ID;
    }
    set
    {
        _ID = value;
    }
}
```

The value keyword contains the value that is being assigned by the set accessor. You normally assign the value of a property to a private member so that it is not visible to code outside the class, which in this case is _ID.

When you retrieve the value of a property, the get accessor is invoked:

```csharp
public int ID
{
    get
    {
        return _ID;
    }
    set
    {
        _ID = value;
    }
}
```

The following statement shows an example of retrieving the value of a property:

```csharp
Console.WriteLine(c.ID); //---prints out 1234---
```

The really useful part of properties is the capability for you to perform checking on the value assigned. For example, before the ID property is set, you want to make sure that the value is between 1 and 9999, so you perform the check at the set accessor, like this:

```csharp
public int ID
{
    get
    {
        return _ID;
    }
    set
    {
        if (value > 0 && value <= 9999)
        {
            _ID = value;
        }
        else
        {
            _ID = 0;
        };
    }
}
```

Using properties, you can now prevent users from setting invalid values.

## Part I: C# Fundamentals

### Read-Only and Write-Only Properties

When a property definition contains the get and set accessors, that property can be read as well as written. To make a property read-only, you simply leave out the set accessor, like this:

```csharp
public int ID
{
    get
    {
        return _ID;
    }
}
```

You can now read but not write values into the ID property:

```csharp
Console.WriteLine(c.ID);   //---OK---
c.ID = 1234;               //---Error---
```

Likewise, to make a property write-only, simply leave out the get accessor:

```csharp
public int ID
{
    set
    {
        _ID = value;
    }
}
```

You can now write but not read from the ID property:

```csharp
Console.WriteLine(c.ID);   //---Error---
c.ID = 1234;               //---OK---
```

You can also restrict the visibility of the get and set accessors. For example, the set accessor of a public property could be set to private to allow only members of the class to call the set accessor, but any class could call the get accessor. The following example demonstrates this:

```csharp
public int ID
{
    get
    {
        return _ID;
    }
    private set
    {
        _ID = value;
    }
}
```

In this code, the set accessor of the ID property is prefixed with the private keyword to restrict its visibility. That means that you now cannot assign a value to the ID property but you can access it:

```csharp
c.ID = 1234;                //---error---
Console.WriteLine(c.ID);    //---OK---
```

You can, however, access the ID property anywhere within the Contact class itself, such as in the Email property:

```csharp
public string Email
{
    get
    {
        //...
        this.ID = 1234;
        //...
    }
    //...
}
```

## Partial Methods (C# 3.0)

Earlier on, you saw that a class definition can be split into one or more class definitions. In C# 3.0, this concept is extended to methods — you can now have partial methods. To see how partial methods works, consider the Contact partial class:

```csharp
public partial class Contact
{
    //...
    private string _Email;
    public string Email
    {
        get
        {
            return _Email;
        }
        set
        {
            _Email = value;
        }
    }
}
```

Suppose that you want to allow users of this partial class to optionally log the email address of each contact when its Email property is set. In that case, you can define a partial method — LogEmail() in this example — like this:

```csharp
public partial class Contact
{
    //...
}

public partial class Contact
{
    //...
```
