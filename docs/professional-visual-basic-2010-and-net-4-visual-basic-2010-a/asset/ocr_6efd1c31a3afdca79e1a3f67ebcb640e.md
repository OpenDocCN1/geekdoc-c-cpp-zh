the `BirthDate` implementation from `Person` right into your enhanced implementation in `Employee`, creating a hybrid version of the property.

The `MyBase` keyword is covered in more detail later in the chapter. Here, you can see how it enables you to enhance or extend the functionality of the base class by adding your own code in the subclass but still invoking the base-class method when appropriate.

# Virtual Methods

The `BirthDate` method is an example of a virtual method. *Virtual methods* are methods in a base class that can be overridden and replaced by subclasses.

Virtual methods are more complex to understand than regular nonvirtual methods. With a nonvirtual method, only one implementation matches any given method signature, so there’s no ambiguity about which specific method implementation will be invoked. With virtual methods, however, there may be several implementations of the same method, with the same method signature, so you need to understand the rules that govern which specific implementation of that method will be called.

When working with virtual methods, keep in mind that the data type of the object is used to determine the implementation of the method to call, rather than the type of the variable that refers to the object.

Looking at the code in your form, you can see that you are declaring an object variable of type `Employee`, and then creating an `Employee` object that you can reference via that object:

```
Dim emp As New Employee()
```

It is not surprising, then, that you are able to invoke any of the methods that are implemented as part of the `Employee` class, and through inheritance, any of the methods implemented as part of the `Person` class:

```
With emp
    .Name = "Fred"
    .Name(NameTypes.Formal) = "Mr. Frederick R. Jones, Sr."
    .Name(NameTypes.Informal) = "Freddy"
    .BirthDate = #1/1/1960#
    .HireDate = #1/1/1980#
    .Salary = 30000
```

When you call the `BirthDate` property, you know that you are invoking the implementation contained in the `Employee` class, which makes sense because you know that you are using a variable of type `Employee` to refer to an object of type `Employee`.

Because your methods are virtual methods, you can experiment with some much more interesting scenarios. For instance, suppose that you change the code in your form to interact directly with an object of type `Person` instead of one of type `Employee`:

```
Private Sub btnOK_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnOK.Click

Dim person As New Person()

With person
    .Name = "Fred"
    .BirthDate = #1/1/1960#

    txtName.Text = .Name
    txtBirthDate.Text = Format(.BirthDate, "Short date")
End With

End Sub
```