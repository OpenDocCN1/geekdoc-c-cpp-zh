Each of these statements has the ability not only to call another method, the preferred way to manage blocks of code, but also to literally encapsulate a block of code. Note that the variables declared within the context of a conditional statement (between the If and End If lines) are only visible up until the End If statement. After that, these variables go out of scope. The concept of scoping is discussed in more detail later in this chapter.

# If Then

The conditional is one of two primary programming constructs (the other being the loop) that is present in almost every programming language. After all, even in those rare cases where the computer is just repeatedly adding values or doing some other repetitive activity, at some point a decision is needed and a condition evaluated, even if the question is only “is it time to stop?” Visual Basic supports the If-Then statement as well as the Else statement; — and unlike some languages, the concept of an ElseIf statement. The ElseIf and Else statements are totally optional, and it is not only acceptable but common to use conditionals that do not utilize either of these code blocks. The following example illustrates a simple pair of conditions that have been set up serially:

```
If i > 1 Then
    'Code A1
ElseIf i < 1 Then
    'Code B2
Else
    'Code C3
End If
```

If the first condition is true, then code placed at marker A1 is executed. The flow would then proceed to the End If, and the program would not evaluate any of the other conditions. Note that for best performance, it makes the most sense to have your most common condition first in this structure, because if it is successful, none of the other conditions need to be tested.

If the initial comparison in the preceding example code were false, then control would move to the first Else statement, which in this case happens to be an ElseIf statement. The code would therefore test the next conditional to determine whether the value of i were less than 1. If so, then the code associated with block B2 would be executed.

However, if the second condition were also false, then the code would proceed to the Else statement, which isn’t concerned with any remaining condition and just executes the code in block C3. Not only is the Else optional, but even if an ElseIf is used, the Else condition is still optional. It is acceptable for the Else and C3 block to be omitted from the preceding example.

# Comparison Operators

There are several ways to discuss what is evaluated in an If statement. Essentially, the code between the If and Then portions of the statement must eventually evaluate out to a Boolean. At the most basic level, this means you can write If True Then, which results in a valid statement, although the code would always execute the associated block of code with that If statement. The idea, however, is that for a basic comparison, you take two values and place between them a comparison operator. Comparison operators include the following symbols: =, >, <, >=, <=.

Additionally, certain keywords can be used with a comparison operator. For example, the keyword Not can be used to indicate that the statement should consider the failure of a given comparison as a reason to execute the code encapsulated by its condition. An example of this is shown in the next example:

```
If Not i = 1 Then
    'Code A1
End If
```

It is therefore possible to compare two values and then take the resulting Boolean from this comparison and reevaluate the result. In this case, the result is only reversed, but the If statement supports more