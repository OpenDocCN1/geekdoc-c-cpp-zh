date you are supplying conforms to your new business rule. Now change the code in your form to use an invalid birth date:

```
With emp
.Name = "Fred"
.Name(NameTypes.Formal) = "Mr. Frederick R. Jones, Sr."
.Name(NameTypes.Informal) = "Freddy"
.BirthDate = #1/1/2000#
```

When you run the application (from within Visual Studio) and click the button, you receive an error indicating that the birth date is invalid. This proves that you are now using the implementation of the BirthDate method from the Employee class, rather than the one from the Person class. Change the date value in the form back to a valid value so that your application runs properly.

# The MyBase Keyword

You have just seen how you can entirely replace the functionality of a method in the base class by overriding it in your subclass. However, this can be somewhat extreme; sometimes it’s preferable to override methods so that you extend the base functionality, rather than replace it.

To do this, you need to override the method using the Overrides keyword as you just did, but within your new implementation you can still invoke the original implementation of the method. This enables you to add your own code before or after the original implementation is invoked — meaning you can extend the behavior while still leveraging the code in the base class.

To invoke methods directly from the base class, you can use the MyBase keyword. This keyword is available within any class, and it exposes all the methods of the base class for your use.

> Even a base class such as Person is an implicit subclass of System.Object, so it can use MyBase to interact with its base class as well.

This means that within the BirthDate implementation in Employee, you can invoke the BirthDate implementation in the base Person class. This is ideal, as it means that you can leverage any existing functionality provided by Person while still enforcing your Employee-specific business rules.

To take advantage of this, you can enhance the code in the Employee implementation of BirthDate. First, remove the declaration of mBirthDate from the Employee class. You won’t need this variable any longer because the Person implementation will keep track of the value on your behalf. Then, change the BirthDate implementation in the Employee class as follows:

```
Public Overrides Property BirthDate() As Date
    Get
        Return MyBase.BirthDate
    End Get

    Set(ByVal value As Date)
        If DateDiff(DateInterval.Year, Value, Now) >= 16 Then
            MyBase.BirthDate = value
        Else
            Throw New ArgumentException(
                "An employee must be at least 16 years old.")
        End If
    End Set
End Property
```

Run your application and you will see that it works just fine and returns the error, even though the Employee class no longer contains any code to actually keep track of the birth-date value. You have effectively merged