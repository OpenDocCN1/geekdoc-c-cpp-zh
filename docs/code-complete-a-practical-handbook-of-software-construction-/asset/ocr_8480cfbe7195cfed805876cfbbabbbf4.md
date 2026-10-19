This is an ugly range for a table lookup because you can’t use a simple data-transformation function to key into the letters A through F. An index scheme would be awkward because the numbers are floating point. You might consider converting the floating-point numbers to integers, and in this case that would be a valid design option, but for the sake of illustration, this example will stick with floating point.

To use the stair-step method, you put the upper end of each range into a table and then write a loop to check a score against the upper end of each range. When you find the point at which the score first exceeds the top of a range, you know what the grade is. With the stair-step technique, you have to be careful to handle the endpoints of the ranges properly. Here’s the code in Visual Basic that assigns grades to a group of students based on this example:

```
**Visual Basic Example of a Stair-Step Table Lookup**

```vb
' set up data for grading table
Dim rangeLimit() As Double = { 50.0, 65.0, 75.0, 90.0, 100.0 }
Dim grade() As String = { "F", "D", "C", "B", "A" }
maxGradeLevel = grade.Length - 1
...

' assign a grade to a student based on the student's score
gradeLevel = 0
studentGrade = "A"
While ( studentGrade = "A" ) and ( gradeLevel < maxGradeLevel )
    If ( studentScore < rangeLimit( gradeLevel ) ) Then
        studentGrade = grade( gradeLevel )
    End If
    gradeLevel = gradeLevel + 1
Wend
```
```

Although this is a simple example, you can easily generalize it to handle multiple students, multiple grading schemes (for example, different grades for different point levels on different assignments), and changes in the grading scheme.

The advantage of this approach over other table-driven methods is that it works well with irregular data. The grading example is simple in that, although grades are assigned at irregular intervals, the numbers are “round,” ending with 5s and 0s. The stair-step approach is equally well suited to data that doesn’t end neatly with 5s and 0s. You can use the stair-step approach in statistics work for probability distributions with numbers like this:

| Probability | Insurance Claim Amount |
|---:|---:|
| 0.458747 | $0.00 |
| 0.547651 | $254.32 |
| 0.627764 | $514.77 |
| 0.776883 | $747.82 |
| 0.893211 | $1,042.65 |