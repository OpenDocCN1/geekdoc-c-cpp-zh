```
theData(inner) = temp
End If
Next
Next
End Sub
```

The GreaterThan parameter is a variable that holds the address of a method matching the method signature defined by the Compare delegate. The address of any method with a matching signature can be passed as a parameter to your Sort routine.

Note the use of the Invoke method, which is how a delegate is called from the code. In addition, note that the routine deals entirely with the generic System.Object data type, rather than with any specific type of data. The specific comparison of one object to another is left to the delegate routine that is passed in as a parameter.

# Implementing a Delegate Method

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