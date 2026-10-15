# The Overrides Keyword

In a subclass, you override a method by implementing a method with the same name and parameter list as the base class, and then you use the Overrides keyword to indicate that you are overriding that method.

This is different from overloading, because when you overload a method you are adding a new method with the same name but a different parameter list. When you override a method, you are actually replacing the original method with a new implementation.

Without the Overrides keyword, you will receive a compilation error when you implement a method with the same name as one from the base class. Open the code window for the Employee class and add a new BirthDate property:

```
Public Class Employee
    Inherits Person

    Public Property HireDate As Date
    Public Property Salary As Double
    Public Property BirthDate As Date

    Private mNames As New Generic.Dictionary(Of NameTypes, String)

    Public Overrides Property BirthDate() As Date
        Get
            Return mBirthDate
        End Get
        Set(ByVal value As Date)
            If DateDiff(DateInterval.Year, Value, Now) >= 16 Then
                mBirthDate = value
            Else
                Throw New ArgumentException("An employee must be at least 16 years old.")
            End If
        End Set
    End Property
```

Because you are implementing your own version of the property, you have to declare a variable to store that value within the Employee class. This is not ideal, and there are a couple of ways around it, including the MyBase keyword and the Protected scope.

Notice also that you have enhanced the functionality in the Set block, so it now raises an error if the new birth-date value would cause the employee to be less than 16 years of age. With this code, you have now entirely replaced the original BirthDate implementation with a new one that enforces your business rule (see Figure 3-8).

The diagram now includes a BirthDate method in the Employee class. While perhaps not entirely intuitive, this is how the class diagram indicates that you have overridden the method. If you hover over the mouse over the BirthDate property in the Employee class, the tooltip will show the method signature, including the Overrides keyword.

If you run your application and click the button on the form, then everything should work as it did before, because the birth

![](bbox=[0.68, 0.545, 0.88, 0.565])

![](bbox=[0.55, 0.585, 0.88, 0.905])