# 5.7 Student Class: Nested if...else Statements

+   - The second operand (between the ? and :) is the value of the conditional expression if the bool expression is true.
- The third operand (to the right of the : ) is the value of the conditional expression if the bool expression is false.

For now, the second and third operands should have the same type. In Section 7.6, we'll discuss implicit conversions that may occur if these operands do not have the same type. For example,

```
Console.WriteLine(studentGrade >= 60 ? "Failed");
```

displays the value of WriteLine's conditional-expression argument. The conditional expression in the preceding statement evaluates to the string "Passed" if the condition

studentGrade >= 60
is true the string "Failed" if it's false. Thus, with the conditional operator performs essentially the same task as the first if...else statement shown in Section 5.6. The precedence of the conditional operator is low, so the entire expression is normally placed in parentheses. We will see that conditional expressions can be used in situations where if...else statements cannot.

# 5.7 Student Class: Nested if...else Statements

The example of 5.5–5.6 demonstrates a nested if...else statement that determines a student's letter grade based on the student's average in a course.

Class Student
Class Student (Fig. 5.5) stores a student's name and average and provides properties for mapping these values. The class contains:

+   - Auto-implemented string property Name (line 7) to store a Student's name.
- Instance variable of type int (line 8) to store a Student's average in a course and the corresponding Average property (lines 18–36) to get and set the Student's average. Average's setter uses nested if (lines 28–34) to validate the value that's assigned to the property. These statements ensure that the value is greater than 0 and less than equal to 100; otherwise, instance variable average is left unchanged. If each statement contains a simple condition—i.e., one that makes a single test. In Section 6.11, you'll see how to use logical operators to write compound conditions that conveniently combine simple conditions. If the condition in line 28 is true, then only the condition in line 30 will be tested, and only if the condition in both lines 28 and 30 are true will the statement in line 32 execute.
- Constructor (lines 11–15) that sets the Name and Average properties.
- Read-only property LetterGrade (lines 39–68), which uses nested if...else statement to determine the student's letter grade based on the student's average. A read-only property provides only a get accessor. Note that the local letterGrade is initialized to string.Empty (line 43), which represents the empty string (that is, a string containing no characters).