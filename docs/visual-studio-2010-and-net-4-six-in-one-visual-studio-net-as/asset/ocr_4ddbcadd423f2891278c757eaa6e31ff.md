However, because the implicit conversion from Nullable(Of T) to T is not allowed, the last two of the following assignments will result in compilation errors with Option Strict On:

```
Dim firstValue As Nullable(Of Integer) = 4
Dim secondValue As Nullable(Of Integer) = 5
' Cannot convert Nullable(Of Integer) to Integer:
Dim myValue As Integer = secondValue
Dim sumAs Integer = firstValue + SecondValue
```

# Documentation Comments

The C# language has been inspired by Javadoc and since the first release of C# in 2000, Visual Basic 2005 introduced the similar concept with a slightly different syntax from that C# and Visual Basic have separate tokens for comments.

Document comments in Visual Basic are special comments that begin with ''' (three quotation marks). They must immediately precede the type or member that they document. All adjacent comments are appended together to produce a single document comment. Here is an example of documentation comments:

```
<summary>
'''This abstract class defines an attribute with a simple string value.
</summary>
'''remarks
'''The class is intended to derive new attributes having a simple string value.
'''Do not use this class to add other properties to the attribute!
'''
Public MustInherit Class StringAttribute
Inherits Attribute
<summary>
'''Creates a new instance of this attribute and sets its initial value.
</summary>
'''param name="val">Initial attribute value.</param> */
Protected Sub New(ByVal val As String)
Value = val
End Sub
'''Other parts of the declaration omitted
End Class
```

During compilation, document comments are transformed into an XML file that can be utilized to generate human-readable source documentation. The documentation generator accepts and processes any tag that is valid according to the rules of XML. The Visual Basic language specification defines most 20 tags that provide commonly used functionality in user documentation.

# Operator Declarations

Operator declarations are methods that define the meaning of an existing Visual Basic operator for the containing class. When the operator is applied to the class in an instance, the operator is compiled into a call to the operator method defined in the class. You can declare unary, binary and conversion operators. Defining an operator for a class is also known as operator overloading.