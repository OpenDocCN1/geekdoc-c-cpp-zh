
A constant is usually a value type or a string literal because the only way to create a non-null value of a reference type other than `string` is to use the `new` operator, which is not permitted.

### Watch Out!

#### Constants Should Be Constant

When creating constants, you should be sure that the value is something that is logically constant forever. Good constants are things that never change, such as the value of Pi, the year Elvis was born, or the number of items in a mol.

If you need to create a field that has constant-like behavior but uses a type not allowed in a constant declaration, you can use a `static` read-only field instead by specifying both the `static` and `readonly` modifiers. A read-only field can be initialized only as part of its declaration or in a constructor.

### Try It Yourself

### Working with Fields

By following these steps, you explore how to create a class containing data and how to provide access to that data. If you closed Visual Studio, repeat the previous exercise first. Keep Visual Studio open at the end of this exercise because you will use this application later.

- 1. Create a new Console application.
- 2. Add a new class file named Contact.cs. Inside the body of the class, declare three private fields named `firstName`, `lastName`, and `dateOfBirth` of type `string`, `string`, and `DateTime`, respectively.
- 3. Add the following method to the class. You learn more about methods later in this hour and more about the StringBuilder class in Hour 8, "Using Strings and Regular Expressions":

```csharp
public override string ToString()
{
    StringBuilder stringBuilder = new StringBuilder();
    stringBuilder.AppendFormat("Name: {0} {1}\r\n", this.firstName, this.lastName);
    stringBuilder.AppendFormat("Date of Birth: {0}\r\n", this.dateOfBirth);
    return stringBuilder.ToString();
}
```

- 4. In the Main method of the Program.cs file, enter the following:

```csharp
Contact c = new Contact();
Console.WriteLine(c.ToString());
```

- 5. Run the application using Ctrl+F5 and observe that the output matches what is shown in Figure 3.3.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_91_0.png)

Figure 3.3 Working with fields

### Properties

If fields represent state and data but are typically private, there must be a mechanism that enables the class to provide that information publicly. Knowing the different accessibility options allowed it would be tempting to simply declare the class fields to have public accessibility.

This would allow us to satisfy the rules of abstraction, but this would then violate the rules of encapsulation because the fields could be directly manipulated. How, then, is it possible to satisfy both the rules of encapsulation and abstraction? What is needed is something accessed using the same syntax as a field but that can define different accessibility than the field itself. Properties enable us to do exactly that. A property provides a simple way to access a field, called the **backing field**, which can be publicly available while still allowing the internal details of that field to be hidden. Just as fields can be static, properties can also be static and are not associated with an instance of the class.

Although fields declare variables, which require storage in memory, properties do not. Instead, properties are declared with accessors that enable you to control whether a value can be read or written and what should occur when you do so. The get accessor enables the property value to be read, whereas the set accessor enables the value to be written.

Listing 3.2 shows the simplest way to declare a property. When using this syntax, known as **automatic properties**, you omit the backing field declaration and must always include both the get and set accessor without a declared implementation, which the compiler provides.

#### LISTING 3.2 Declaring an Automatic Property

```csharp
class Contact
{
   public string FirstName
   {
      get;
      set;
   }
}
```

In fact, the compiler transforms the code shown in Listing 3.2 into code that looks roughly like that shown in Listing 3.3.

#### LISTING 3.3 Declaring a Property

```csharp
class Contact
{
    private string firstName;

    public string FirstName
    {
        get
        {
            return this.firstName;
        }
        set
        {
            this.firstName = value;
        }
    }
}
```

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_92_0.png)

#### Automatic Properties

Automatic properties are convenient, especially when you implement a large number of properties. This convenience does come at a slight cost, however.

Because you don’t provide a body for the accessors, you can’t specify any logic that executes as part of that accessor, and both accessors must be declared using the automatic property syntax. As a result, if at some point later you realize that you need to provide logic for either of the accessors, you need to add a backing field and the appropriate logic to both accessors.

Fortunately, this change doesn’t affect the public interface of your class, so it is safe to make, although it might be a bit tedious.

The get accessor uses a return statement, which simply instructs the accessor to return the value indicated. In the set accessor of the code in Listing 3.3, the class field firstName is set equal to value, but where does value come from? From Table 1.6 in Chapter 1, you know that value is a contextual keyword. When used in a property set accessor, the value keyword always means “the value that was provided by the caller” and is always typed to be the same as the property type.

By default, the property accessors inherit the accessibility declared on the property definition itself. You can, however, declare a more restrictive accessibility for either the get or the set accessor.

You can also create calculated properties that are read-only and do not have a backing field. These calculated properties are excellent ways to provide data derived from other information.

Listing 3.4 shows a calculated `FullName` property that combines the `firstName` and `lastName` fields.

#### LISTING 3.4 Declaring a Calculated Property

```csharp
class Contact
{
    private string firstName;
    private string lastName;

    public string FullName
    {
        get
        {
            return this.firstName + " " + this.lastName;
        }
    }
}
```

#### Read-Only and Write-Only Properties

For explicitly declared properties, you are allowed to omit either accessor. By including only the `get` accessor, you create a read-only property. To create the equivalent of a read-only property using automatic properties, you would declare the `set` accessor to be `private`.

By including only the `set` accessor, or declaring the `get` accessor to be `private`, you create a write-only property. In practice, you should avoid write-only properties.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_93_0.png)

Because properties are accessed as if they were fields, the operations performed in the accessors should be as simple as possible. If you need to perform more complex operations or perform an operation that could be time-consuming or expensive (resource consuming), it might be better to use a method rather than a property.

### Try It Yourself

### Working with Properties

To modify the `Contact` class to allow access to the private data using properties, and to use automatic and calculated properties, follow these steps. If you closed Visual Studio, repeat the previous exercise first. Be sure to keep Visual Studio open at the end of this exercise because you will use this application later.

- 1. Open the Contact.cs file.
- 2. Add a new public property named `DateOfBirth` that enables reading and writing to the `dateOfBirth` field.
- 3. Remove the `firstName` and `lastName` fields and create a `FirstName` and `LastName` property as automatic properties.
- 4. Add a calculated property named `FullName`, which combines the values of the `FirstName` and `LastName` properties. This should be similar to the calculated property shown in Listing 3.4.
- 5. Modify the `ToString` method to make use of the new `FullName` property instead of performing the string concatenation directly.
- 6. In the `Main` method of the `Program.cs` file, enter the following code after the `Console.WriteLine` statement:

```csharp
c.FirstName = "Jim";
c.LastName = "Morrison";
c.DateOfBirth = new DateTime(1943, 12, 8);
Console.WriteLine(c.ToString());
```

- 7. Run the application using Ctrl+F5, and observe that the output matches what is shown in Figure 3.4.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_94_0.png)

### Methods

If fields and properties define and implement data, methods, which are also called **functions**, define and implement a behavior or action that can be performed. The `WriteLine` action of the `Console` class you have been using in the examples and exercises so far is an example of a method.

Listing 3.5 shows how to add a method to the `Contact` class that verifies an email address. In this case, the `VerifyEmailAddress` method specifies `void` as the return type, meaning that it does not return a value.
