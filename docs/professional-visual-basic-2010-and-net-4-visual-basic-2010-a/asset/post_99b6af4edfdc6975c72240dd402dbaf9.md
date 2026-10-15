
It is easy enough to write a sort routine that sorts Person objects by name, or to write a sort routine that sorts SalesOrder objects by sales date. However, if you want to write a sort routine that can sort any type of object based on arbitrary sort criteria, that gets pretty difficult. At the same time, because some sort routines can get very complex, it would be nice to reuse that code without having to copy and paste it for each different sort scenario.

By using delegates, you can create such a generic routine for sorting; and in so doing, you can see how delegates work and can be used to create many other types of generic routines. The concept of a delegate formalizes the process of declaring a routine to be called and calling that routine.

> The underlying mechanism used by the .NET environment for callback methods is the delegate. Visual Basic uses delegates behind the scenes as it implements the Event, RaiseEvent, WithEvents, and Handles keywords.

## Declaring a Delegate

In your code, you can declare what a delegate procedure must look like from an interface standpoint. This is done using the Delegate keyword. To see how this works, let’s create a routine to sort any kind of data.

To do this, you will declare a delegate that defines a method signature for a method that compares the value of two objects and returns a Boolean indicating whether the first object has a larger value than the second object. You will then create a sort algorithm that uses this generic comparison method to sort data. Finally, you create an actual method that implements the comparison, and then you pass the method’s address to the sort routine.

Add a new module to the project by choosing Project Add Module. Name the module Sort.vb, click Add, and then add the following code:

```
Module Sort
    Public Delegate Function Compare(ByVal v1 As Object, ByVal v2 As Object) _
        As Boolean
End Module
```

Code snippet from Sort

This line of code does something interesting. It actually defines a method signature as a data type. This new data type is named Compare, and it can be used within the code to declare variables or parameters that are accepted by your methods. A variable or parameter declared using this data type could actually hold the address of a method that matches the defined method signature, and you can then invoke that method by using the variable.

Any method with the following signature can be viewed as being of type Compare:

```
f(Object, Object)
```

## Using the Delegate Data Type

You can write a routine that accepts the delegate data type as a parameter, meaning that anyone calling your routine must pass the address of a method that conforms to this interface. Add the following sort routine to the code module Sort:

```
Public Sub DoSort(ByVal theData() As Object, ByVal greaterThan As Compare)
    Dim outer As Integer
    Dim inner As Integer
    Dim temp As Object

    For outer = 0 To UBound(theData)
    For inner = outer + 1 To UBound(theData)
        If greaterThan.Invoke(theData(outer), theData(inner)) Then
        temp = theData(outer)
        theData(outer) = theData(inner)
        theData(inner) = temp
        End If
    Next
    Next
End Sub
```

The GreaterThan parameter is a variable that holds the address of a method matching the method signature defined by the Compare delegate. The address of any method with a matching signature can be passed as a parameter to your Sort routine.

Note the use of the Invoke method, which is how a delegate is called from the code. In addition, note that the routine deals entirely with the generic System.Object data type, rather than with any specific type of data. The specific comparison of one object to another is left to the delegate routine that is passed in as a parameter.

## Implementing a Delegate Method

Now create the implementation of the delegate routine and call the sort method. On a very basic level, all you need to do is create a method that has a matching method signature, add the following code to your Sort module:

```
Public Function PersonCompare(ByVal person1 As Object, _
    ByVal person2 As Object) As Boolean

End Function
```

The method signature of this method exactly matches what you defined by your delegate earlier:

```
Compare(Object, Object)
```

In both cases, you are defining two parameters of type Object.

Of course, there is more to it than simply creating the stub of a method. The method needs to return a value of True if its first parameter is greater than the second parameter. Otherwise, it should be written to deal with some specific type of data.

The Delegate statement defines a data type based on a specific method interface. To call a routine that expects a parameter of this new data type, it must pass the address of a method that conforms to the defined interface.

To conform to the interface, a method must have the same number of parameters with the same data types defined in your Delegate statement. In addition, the method must provide the same return type as defined. The actual name of the method does not matter; it is the number, order, and data type of the parameters and the return value that count.

To find the address of a specific method, you can use the AddressOf operator. This operator returns the address of any procedure or method, enabling you to pass that value as a parameter to any routine that expects a delegate as a parameter.

The Person class already has a shared method named CompareAge that generally does what you want. Unfortunately, it accepts parameters of type Person, rather than of type Object as required by the Compare delegate. You can use method overloading to solve this problem.

Create a second implementation of CompareAge that accepts parameters of type Object as required by the delegate, rather than of type Person as shown in the existing implementation:

```
Public Shared Function CompareAge(ByVal person1 As Object, _
    ByVal person2 As Object) As Boolean

    Return CType(person1, Person).Age > CType(person2, Person).Age

End Function
```

This method simply returns True if the first Person object’s age is greater than the second. The routine accepts two Object parameters, rather than specific Person type parameters, so you have to use the CType method to access those objects as type Person. You accept the parameters as type Object because that is what is defined by the Delegate statement. You are matching its method signature:

```
f(Object, Object)
```

Because this method’s parameter data types and return value match the delegate, you can use it when calling the Sort routine. Place a button on the Form1 form and write the following code behind that button:

```vb
Private Sub Button2_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles button2.Click

    Dim myPeople(4) As Person

    myPeople(0) = New Person("Fred", #7/9/1960#)
    myPeople(1) = New Person("Mary", #1/21/1955#)
    myPeople(2) = New Person("Sarah", #2/1/1960#)
    myPeople(3) = New Person("George", #5/13/1970#)
    myPeople(4) = New Person("Andre", #10/1/1965#)

    DoSort(myPeople, AddressOf Person.CompareAge)
End Sub
```

This code creates an array of Person objects and populates them. It then calls the DoSort routine from the module, passing the array as the first parameter, and the address of the shared CompareAge method as the second parameter. To display the contents of the sorted array in the IDE’s output window, you can add the following code:

```vb
Private Sub button2_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles button2.Click

    Dim myPeople(4) As Person

    myPeople(0) = New Person("Fred", #7/9/1960#)
    myPeople(1) = New Person("Mary", #1/21/1955#)
    myPeople(2) = New Person("Sarah", #2/1/1960#)
    myPeople(3) = New Person("George", #5/13/1970#)
    myPeople(4) = New Person("Andre", #10/1/1965#)

    DoSort(myPeople, AddressOf Person.CompareAge)
    Dim myPerson As Person
    For Each myPerson In myPeople
        System.Diagnostics.Debug.WriteLine(myPerson.Name & " " & myPerson.Age)
    Next
End Sub
```

When you run the application and click the button, the output window displays a list of the people sorted by age, as shown in Figure 2-16.

What makes this so powerful is that you can change the comparison routine without changing the sort mechanism. Simply add another comparison routine to the Person class:

```vb
Public Shared Function CompareName(ByVal person1 As Object, _
    ByVal person2 As Object) As Boolean

    Return CType(person1, Person).Name > CType(person2, Person).Name

End Function
```

![](img/d99870e80390742f93963da7be0b2e61_153_0.png)
