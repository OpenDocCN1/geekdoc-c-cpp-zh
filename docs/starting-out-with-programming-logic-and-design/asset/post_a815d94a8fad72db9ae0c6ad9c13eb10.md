
# Appendix C Pseudocode Reference 595

Case value_2:
statement
statement
etc. These statements are executed if the testExpression is equal to value_2.

Insert as many Case sections as necessary

Case value_N:
statement
statement
etc. These statements are executed if the testExpression is equal to value_N.

Default:
statement
statement
etc. These statements are executed if the testExpression is not equal to any of the values listed after the Case statements.

End Select This is the end of the structure.

The first line of the structure starts with the Select statement, followed by a testExpression. Inside the structure there are one or more blocks of statements that begin with a Case statement. Notice that the Case word is followed by a value.

When the Case statement executes, it compares the value with the values that follow each of the Case statements (from top to bottom). If it finds a value that matches the testExpression's value, the program branches to the Case statement. The statements that immediately follow the Case statement are executed, and then the program jumps out of the structure. If the testExpression does not match any of the Case values, the program branches to the Default statement and executes the statements that immediately follow it. Here is an example:

```
Select month
Case 1:
Display "January"
Case 2:
Display "February"
Case 3:
Display "March"
Default:
Display "Error: Invalid month"
End Select
```

# The While Loop

General format:

While condition
statement
statement
etc. These statements are the body of the loop. They are repeated while the condition is true.

End While

In the general format, the condition is a Boolean expression, and the statements that appear on the lines between the While and the End clauses are the body of the loop. When the loop executes, the condition is tested. If it is true, the statements that appear in the body of the loop are executed, and then the loop starts over. If the condition is false, the program exits the loop. The following pseudocode shows an example:

```
Set count = 0
While count < 10
Display count
Set count = count + 1
End While
```

# The Do-While Loop

General format:

```
Do
statement
statement
etc.
While condition
```

> These statements are the body of the loop. They are always performed once, and then repeated while the condition is true.

In the format, the statements that appear in the lines between the Do and While are the body of the loop. The condition that appears after the While clause is a Boolean expression. When the loop executes, the statements in the body of the loop are executed, and then the condition is tested. If the condition is true, the loop starts over and the statements in the body are executed again. If the condition is false, the program exits the loop. Here is an example:

```
Set count = 10
Do
Display count
Set count = count - 1
While count > 0
```

# The Do-Until Loop

General format:

```
Do
statement
statement
etc.
Until condition
```

> These statements are the body of the loop. They are always performed once, and then repeated until the condition is true.

In the format, the statements that appear in the lines between the Do and Until are the body of the loop. The condition that appears after the While clause is a Boolean expression. When the loop executes, the statements in the body of the loop are executed, and then the condition is tested. If the condition is true, the program exits the loop. If the condition is false, the loop starts over and the statements in the body are executed again. Here is an example:

```
Set count = 10
Do
Display count
Set count = count - 1
Until count == 0
```

# The For Loop

General format:

```
For counterVariable = startingValue To maxValue
statement
statement // These statements are the body of the loop.
statement
etc.
End For
```

In the general format, counterVariable is the name of a variable that is used as a counter, startingValue is the value of the counter that will be initially set to, and maxValue is the maximum value that the counter can contain. When the loop executes, the following actions are performed:

1. The counter is set to the startingValue.
2. The counter is compared to the maxValue. If the counterVariable is greater than maxValue, the loop stops. Otherwise:
   a. the statements that appear in the body of the loop are executed.
   b. the counter is incremented.
   c. the loop starts over again at step 2.

Here is an example:

```
For counter = 1 To 10
Display "Hello world"
End For
```

# The For Each Loop

General format:

```
For Each var In array
statement
statement
statement
etc.
End For
```

In the general format, var is the name of a variable and array is the name of an array. The loop will iterate once for every element in the array. Each time the loop iterates, it copies an element to the var variable. For example, the first time the loop iterates, var will contain the value of array[0], the second time the loop iterates will contain the value of array[1], and so forth. This continues until the loop has stopped through all elements of the array. The following pseudocode shows an example:

```
Constant INTEGER SIZE = 5
Declare Integer numbers[SIZE] = 5, 10, 15, 20, 25
Declare Integer num
For Each num In numbers
Display num
End For
```

# Defining a Module

To create a module, it has two parts: header and a body. The header indicates the module name, the body contains the statements that are executed when the module is called. Here is the general format:

```
Module ModuleName
statement
etc.
```

# Calling a Module

To call a module, you use the Call statement. Here is the general format:

```
Call ModuleName
```

# Parameter Variables

If you want a module or function to receive arguments, they are declared inside parentheses. To pass an argument by value, the name is used. To pass an argument by reference, the word ref is used in the parameter declaration.

```
Module ModuleName(ref value)
statement
etc.
```

# Defining a Function

A function is similar to a module, but it must have a Return statement. This causes a value to be sent back to the part of the program that called it. The general format is:

```
Function DataType FunctionName(ParameterList)
statement
etc.
Return value
```

The value that follows Return is the value that the function will send back. Here is an example:

```
Function sum(Integer num1, Integer num2)
Declare Integer result
Set result = num1 + num2
Return result
```

# Opening an Output File and Writing Data to it

In our pseudocode, we first declare an Output variable, and then we use the Open statement to open the file. Here is an example:

```
Declare OutputFile customerFile
Open customerFile "customers.dat"
```

We use the Write statement to write data to the file. Here is an example:

```
Write customerFile "Charles Pace"
```

When writing to the file, we use the Close statement to close the file. Here is an example:

```
Close customerFile
```

# Opening an Input File and Reading Data from it

In our pseudocode, we first declare an InputFile variable, and then we use the Open statement to open the file. Here is an example:

```
Declare InputFile inventoryFile
Open inventoryFile "inventory.dat"
```

We use the Read statement to read data from the file. Here is an example:

```
Read inventoryFile itemName
```

This statement reads an item from the file and stores it in the itemName variable. When finished reading file, we use the Close statement to close the file. Here is an example:

```
Close inventoryFile
```
