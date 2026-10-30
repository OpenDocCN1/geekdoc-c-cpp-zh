
More examples of calling our new Swap procedure would be (assume that all the variables have already been declared):

```
Swap(ALong, BLong)      ' Swaps the two longs.
Swap(FirstDate, SecondDate) ' Swaps the two dates.
' The next statement produces a compiler error because both
' parameters must be of the same type.
Swap(ALong, FirstDate)   ' Compiler Error!
```

## Generic Classes

**Generic classes** allow you to instantiate strongly typed classes while maintaining a high degree of reusability. Let's take a look at the Swap procedure as it is declared in a class. You can code this class in two different ways. The first is to specify GenericType in the class header so the entire class will be of that type. The second is to define the methods in the classes with GenericType (just as in the previous Swap procedure header). The first example using the class header is:

```
Class GenericClass(Of GenericType)
Public Sub Swap(ByRef ItemType As GenericType, _
ByRef Item2Type As GenericType)
Dim TempType As GenericType

TempType = ItemType
ItemType = Item2Type
Item2Type = TempType
End Sub
End Class
```

To use this new class, you instantiate it and then call the method of the class:

```
Dim Number1Integer As Integer = 333
Dim Number2Integer As Integer = 444

' Instantiate the generic class.
Dim SwapIntegersGenericClass As New GenericClass(Of Integer)

' Swaps '333' with '444'.
SwapIntegersGenericClass.Swap(Number1Integer, Number2Integer)
```

You'll notice that the IDE is smart enough to know that when you have instantiated the class with a type of Integer, coding the method call prompts you for integers (Figure 10.6).

The second class example, with the methods defined as GenericType, is:

```
Class GenericClass
Public Sub Swap (Of GenericType)(ByRef ItemType As GenericType, _
ByRef Item2Type As GenericType)
Dim TempType As GenericType

TempType = ItemType
ItemType = Item2Type
Item2Type = TempType
End Sub
End Class
```

## Figure 10.6

The smart IDE prompts for the data type specified in the declaration.

```
Private Sub CalculateButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles CalculateButton.Click
' Swap integers using the generic class.
Dim Number1Integer As Integer = 333
Dim Number2Integer As Integer = 444
' Instantiate the generic class.
Dim IntegersGenericClass As New GenericClass(Of Integer)
SwapIntegersGenericClass.Swap(
Swap: SwapIntegersGenericClass.Swap
End Sub
End Class
```

## The Entire Program

```
'Project      Ch10Generics
'Programmer    Bradley/Millspaugh/Price
'Date          June 2009
'Description   A form for entering two values to
be swapped using a generic swap routine.
'              Two different generic class types are contained in
this example. One example, including the instantiation
and method calls, is commented out.
```

```
Public Class GenericsForm

Private Sub SwapButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles SwapButton.Click
' Instantiate the generic class and test using string or numeric types.
' Dim FirstValueDecimal, SecondValueDecimal As Decimal
' Dim SwapClass As New GenericClass

Dim FirstEntryString As String = FirstValueTextBox.Text
Dim SecondEntryString As String = SecondValueTextBox.Text
Try
FirstValueDecimal = Decimal.Parse(FirstEntryString)
SecondValueDecimal = Decimal.Parse(SecondEntryString)
Both fields are numeric
Dim SwapDecimalsClass As New GenericClass(Of Decimal)
SwapDecimalsClass.Swap(FirstValueDecimal, SecondValueDecimal)
SwapClass.Swap(FirstValueDecimal, SecondValueDecimal)
MessageBox.Show('First value is ' & FirstValueDecimal)
Catch ex As Exception
' Swap text values.
Dim SwapStringsClass As New GenericClass(Of String)
SwapStringsClass.Swap(FirstEntryString, SecondEntryString)
' SwapClass.Swap(FirstEntryString, SecondEntryString)
MessageBox.Show('First value is ' & FirstEntryString)
End Try
End Sub
End Class
```

```
' This is a generic class.
Class GenericClass(Of GenericType)
Public Sub Swap(ByRef Item1Type As GenericType, _
ByRef Item2Type As GenericType)
' Swap two values using a temporary location.
Dim TempType As GenericType

TempType = Item1Type
Item1Type = Item2Type
Item2Type = TempType
End Sub
End Class
```

## Generic Collections

Collections are a great way to store your variables and keep them together. One of the drawbacks with collections is that all items are stored as object type variables, so a collection can store a string, an integer, and a class object all in the same collection without any problem. Usually that is not what you want, as your collection will probably contain objects of the same object type. You can write a "generic" wrapper around the class, which guarantees that all objects in the collection are the same type.

Generic collections provide a way to define strongly typed collections where the collection type is not declared until you instantiate the class. By using generics, you will have a strongly typed collection class that can be used with any object type that you want. Just instantiate the generic collection class, specifying the type you want to use. And from then on, that collection is "locked in" to the specified type.

Just as we did earlier with generic classes, we will define our generic collection class using the "Of Type" specifier.

```
Public Class GenericCollection(Of GenericType)
Inherits CollectionBase
' Code goes here . . .
End Class
```

Inheriting from a CollectionBase class gives our new collection class some inherited properties and methods, such as Count and Clear.

A collection class will need Add, Remove, and Item methods that utilize GenericType. The complete class code listing looks like this:

```
Public Class GenericCollection(Of GenericType)
Inherits CollectionBase

Public Function Add(ByVal Value As GenericType) As Integer
' Add the passed "Value" to the inherited List.

Return List.Add(Value)
End Function
```

```
Public Sub Remove(ByVal Value As GenericType)
    ' Remove the passed "Value" from the inherited List.
    List.Remove(Value)
End Sub

Public ReadOnly Property Item(ByVal IndexInteger As Integer) As GenericType
    Get
        ' Cast the List object to the correct type and return it.
        Return CType(List.Item(IndexInteger), GenericType)
    End Get
End Property
End Class
```

Remember that some properties, like Count, were inherited from CollectionBase, so there is no need to duplicate them here.

Once you instantiate the GenericCollection class and specify a type, using GenericType, you have imposed a restriction on the class that it must use that type in its methods—wherever you use GenericType. The following code is an example of how you might use this class.

```
' Create the GenericCollection instance, and specify a type
' (in this case, String).
Dim StringCollection As New GenericCollection(Of String)

' Add two strings.
StringCollection.Add("The sky is blue.")
StringCollection.Add("The car is green.")

' The next statement will cause a compiler error (with Option Strict On),
' because it must be a String since that is how StringCollection
' was declared (in the instantiation of the GenericCollection class).
StringCollection.Add(123)
Debug.WriteLine("Our List contains " & StringCollection.Count.ToString & " _
" & items.")
```

While our generic collection example is useful, there may not be any need to create them yourself since Visual Studio includes a number of generic collections in the Systems.Collections.Generic namespace:

- List—A basic generic collection, like the GenericCollection example, using an array whose size is dynamically increased as required.
- Dictionary—A name/value collection that indexes each item with a key.
- LinkedList—A doubly linked list, where each item points to the next item in the chain.
- Queue—A first-in, first-out (FIFO) collection of objects.
- ReadOnlyCollection—A collection with a fixed set of items that can’t be changed once it’s created.
- Stack—A last-in, first-out (LIFO) collection.
