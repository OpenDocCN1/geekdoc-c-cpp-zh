
This means you can have generic types that have both covariant and contravariant type parameters. Before you think this is theoretical and might not have practical reason, consider the fact that there are generic types frequently used with such behavior.

The Func(Of T, TResult) family of generic delegates is like this:

```vbnet
Public Delegate Function Func(Of In T, Out TResult)
(ByVal arg T) As TResult
Public Delegate Function Func(Of In T1, In T2, Out TResult)
(ByVal arg T1, ByVal arg T2) As TResult
```

You can see that they have both kinds of type parameters. With a simple console application, it is pretty easy to show the power of the generic Func delegate.

Create a console application and name it FuncExample. Add a new Pet.vb file to the project with the code in Listing 22-10.

## LISTING 22-10: Pet.vb in FuncExample

```vbnet
Public MustInherit Class Pet
Public Property NickName As String
Public Property Age As Integer
End Class

Public NotInheritable Class Dog
Inherits Pet
End Class

Public NotInheritable Class Macaw
Inherits Pet
End Class

Public NotInheritable Class Eagle
Inherits Pet
End Class
```

> Code file [Pet.vb] available for download at Wrox.com

You are going to use the Func(Of In T, Out TResult) delegate to define transformations among pets. Listing 22-11 shows the Module1.vb file implementing this.

## LISTING 22-11: Module1.vb in FuncExample

```vbnet
Option Infer On
Option Strict On

Module Module1

Dim Dogs As New List(Of Dog) From
(
    New Dog With {.NickName = "Spike", .Age = 3),
    New Dog With {.NickName = "Murray", .Age = 12),
    New Dog With {.NickName = "Peach", .Age = 2}
)

Dim Macaws As New List(Of Macaw) From
(
    New Macaw With {.NickName = "Georgey", .Age = 32),
    New Macaw With {.NickName = "Bella", .Age = 4),
    New Macaw With {.NickName = "Grey", .Age = 11}
)

Sub Main()
Dim macawsToDogs = TransformMacawTo(Macaws, AddressOf TransformMacawTo)
Dim dogsToEagles = TransformMacawTo(Macaws, AddressOf TransformMacawToEagle)
End Sub

Private Function TransformMacawTo(
ByVal pets As IEnumerable(Of Macaw),
ByVal transformation As Func(Of Macaw, Pet)) As Enumerable(Of Pet)
    Dim result As New List(Of Pet)
    For Each pet In pets
        result.Add(transformation(pet))
    Next
    Return result
End Function

Private Function TransformDogTo(
ByVal pets As IEnumerable(Of Dog),
ByVal transformation As Func(Of Dog, Pet)) As Enumerable(Of Pet)
    Dim result As New List(Of Pet)
    For Each pet In pets
        result.Add(transformation(pet))
    Next
    Return result
End Function

Private Function TransformDogTo(ByVal macaw as Macaw) As Dog
End Function

Private Function TransformToEagle(ByVal pet As Pet) As Eagle
    Return New Eagle With (.NickName = pet.NickName, .Age = pet.Age)
End Function

End Module
```

In the TransformMacawToFunction, the Func (Of Macaw, Pet) delegate is used, while the TransformDogToFunction, a Func (Of Dog, Pet) argument, is passed.

Two functions, TransformToDog and TransformToEagle, are responsible for performing the "magical cast" of pets. The following lines of code utilize variance:

```vbnet
Dim MacawToDogs = TransformMacawTo(Macaw, AddressOf TransformToDog)
Dim MacawToEagles = TransformMacawTo(Macaw, AddressOf TransformToEagle)
Dim dogToEagles = TransformToDog(Dog, AddressOf TransformToEagle)
```

In the two TransformMacaw calls, the Func (Of Macaw, Pet) arguments are substituted with Func (Of Macaw, Dog) and Func (Of Pet, Eagle). In the invocation of TransformToDog, a Func (Of Pet, Eagle) is entirely valid, strictly typed, and no type conversion magic is behind the scenes!

