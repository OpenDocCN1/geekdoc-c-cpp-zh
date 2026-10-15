This is pretty much the normal interface definition you would expect, but with a couple of new attributes included. The <ServiceContract()> attribute is used to define the class or interface as the service class, and it needs to precede the opening declaration of the class or interface.

Within the interface, four methods are defined. Each of these methods is going to be exposed through the WCF service as part of the service contract, so they all require that the <OperationContract()> attribute be applied to them.

# Utilizing the Interface

The next step is to create a class that implements the interface. Not only is the new class implementing the interface defined, it is also implementing the service contract. From Solution Explorer, right-click on the generated Service1.vb file and rename this file as Calculator.vb. Next, replace the code in this file with the code that follows:

```
Public Class Calculator
    Implements ICalculator
    Public Function Add(ByVal a As Integer,
                        ByVal b As Integer) As Integer _
                        Implements ICalculator.Add
        Return (a + b)
    End Function
    Public Function Subtract(ByVal a As Integer,
                             ByVal b As Integer) As Integer _
                        Implements ICalculator.Subtract
        Return (a - b)
    End Function
    Public Function Multiply(ByVal a As Integer,
                             ByVal b As Integer) As Integer _
                        Implements ICalculator.Multiply
        Return (a * b)
    End Function
    Public Function Divide(ByVal a As Integer,
                           ByVal b As Integer) As Integer _
                        Implements ICalculator.Divide
        Return (a / b)
    End Function
End Class
```

From these new additions, you can see that nothing is done differently with the Calculator class than what you might do otherwise. It is a simple class that implements the ICalculator interface and provides implementations of the Add, Subtract, Multiply, and Divide methods.

With the interface and the class available, you now have your WCF service built and ready to go. The next step is to get the service hosted. This is a simple service. One of the simplicities of the service is that it exposes only simple types, rather than a complex type. This enables you to build only a service contract and not have to deal with construction of a data contract. Constructing data contracts is presented later in this chapter.

# Hosting the WCF Service in a Console Application

The next step is to take the service just developed and host it in some type of application process. You have many available hosting options, including the following:

+   - Console applications
+   - Windows Forms applications
+   - Windows Presentation Foundation applications
+   - Managed Windows Services