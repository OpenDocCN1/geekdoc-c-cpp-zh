
can't contain most punctuation, and can't be more than 255 characters long. Rules aside, you should pick names for your procedures that describe what they do in a way that will be obvious to you when you read them later. Procedure names like GetData() will likely be hard to understand later, but ReadDataFromEmployeeTable() will be crystal clear. You probably don't want to push the 255-character limit on procedure names, but don't be afraid to make long, descriptive names.

## Variable declaration

The first statement in our simple subprocedure is a variable declaration statement. It starts with the Dim keyword, which is short for dimension. The variable's name, lNumber, comes next. Variable names follow the same rules as procedure names, described in the previous section. The As keyword follows the name, which is followed by the data type. In this case, lNumber was declared as a Long Integer data type.

Variables and data types are discussed extensively in Chapter 25.

Variables hold data that you can use later in your procedure. When you declare a variable with the Dim keyword, you're telling VBA to reserve a spot in the computer's memory to store that data. The amount of memory that VBA will reserve depends on the data type. In this example, you told VBA to hold enough memory to store a Long Integer, or 32 bits of memory.

The As datatype portion of the variable declaration statement is optional. You could declare lNumber with the statement:

```
Dim lNumber
```

When you omit the data type, VBA will determine an appropriate data type when you assign a value to the variable. That may seem like a handy service VBA is providing, but it's not a very good practice. VBA will assign a data type to the variable based on the first time you use it, but it doesn't know all the plans you have in mind for that variable. It may end up assigning a data type that's too small for what you need. Having VBA assign data types is also slower than if you assign them as you write the code.

TIP
If you're new to VBA, don't get too hung up on which data type to use for your variables. Use String for text, Long for numbers without decimals, Double for numbers with decimals, and Boolean for true/false values. You can get a lot done with just those four data types.

## Variable assignment

By declaring a variable with the Dim statement, you've reserved a place in memory where you can store data for later use. The next line in the procedure stores the number 2 in the variable lNumber. Here's what that line looks like in the procedure:

```
lNumber = 2
```

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

## Working in the code window

Unlike designing a table or dropping controls in the sections of a report, a module's code pane is a very unstructured place to work. VBA code is simply text, and there aren't a lot of visual cues to tell you how to write the code or where to put particular pieces of the code. In this section, we'll describe some features of the code window and some techniques to keep your code organized and readable.

## White space

In the code already presented in this chapter, you may have noticed some indentation and some blank lines. In the programming world, this is known as white space. White space
consists of spaces, tabs, and blank lines. With very few exceptions, VBA ignores white space. The following two procedures are identical as far as the VBA compiler is concerned:

```
Function BMI(dPounds As Double, lHeight As Long) As Double

    BMI = dPounds / (lHeight ^ 2) * 703

End Function
```

```
Function BMI(dPounds As Double, lHeight As Long) As Double
BMI = dPounds / (lHeight ^ 2) * 703
End Function
```

In the first function, a blank line was inserted after the Function statement, and another blank line was inserted before the End Function statement. Also, a tab was inserted before the single statement within the procedure. All the white space elements were removed in the second function. Despite the difference in appearance, the VBA compiler reads the two functions identically, and the two functions return the same result.

In some programming languages, white space is important and meaningful. That isn't the case for VBA. The purpose of white space is to make your code more readable. Different programmers format their code with white space in different ways. Whatever formatting conventions you choose to use, the most important thing is to be consistent. Consistency in formatting will help you read and understand your code more easily, even if you're reading months or years later.

## Line continuation

The VBE window can expand to be as wide as your screen. Sometimes your statements are so long that they extend beyond the window even when it's as wide as it can be. VBA provides a way to continue the current line onto the next line. When used with long statements, this can help make your code more readable. The line continuation characters are a space followed by an underscore. When the VBA compiler sees a space and an underscore at the end of the line, it knows that the next line is a continuation of the current one. Figure 24.4 shows a simple procedure with one very long statement. The statement extends beyond the code pane window, and you must scroll to read it.

Use the line continuation characters to break the long statement into multiple lines. This will allow you to see the whole statement. The statement in Figure 24.4 could be rewritten as the following statement:

```
Function GetDateFooter() As String

    GetDateFooter = "This report was printed on " & _
        & Format(Now, "dd-mmm-yyyy") & _
        " and changes made to the data after that " & _
        "date won't be reflected."

End Function
```

## **FIGURE 24.4**

A long statement extends beyond the code window.

![](img/1e45673ab6eca9d20e67635ff5b9b318_815_0.png)

The underscore is typically referred to as the line continuation character, but the space that comes before it is equally important. You need both characters, space and underscore, to continue a line. The line continuation character can't be used in the middle of a string. Notice in the preceding example that the long string is broken up into four smaller strings and concatenated together with ampersands. To spread a long string over multiple lines, it must be broken up so that the line continuation character can be used.

## Multi-statement lines

Another way to improve the readability of your code is by putting two or more statements on one line. VBA uses the colon to separate statements on the same line. If you have a lot of short statements that are taking up a lot of vertical space in the code pane, you can put a few of them on the same line to clean up the code. In the following example, many similar statements are grouped together:

```
i = 12: j = 45: k = 32
l = 87: m = 77: n = 2
o = 89: p = 64: q = 52
```

Those nine statements are assigning numbers to nine different variables. If they were written out one after the other, they would eat up a lot of the code window. By putting three statements on each line, less space is wasted. This technique is useful when you have small
