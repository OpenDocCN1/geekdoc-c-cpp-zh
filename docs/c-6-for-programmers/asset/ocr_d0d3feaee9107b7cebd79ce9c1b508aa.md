```
```text
Grade distribution:
00-09:
10-19:
20-29:
30-39:
40-49:
50-59: *
60-69: *
70-79: **
80-89: ****
90-99: **
 100: *
```
```

Fig. 8.14 | Output of the GradeBook example that stores one exam's grades in an array. (Part 2 of 2.)

```
```csharp
// Fig. 8.15: GradeBook.cs
// Grade book using an array to store test grades.
using System;

class GradeBook
{
    private int[] grades; // array of student grades

    // getter-only auto-implemented property CourseName
    public string CourseName { get; }

    // two-parameter constructor initializes
    // auto-implemented property CourseName and grades array
    public GradeBook(string name, int[] gradesArray)
    {
        CourseName = name; // set CourseName to name
        grades = gradesArray; // initialize grades array
    }

    // display a welcome message to the GradeBook user
    public void DisplayMessage()
    {
        // auto-implemented property CourseName gets the name of course
        Console.WriteLine(
            $"Welcome to the grade book for\n{CourseName}!\n");
    }

    // perform various operations on the data
    public void ProcessGrades()
    {
        // output grades array
        OutputGrades();

        // call method GetAverage to calculate the average grade
        Console.WriteLine($"\nClass average is {GetAverage():F}");
    }
```
```

Fig. 8.15 | Grade book using an array to store test grades. (Part 1 of 4.)