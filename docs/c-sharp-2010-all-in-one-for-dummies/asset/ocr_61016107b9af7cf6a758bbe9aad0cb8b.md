# Element binding

In this chapter, we bind Label and TextBox controls to properties of underlying objects. You are not limited to this scenario; you can bind to just about anything from primitive variables to property values gleaned from other UIElements. Element binding in particular has its own component in the Binding expression. For instance, suppose you have a TextBox and Label control in your window. You would like to have the Content of the Label automatically update with the changing value of the Text property of the TextBox. The XAML code to accomplish Element Binding between the TextBox and the Label looks similar to:

```
<Label x:Name="lblCarMake" Content="{Binding ElementName=txtCarMake, Path=Text}"/>
<TextBox x:Name="txtCarMake" Width="100" Height="25" />
```

The C# code to define this binding looks similar to:

```
Binding b = new Binding("Text");
b.ElementName = "txtCarMake";
BindingOperations.SetBinding(lblCarMake, Label.ContentProperty, b);
```

# Validating data

It is good practice to validate any input provided to you from the user. People aren't perfect, and some people can be downright malicious. WPF provides a built-in framework for data validation and error notification. It is available to you through the implementation of the IDataErrorInfo interface on your classes.

![](bbox=[0.05, 0.78, 0.18, 0.9])

Let's add validation to the Car class you already created in BindingSample2 from the preceding section.

The complete solution is available on the Web in the BindingSample2 Validation project.

Just follow these steps to add validation to your Car class:

+   1. Open the Car.cs file, and edit the class to also implement the IDataErrorInfo interface, like this:

```
public class Car : INotifyPropertyChanged, IDataErrorInfo
```

Implementing this interface adds the following methods to the Car class:

```
public string Error
{
    get { throw new NotImplementedException(); }
}
```