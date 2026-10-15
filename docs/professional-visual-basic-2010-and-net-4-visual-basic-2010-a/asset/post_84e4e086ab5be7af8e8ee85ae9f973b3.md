

![](img/d99870e80390742f93963da7be0b2e61_547_0.png)

## Looking at WSDL and the Schema for HelloCustomerService

After you made the reference to the HelloCustomer service, it was possible for you to review the WSDL in your new reference. With the Solution Explorer showing all files, you’ll see the HelloCustomer1.wsdl within your solution. You can open this file to look at the WSDL, where you will find the following XSD imports:

```
<wsdl:types>
  <xsd:schema targetNamespace="http://www.Wrox.com/ns/Imports">
    <xsd:import schemaLocation="http://localhost:8000/HelloCustomer?xsd=xsd0" namespace="http://www.Wrox.com/ns/" />
    <xsd:import schemaLocation="http://localhost:8000/HelloCustomer?xsd=xsd1" namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
    <xsd:import schemaLocation="http://localhost:8000/HelloCustomer?xsd=xsd2" namespace="http://schemas.datacontract.org/2004/07/ProVB_WCFWithDataContract" />
  </xsd:schema>
</wsdl:types>
```

Code snippet from ProVB_HelloWorldConsumer\Service References\HelloCustomerService\HelloCustomer1.wsdl

http://localhost:8000/HelloCustomer?xsd=xsd2 provides the details about your Customer object. The code from the file HelloCustomer2.xsd, which is part of your reference definition, is shown here:

```
<?xml version="1.0" encoding="utf-8"?>
<xsd:schema
    xmlns:tns="http://schemas.datacontract.org/2004/07/ProVB_WCFWithDataContract"
    elementFormDefault="qualified"
    targetNamespace="http://schemas.datacontract.org/2004/07/ProVB_WCFWithDataContract"
    xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:complexType name="Customer">
    <xs:sequence>
      <xs:element minOccurs="0" name="FirstName" nillable="true" type="xs:string" />
      <xs:element minOccurs="0" name="LastName" nillable="true" type="xs:string" />
    </xs:sequence>
  </xs:complexType>
  <xs:element name="Customer" nillable="true" type="tns:Customer" />
</xsd:schema>
```

Code snippet from ProVB_HelloWorldConsumer\Service References\HelloCustomerService\HelloCustomer2.xsd

This is an XSD description of the Customer object. Making a reference to the WSDL that includes the XSD description of the Customer object causes the auto-generated proxy class (located in the file Reference.vb) to create the following class as part of the proxy (this code follows the Namespace declaration in the downloadable sample):

```
<System.Diagnostics.DebuggerStepThroughAttribute(), _
    System.CodeDom.Compiler.GeneratedCodeAttribute("System.Runtime.Serialization", "4.0.0.0"), _
    System.Runtime.Serialization.DataContractAttribute(Name:="Customer", Namespace:= _
    "http://schemas.datacontract.org/2004/07/ProVB_WCFWithDataContract"), _
    System.SerializableAttribute()> _
Partial Public Class Customer
    Inherits Object
    Implements System.Runtime.Serialization.IExtensibleDataObject,
        System.ComponentModel.INotifyPropertyChanged
    <System.NonSerializedAttribute()> _
    Private extensionDataField As _
        System.Runtime.Serialization.ExtensionDataObject

    <System.Runtime.Serialization.OptionalFieldAttribute()> _
    Private FirstNameField As String

    <System.Runtime.Serialization.OptionalFieldAttribute()> _
    Private LastNameField As String

    <Global.System.ComponentModel.BrowsableAttribute(false)> _
    Public Property ExtensionData() As _
        System.Runtime.Serialization.ExtensionDataObject _
    Implements System.Runtime.Serialization.IExtensibleDataObject.ExtensionData
        Get
            Return Me.extensionDataField
        End Get
        Set
            Me.extensionDataField = value
        End Set
    End Property

    <System.Runtime.Serialization.DataMemberAttribute()> _
    Public Property FirstName() As String
        Get
            Return Me.FirstNameField
        End Get
        Set
            If (Object.ReferenceEquals(Me.FirstNameField, value) <> _
                true) Then
                Me.FirstNameField = value
                Me.RaisePropertyChanged("FirstName")
            End If
        End Set
    End Property

    <System.Runtime.Serialization.DataMemberAttribute()> _
    Public Property LastName() As String
        Get
            Return Me.LastNameField
        End Get
        Set
            If (Object.ReferenceEquals(Me.LastNameField, value) <> _
                true) Then
                Me.LastNameField = value
                Me.RaisePropertyChanged("LastName")
            End If
        End Set
    End Property
```

