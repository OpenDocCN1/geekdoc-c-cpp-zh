A class consists of both state and behavior. State is a fancy way of referring to the fact that the class has one or more values also known as properties associated with it. Embedded in the class definition are zero or more Dim statements that create variables used to store the properties of the class. When you create an instance of this class, you create these variables; and in most cases the class contains logic to populate them. The logic used for this, and to carry out other actions, is the behavior. This behavior is encapsulated in what, in the object-oriented world, are known as methods.

However, Visual Basic doesn’t have a “method” keyword. Instead, it has two other keywords that are brought forward from Visual Basic’s days as a procedural language. The first is Sub. Sub, short for “subroutine,” and it defines a block of code that carries out some action. When this block of code completes, it returns control to the code that called it without returning a value. The following snippet shows the declaration of a Sub:

```
Private Sub Load(ByVal object As System.Object)

End Sub
```

The preceding example shows the start of a Sub called Load. For now you can ignore the word `Private` at the start of this declaration; this is related to the object and is further explained in the next chapter. This method is implemented as a Sub because it doesn’t return a value and accepts one parameter when it is called. Thus, in other languages this might be considered and written explicitly as a function that returns Nothing.

The preceding method declaration for Sub Load also includes a single parameter, object, which is declared as being of type `System.Object`. The meaning of the `ByVal` qualifier is explained in chapter 2, but is related to how that value is passed to this method. The code that actually loads the object would be written between the line declaring this method and the End Sub line.

Alternatively, a method can return a value; Visual Basic uses the keyword `Function` to describe this behavior. In Visual Basic, the only difference between a Sub and the method type Function is the return type.

The Function declaration shown in the following sample code specifies the return type of the function as a Long value. A Function works just like a Sub with the exception that a Function returns a value, which can be Nothing. This is an important distinction, because when you declare a function the compiler expects it to include a Return statement. The Return statement is used to indicate that even though additional lines of code may remain within a Function or Sub, those lines of code should not be executed. Instead, the Function or Sub should end processing at the current line, and if it is a function, the return value should be returned. To declare a Function, you write code similar to the following:

```
Public Function Add(ByVal ParamArray values() As Integer) As Long
    Dim result As Long = 0
    'TODO: Implement this function
    Return result
    'What if there is more code
    Return result
End Function
```

In the preceding example, note that after the function initializes the second line of code, there is a Return statement. There are two Return statements in the code. However, as soon as the first Return statement is reached, none of the remaining code in this function is executed. The Return statement immediately halts execution of a method, even from within a loop.

As shown in the preceding example, the function’s return value is assigned to a local variable until returned as part of the Return statement. For a Sub, there would be no value on the line with the Return statement, as a Sub does not return a value when it completes. When returned, the return value is usually assigned to something else. This is shown in the next example line of code, which calls a function to retrieve the currently active control on the executing Windows Form:

```
Dim ctrl = Me.Add(1, 2)
```

The preceding example demonstrates a call to a function. The value returned by the function Add is a Long, and the code assigns this to the variable ctrl. It also demonstrates another keyword that you should be aware of: Me. The Me keyword is how, within an object, that you can reference the current instance of that object.