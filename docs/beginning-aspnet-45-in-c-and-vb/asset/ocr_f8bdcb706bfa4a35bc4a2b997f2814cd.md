```
VB.NET
Dim myPerson As Person = New Person()  ' Create a new instance of Person
myPerson.FirstName = "Imar"  ' Accessing setter to change the value

Label1.Text = myPerson.FirstName  ' Accessing getter that now returns Imar
```

```
C#
Person myPerson = new Person();  // Create a new instance of Person
myPerson.FirstName = "Imar";  // Accessing setter to change the value

Label1.Text = myPerson.FirstName;  // Accessing getter that now returns Imar
```

For simple properties that don't need any data manipulation or validation, you can use so-called automatic properties. With these properties, you can use a much more condensed syntax without the need for a private backing variable. When the code is compiled, the compiler creates a hidden backing variable for you, and you'll need to refer to the public property. Here's the DateOfBirth property of the Person class, written as an automatic property:

```
VB.NET
Public Property DateOfBirth As DateTime
```

```
C#
public DateTime DateOfBirth { get; set; }
```

The Visual Basic implementation of automatic properties has one advantage over the C# version: You can declare the property and give it a value in one shot. The following snippet defines a CreateDate property and assigns it with the current date and time:

```
VB.NET
Public Property CreateDate As DateTime = DateTime.Now
```

To assign a default value to an automatic property in C#, you need to set its value using constructors, which are discussed later.

# Creating Read-Only and Write-Only Properties

At times, read-only or write-only properties make a lot of sense. For example, the ID of an object could be read-only if it is assigned by the database automatically. When the object is constructed from the database, the ID is assigned to the private backing variable. The public Id property is then made read-only to stop calling code from accidentally changing it. Likewise, you can have a write-only property for security reasons. For example, you could have a Password property on a Person object that you can only assign to if you know it, but no longer read it afterward. Internally, code within the class can still access the backing variables to work with the password value. Another good candidate for a read-only property is one that returns a combination of data. Consider a FullName property of a Person class that returns a combination of the FirstName and LastName properties. You use the setter of each individual property to assign data, but you can have a read-only property that returns the concatenated values.