Code snippet from ProVB_HelloWorldConsumer\Service References\HelloCustomerService\Reference.vb

As you can see, Visual Studio and WCF provide the tools you need to define and share complex data types across a distributed system. Combined with the other powerful features supported by WCF, you have the tools to build robust, enterprise-quality distributed solutions.

## SUMMARY

This chapter looked at one of the more outstanding capabilities provided to the Visual Basic world. Visual Studio 2010 and .NET 4 are a great combination for building advanced services that take your application to a distributed level.

Though not exhaustive, this chapter broadly outlined the basics of the WCF framework. As you begin to dig more deeply into the technology, you will find strong and extensible capabilities.

## PART III: Smart Client Applications

- CHAPTER 14: Windows Forms
- CHAPTER 15: Advanced Windows Forms
- CHAPTER 16: User Controls Combining WPF and Windows Forms
- CHAPTER 17: WPF Desktop Applications
- CHAPTER 18: Expression Blend 3
- CHAPTER 19: Silverlight

## 14 Windows Forms

### WHAT YOU WILL LEARN IN THIS CHAPTER

- How to construct a Windows Forms application
- How to control the startup and organization of your forms
- Important controls available in Windows Forms and how to take advantage of their capabilities
- Usage of special families of controls and components, such as extender providers, common dialogs, and the ToolStrip
- Programming tips for a variety of programming scenarios

Windows Forms is a part of the .NET Framework that is used to create user interfaces for local applications, often called Win32 clients. Windows Forms does not change when moving from Visual Basic 2005 or Visual Basic 2008 to Visual Basic 2010. Accordingly, the version number used for Windows Forms in Visual Studio 2010 is still 2.0.

The pace of change in Windows Forms is slowing because of the advent of Windows Presentation Foundation (WPF). Going forward, you can expect continued innovation in WPF, but not much in Windows Forms. However, that does not imply that you should abandon Windows Forms or be reluctant to write programs in it. Windows Forms still has many advantages over WPF.

Those advantages include a more complete set of controls and a mature, easy-to-use designer. The result is often faster development in Windows Forms compared to WPF. WPF has advantages of its own, of course. These are discussed in Chapter 17, which provides an introduction to WPF.

Chapter 15 includes more advanced treatment of certain aspects of Windows Forms. After gaining a basic understanding of the key capabilities in this chapter, you'll be ready to go on to the more advanced concepts in that chapter.

### THE SYSTEM.WINDOWS.FORMS NAMESPACE

You've already seen how namespaces are used to organize related classes in the .NET Framework. The main namespace used for Windows Forms classes is System.Windows.Forms. The classes in this namespace are contained in the System.Windows.Forms.dll assembly.

If you choose a Windows Forms Application project or Windows Forms Control Library project in VS.NET, a reference to System.Windows.Forms.dll is added by default. In some other cases, such as creating a library that will work with controls, you need to add that reference manually. (You can learn more about creating controls in Windows Forms in Chapter 15.)

### USING FORMS

A window on the desktop is created in Windows Forms by using a form. Thus, a form is the outer container for your application’s interface.

A form is just a special kind of class in Windows Forms. A class becomes a form based on inheritance. It must have the System.Windows.Forms.Form class in its inheritance tree, which causes the form to have the behavior and object interface a form requires.

The preferred technique to create a form is to create an instance with the New keyword, just as you would with any other class. Typical code would look like this:

```
Dim f As New Form1
f.Show()
```

### Setting a Startup Form

If you create a new Windows Forms application in Visual Studio, by default it will contain a form class named Form1. The properties for the project will be set to use that form as the startup form for the application — that is, it will be the initial form displayed when the application begins.

To change the startup form, open the Properties dialog for the project. Do this using the Project Properties menu. You can also invoke the window by right-clicking the project name in the Solution Explorer and selecting Properties from the context menu. The Properties dialog for a Windows Forms application is shown in Figure 14-1.

![](img/d99870e80390742f93963da7be0b2e61_552_0.png)

FIGURE 14-1

