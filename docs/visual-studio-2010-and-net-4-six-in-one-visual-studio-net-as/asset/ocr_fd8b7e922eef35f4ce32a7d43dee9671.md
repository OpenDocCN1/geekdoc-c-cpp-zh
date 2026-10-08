# Multiline Lambda Expressions

Lambda expressions introduced in Visual Basic 2008 represent a function without a name that calculates and returns a single value. Lambda expressions can be used wherever delegate type is valid. They provide a simple and concise syntax to eliminate the need for defining separate functions to be passed as delegates.

For example, without lambda expressions, you could write similar code in Visual Basic 2005:

```
Module VB2005Module

Delegate Function BinaryOperation(ByVal op1 As Double, \\ByVal op2 As Double) As Double

Sub Main()
Dim op1 As Double = 12.3
Dim op2 As Double = 23.4
Dim operation As BinaryOperation = AddressOf MyOperation
Dim Result As Double = operation(op1, op2)
End Sub

Function MyOperation(ByVal op1 As Double, ByVal op2 As Double) As Double
Return (op1 + op2) / op2
End Function

End Module
```

With Visual Basic 2008 lambda expressions, it gets shorter:

```
Module VB2008Module

Delegate Function BinaryOperation(ByVal op1 As Double, \\ByVal op2 As Double) As Double

Sub Main()
Dim op1 As Double = 12.3
Dim op2 As Double = 23.4
Dim operation As BinaryOperation = =
Function(x As Double, y As Double) (x + y) / y
Dim Result As Double = operation(op1, op2)
End Sub

End Module
```

While Visual Basic 2008 lambda expression implementation is great, it has two significant constraints:

+   - Only single-line functions can be used to define the return value of the lambda expressions.

+   - Only Function definitions are allowed; subroutines cannot be used.