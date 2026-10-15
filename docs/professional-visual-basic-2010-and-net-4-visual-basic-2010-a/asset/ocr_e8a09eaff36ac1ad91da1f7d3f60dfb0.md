```
End Interface

<System.CodeDom.Compiler.GeneratedCodeAttribute("System.ServiceModel", "4.0.0.0")> _
Public Interface ICalculatorChannel
    Inherits CalculatorService.ICalculator, System.ServiceModel.IClientChannel
End Interface

<System.Diagnostics.DebuggerStepThroughAttribute(), _
System.CodeDom.Compiler.GeneratedCodeAttribute("System.ServiceModel", "4.0.0.0")> _
Partial Public Class CalculatorClient
    Inherits System.ServiceModel.ClientBase(Of CalculatorService.ICalculator)
    Implements CalculatorService.ICalculator

    Public Sub New()
        MyBase.New
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String)
        MyBase.New(endpointConfigurationName)
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String,
        ByVal remoteAddress As String)
        MyBase.New(endpointConfigurationName, remoteAddress)
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String,
        ByVal remoteAddress As System.ServiceModel.EndpointAddress)
        MyBase.New(endpointConfigurationName, remoteAddress)
    End Sub

    Public Sub New(ByVal binding As System.ServiceModel.Channels.Binding,
        ByVal remoteAddress As System.ServiceModel.EndpointAddress)
        MyBase.New(binding, remoteAddress)
    End Sub

    Public Function Add(ByVal a As Integer, ByVal b As Integer) As Integer
        Implements CalculatorService.ICalculator.Add
        Return MyBase.Channel.Add(a, b)
    End Function

    Public Function Subtract(ByVal a As Integer, ByVal b As Integer) As Integer
        Implements CalculatorService.ICalculator.Subtract
        Return MyBase.Channel.Subtract(a, b)
    End Function

    Public Function Multiply(ByVal a As Integer, ByVal b As Integer) As Integer
        Implements CalculatorService.ICalculator.Multiply
        Return MyBase.Channel.Multiply(a, b)
    End Function

    Public Function Divide(ByVal a As Integer, ByVal b As Integer) As Integer
        Implements CalculatorService.ICalculator.Divide
        Return MyBase.Channel.Divide(a, b)
    End Function
End Class
End Namespace
```

Here, an interface is defining the four methods and the implementing class CalculatorClient, which contains the functions that, in turn, call the service built earlier in the chapter.