Why can, for example, Func (Of Dog, Pet) be substituted with Func (Of Pet, Eagle)? The fact that Func (Of Dog, Pet) is covariant in return means that you can return a derived type, named Eagle, because Eagle is a Pet. The same thinking Func (Of Dog, Pet) is contravariant in Dog, and so operation with Pet will work on Dog, Dog is derived from Pet. Therefore, Func (Of Pet, Eagle) is a good substitution for Func (Of Dog, Pet).

## Variance with Type Options

Obviously, we are not constrained to using only the existing generic types with type parameters. You can create your own generic interfaces and delegates. You can use the modifier for signifying a contravariant, and the Out modifier for a covariant type parameter. Without a modifier, the type parameter remains invariant.

For example, consider the following declarations:

```vbnet
Public Interface IOperations(Of T, U, V)
...
End Interface
Public Delegate MyDelegate(Of T, U, Out X)
(ByVal tpar as T, ByVal upar as U) As X
```

Here, X is covariant, and U and V are invariant type parameters. The compiler checks to ensure that you keep within the rules for variant type parameters. For example, in the following interface definitions, all declarations are invalid because one more covariant parameters are in positions:

```vbnet
Public Interface IOperations(Of T, U, V)
Function OutputUnsafeOp1() As T
Function OutputUnsafeOp2() As U
Function OutputUnsafeOp3() As List(Of T)
Function OutputUnsafeOp4() As Func(Of V, U)
Sub OutputUnsafeOp5(ByRef tpar As T)
Sub OutputUnsafeOp6(ByRef par As Func(Of V, U))
End Interface
```

Similarly, in the following interface definition, all operations are invalid because covariant parameters are invalid in inputs:

```vbnet
Public Interface IOperations(Of Out T, U)
Sub InputUnsafeOp1(ByVal t as T)
Function InputUnsafeOp2() As U
Function InputUnsafeOp3() As Func(Of V, U)
End
```

## Variance and Reflection

In the TransformMacawToFunction, the Func (Of Macaw, Pet) delegate is used, while the TransformDogToFunction, a Func (Of Dog, Pet) argument, is passed.

Two functions, TransformToDog and TransformToEagle, are responsible for performing the "magical cast" of pets. The following lines of code utilize variance:

```vbnet
Dim MacawToDogs = TransformMacawTo(Macaw, AddressOf TransformToDog)
Dim MacawToEagles = TransformMacawTo(Macaw, AddressOf TransformToEagle)
Dim dogToEagles = TransformToDog(Dog, AddressOf TransformToEagle)
```

In the two TransformMacaw calls, the Func (Of Macaw, Pet) arguments are substituted with Func (Of Macaw, Dog) and Func (Of Pet, Eagle). In the invocation of TransformToDog, a Func (Of Pet, Eagle) is entirely valid, strictly typed, and no type conversion magic is behind the scenes!

Why can, for example, Func (Of Dog, Pet) be substituted with Func (Of Pet, Eagle)? The fact that Func (Of Dog, Pet) is covariant in return means that you can return a derived type, named Eagle, because Eagle is a Pet. The same thinking Func (Of Dog, Pet) is contravariant in Dog, and so operation with Pet will work on Dog, Dog is derived from Pet. Therefore, Func (Of Pet, Eagle) is a good substitution for Func (Of Dog, Pet).

## Variance and Reflection

This code iterates through all generic types in System. The nested For cycle goes through the type parameters, and uses the GenericParameterAttributes property of System.Type to obtain information about variance.

```vbnet
Imports System.Reflection

Module Module1
  Sub Main()
    Dim As = GetType(Assembly)
    Dim GenericTypes = From type In As.GetTypes()
    Where type.IsGenericDefinition And type.IsPublic
    Select type
    For Each type In GenericTypes
      Console.WriteLine("{0}: {1}", type.Name)
      For Each typeParam In type.GenericParameterAttributes And GenericParameterAttributes.VarianceMask
        If (typeParam And GenericParameterAttributes.Covariant) <> 0 Then
          Console.WriteLine("{0}: covariant", typeParam.Name)
        ElseIf (typeParam And GenericParameterAttributes.Contravariant) <> 0 Then
          Console.WriteLine("{0}: contravariant", typeParam.Name)
        Else
          Console.WriteLine("{0}: invariant", typeParam.Name)
      End If
    Next
  Next
  End Sub
End Module
```
