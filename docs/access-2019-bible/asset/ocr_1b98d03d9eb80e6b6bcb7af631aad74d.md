on). The function always returns exactly the correct calculated value, no matter where the function is used.

Within the body of a function, you specify the function's return value by assigning a value to the function's name (and, yes, it does look pretty strange to include the function's name within the function's body). You then can use the returned value as part of a larger expression. The following function calculates the square footage of a room:

```
Function SquareFeet(dHeight As Double, _
    dWidth As Double) As Double

'Assign this function's value:
SquareFeet = dHeight * dWidth

End Function
```

This function receives two parameters: dHeight and dWidth. Notice that the function's name, SquareFeet, is assigned a value within the body of the function. The function is declared as a Double data type, so the return value is recognized by the VBA interpreter as a Double.

The main thing to keep in mind about functions is that they return values. The returned value is often assigned to a variable or control on a form or report, as in these two examples:

```
dAnswer = SquareFeet(dHeight, dWidth)
```

```
Me!txtAnswer = SquareFeet(dHeight, dWidth)
```

If the function (or subroutine, for that matter) requires information (such as the Height and Width in the case of the SquareFeet function), the information is passed as arguments within the parentheses in the function's declaration.

Arguments (also called parameters) are discussed in more detail in Chapter 25.

# Working in the code window

Unlike designing a table or dropping controls in the sections of a report, a module's code pane is a very unstructured place to work. VBA code is simply text, and there aren't a lot of visual cues to tell you how to write the code or where to put particular pieces of the code. In this section, we'll describe some features of the code window and some techniques to keep your code organized and readable.

# White space

In the code already presented in this chapter, you may have noticed some indentation and some blank lines. In the programming world, this is known as white space. White space