
Imports System.ComponentModel.DataAnnotations

Namespace Models
    Public Class Customer
        Inherits ModelBase

        <Display(AutoGenerateField:=False)>
        Public Property CustomerID As Integer

        Private _Name As String
        <Display(Name:="Customer Name", Order:=0, Description:="This is the Customer's Name")>
        <Required()>
        Public Property Name As String
            Get
                Return _Name
            End Get
            Set(ByVal value As String)
                _Name = value
                RaisePropertyChange("Name")
            End Set
        End Property

        Private _PhoneNumber As String
        <Display(Name:="Phone Number", Order:=1)>
        <RegularExpression("^((0{0,1}[1-9]{1}{1}[0-9]{2}[\s]{0,1}[\-]{0,1}[\s]{0,1}[1-9]{1}[0-9]{6}$", ErrorMessage:="Please enter valid Phone Number (xxx) xxx-xxxx")>
        Public Property PhoneNumber As String
            Get
                Return _PhoneNumber
            End Get
            Set(ByVal value As String)
                _PhoneNumber = value
                RaisePropertyChange("PhoneNumber")
            End Set
        End Property

        Private _EMailAddress As String
        <Display(Name:="EMail Address", Order:=2)>
        <Required()>
        <RegularExpression("^([0-9a-zA-Z]([-\.\w]*[0-9a-zA-Z])*@([0-9a-zA-Z][-\w]*[0-9a-zA-Z])*(\.[0-9a-zA-Z][-\w]*[0-9a-zA-Z])*\.)+[a-zA-Z]{2,9}$", ErrorMessage:="Please enter valid email address")>
        Public Property EMailAddress As String
            Get
                Return _EMailAddress
            End Get
            Set(ByVal value As String)
                _EMailAddress = value
                RaisePropertyChange("EMailAddress")
            End Set
        End Property

        Private _Address As String
        <Display(Name:="Address", Order:=3)>
        Public Property Address As String
            Get
                Return _Address
            End Get
            Set(ByVal value As String)
                _Address = value
                RaisePropertyChange("Address")
            End Set
        End Property

End Property

Private _City As String
<Display(Name:="City", Order:=4)>
Public Property City As String
    Get
        Return _City
    End Get
    Set(ByVal value As String)
        _City = value
        RaisePropertyChange("City")
    End Set
End Property

Private _State As String
<Display(Name:="State", Order:=5)>
Public Property State As String
    Get
        Return _State
    End Get
    Set(ByVal value As String)
        _State = value
        RaisePropertyChange("State")
    End Set
End Property

Private _Zip As String
<Display(Name:="Zip", Order:=6)>
Public Property Zip As String
    Get
        Return _Zip
    End Get
    Set(ByVal value As String)
        _Zip = value
        RaisePropertyChange("Zip")
    End Set
End Property

End Class
End Namespace

As you can see, this model simply describes the data. You can also do custom validation in the model by using the CustomValidation attribute — for example, to do more complex validation you may need to use the regular expression validation.

Through such a simple model class you have centralized all of your business logic for the Customer class. This makes the class very simple to test and very reusable. If you create a List(Of Customer) and bind it to a data grid, it will use this logic to validate the rows; or if you bind one instance of the Customer class to a DataForm, it will also use the same validation. Clearly, centralizing this logic in one place creates powerful code.

The other part of the implementation for the model is the model base. All models in your project should inherit from a ModelBase class. This is how you can centralize how you implement the INotifyPropertyChanged needs of a model. Here is the sample ModelBase for this project:

```
Imports System
Imports System.Collections.Generic
Imports System.ComponentModel
Imports System.ComponentModel.DataAnnotations

Namespace Models
```

![](img/d99870e80390742f93963da7be0b2e61_723_0.png)

Public MustInherit Class ModelBase
    Implements INotifyPropertyChanged

    Private Property validationResults() As List(Of ValidationResult)

    Protected Sub RaisePropertyChange(ByVal ParamArray propertyname() As String)
        For Each s As String In propertyname
            RaiseEvent PropertyChanged(Me, New PropertyChangedEventArgs(s))
        Next

    End Sub

    Protected Sub Validate(ByVal value As Object, ByVal propertyName As String)
        Validator.ValidateProperty(value,
            New ValidationContext(Me, Nothing, Nothing))
    End Sub

    Public Function IsValid() As Boolean
        Return Validator.TryValidateObject(Me,
            New ValidationContext(Me, Nothing, Nothing), Me.validationResults, True)
    End Function

    Public Event PropertyChanged(ByVal sender As Object,
    ByVal e As System.ComponentModel.PropertyChangedEventArgs)
    Implements System.ComponentModel.INotifyPropertyChanged.PropertyChanged

    End Class
End Namespace

Code snippet from MyModels

The PropertyChanged event is what lets the View know that something changed in your model. This is the most basic model implementation for MVVM.

## The View

The View is simply the user interface to which you will bind your ViewModel. The ViewModel should simply be a description of where fields are placed to display data. If you read various references outlining the ways to do MVVM, you will find many highly opinionated developers who believe that there should be zero code in your code-behind for your views. While this is a noble goal, it is not always practical.

The View is generally just a simple user control to place controls on the form; but there is also an out-of-the-box view called DataForm that will use the metadata from the model to generate the form. This is great for building applications quickly and easily.

That is just one way to create a View; the other is to actually define the fields directly on the user control. To bind a text field to a model, you would do the following:

```
<TextBox Text="{Binding CompanyName,Mode=TwoWay,ValidatesOnDataErrors=True,
NotifyOnValidationError=True}" />
```

This will allow the View to receive validation errors directly from the model. For you, this means that there is no business logic in your View — it is self-contained in the Model, which creates an ideal way of testing your UI also.

## The ViewModel

The final part of the MVVM puzzle is the ViewModel. You can think of this as the glue that binds the Model and the View together. It is what will go and get the data from the Web service and fill a collection of your model class to bind to other controls.

In addition, you will bind the View’s data context to an instance of the ViewModel. This basically becomes the code-behind for your view except that it is loosely tied to the view so you can reuse it for multiple views. This also gives you great flexibility for testing and much more.

## SUMMARY

In this chapter you saw how to interact with various types of Web services, and used that knowledge to build a basic MVVM application. This will give you a foundation for building stronger Silverlight line-of-business applications. The lessons you have learned throughout this chapter, Chapter 18, and Chapter 19 should enable you to build very powerful Silverlight applications with rich interfaces. There are also many new technologies coming with Silverlight 4 that will continue to make it easier to build applications, and using less code.

# 21

# Working with ASP.NET

## WHAT YOU WILL LEARN IN THIS CHAPTER

- Overview of ASP.NET
- Introduction to Web Forms
- Using server controls
- Working with events
- Understanding ViewState
- Adding validation
- Building data-driven applications

ASP.NET is a Web application framework (built on top of the .NET framework) that enables you to build powerful, secure, and dynamic applications in a highly productive environment. This chapter introduces ASP.NET and helps get you started building applications for the Web.

## THE HISTORY OF ASP.NET

The technologies and practices around Web development have changed considerably since .NET was first released in 2002, and ASP.NET has evolved to keep up. The additions of the provider model, ASP.NET AJAX, ASP.NET MVC, ASP.NET Dynamic Data, Silverlight, and SharePoint have enabled Web developers on the Microsoft platform to build applications that meet the needs and expectations of today’s consumer.

Here’s a brief summary of the versions of ASP.NET and some of the key features introduced with each version.

| VERSION | FEATURES |
|---|---|
| 1.0/1.1 | Web Forms |
| 2.0 | Master pages<br>Themes and skins<br>DataSource controls |
