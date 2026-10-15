This means that you can simply override the ToString method from the Object class within your Person class by adding the following code:

```
Public Overrides Function ToString() As String
    Return Name
End Function
```

This implementation returns the person’s Name property as a result when ToString is called.

> By default, ToString returns the class name of the class. Until now, if you called the ToString method on a Person object, you would get a result of InheritanceAndInterfaces.Person. InheritanceAndInterfaces represents your assembly name when you create your project.

Notice that the ToString method is calling another method within your same class — in this case, the Name method.

You could also write this routine using the Me keyword:

```
Public Overrides Function ToString() As String
    Return Me.Name
End Function
```

This is redundant because Me is the default for all method calls in a class. These two implementations are identical, so typically the Me keyword is simply omitted to avoid the extra typing.

To see how the ToString method now works, you can change your code in Form1 to use this value instead of the Name property:

```
Private Sub btnOK_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnOK.Click
    Dim objPerson As OfficeEmployee = New OfficeEmployee()

    With objPerson
        .Name = "Fred"
        .BirthDate = #1/1/1960#
        .Age = 20
        .OfficeNumber = "A42"

        txtName.Text = .ToString()
        txtBirthDate.Text = Format(.BirthDate, "Short date")
        txtAge.Text = CStr(.Age)
        txtOffice.Text = .OfficeNumber
    End With
End Sub
```

When you run the application, the person’s name is displayed appropriately, which makes sense, as the ToString method is simply returning the result from the Name property.

Earlier, you looked at virtual methods and how they work. Because either calling a method directly or calling it using the Me keyword invokes the method on the current object, the method calls conform to the same rules as an external method call. In other words, your ToString method may not actually end up calling the Name method in the Person class if that method was overridden by a class farther down the inheritance chain, such as the Employee or OfficeEmployee classes.

For example, you could override the Name property in your OfficeEmployee class such that it always returns the informal version of the person’s name, rather than the regular name. You can override the Name property by adding this method to the OfficeEmployee class: