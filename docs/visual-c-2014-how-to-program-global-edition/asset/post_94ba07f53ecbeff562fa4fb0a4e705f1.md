
## 8.9 Multidimensional Arrays

```csharp
// loop through each element in current row
foreach (var element in row)
{
    Console.Write($"{element}");
}
Console.WriteLine(); // start new line of output
```

Values in the rectangular array by row are
1 2 3
4 5 6

Values in the jagged array by row are
1 2
3
4 5 6

## Overloaded Method OutputArray

Method OutputArray is overloaded. The first version (lines 27–42) specifies the array parameter as int[], to indicate that it takes a rectangular array. The second version (lines 45–60) takes a jagged array, because its array parameter is listed as int[][] array.

## Method OutputArray for Rectangular Arrays

Line 21 invokes method OutputArray with argument rectangular, so the version of OutputArray at lines 27–42 is called. The nested for statement (lines 32–41) outputs the rows of a rectangular array. The loop-continuation condition of each statement (lines 32 and 35) uses the rectangular array's GetLength method to obtain the length of each dimension. Dimensions are numbered starting from 0, so the method GetLength(0) returns the size of the first dimension of the array (the number of rows), and the call GetLength(1) returns the size of the second dimension (the number of columns). A for statement can iterate through all the rows and columns in a rectangular array. In this case, foreach iterates through the rows and columns starting from 0, as if the elements were in a one-dimensional array.

## Method OutputArray for Jagged Arrays

Line 23 invokes method OutputArray with argument jagged, so OutputArray at lines 45–60 is called. The nested for statement (lines 50–59) outputs the rows of a jagged array. The inner for statement iterates through each element in the current row. This allows the loop to determine the exact number of columns in each row. Since the jagged array is created as an array of arrays, we can use nested for statements to output the elements in the console window. The outer loop iterates through the elements of array, which are references to int values that represent each row. The inner loop iterates through the elements of the current row.

## Chapter 8 Arrays; Introduction to Exception Handling

### Common Multidimensional-Array Manipulations Performed with for Statements

Many common array manipulations use for statements. As an example, the following for statement sets all the elements in row 2 of rectangular array a in 8.17 to 0:

```csharp
for (int column = 0; column < a.GetLength(1); ++column)
  a[2, column] = 0;
```

We specified 2; therefore, we know that the first index is always 2 (0 is the first row, and 1 is the second row). This loop varies only the second index (i.e., the column in-). The preceding for statement is equivalent to the assignment statements

```csharp
a[2, 0] = 0;
a[2, 1] = 0;
a[2, 2] = 0;
a[2, 3] = 0;
```

The following nested statement for the values of all the elements in array a:

```csharp
for (int row = 0; row < a.GetLength(0); ++row)
  for (int column = 0; column < a.GetLength(1); ++column)
    total += a[row, column];
```

These nested statements total the array elements one row at a time. The outer for statement begins setting the row index to 0 so that row 0's elements can be totaled by the inner for statement. The outer for then increments row to 1 so that row 1's elements can be totaled. Then the outer for increments row to 2 so that row 2's elements can be totaled. The variable total can be displayed when the outer for statement terminates. In the next example, we show how to process a rectangular array in a more concise manner using foreach statements.

## 8.10 Case Study: GradeBook Using a Rectangular Array

In Section 8.8, we presented class GradeBook (Fig. 8.15), which uses a one-dimensional array to store grades on a single exam. In most courses, students take several exams. Instructors are likely to want to analyze grades the entire course, both for a single student and for the class as a whole.

### Storing Student Grades in a Rectangular Array in Class GradeBook

Figure 8.21 shows a version of GradeBook that uses a rectangular array to store the grades of a number of students on multiple exams. Each row of the array represents a single student's grades for the entire course, and each column represents the grades for the class on one of the exams students took during the course. An app as GradeBookTest (Fig. 8.22) passes the array as an argument to the GradeBook constructor. In this example, we use a 10-3 array containing 10 students' grades on three exams.

Welcome to the grade book for
CS101 Introduction to C# Programming!

The grades are:

| Student | Test 1 | Test 2 | Test 3 | Average |
| --- | --- | --- | --- | --- |
| 1 | 87 | 96 | 70 | 84.33 |
| 2 | 68 | 87 | 90 | 81.67 |
| 3 | 94 | 100 | 90 | 94.67 |
| 4 | 100 | 81 | 82 | 87.67 |
| 5 | 82 | 65 | 85 | 77.67 |
| 6 | 78 | 87 | 65 | 76.67 |
| 7 | 85 | 75 | 83 | 81.00 |
| 8 | 91 | 94 | 100 | 95.00 |
| 9 | 76 | 72 | 84 | 77.33 |
| 10 | 87 | 93 | 73 | 84.33 |

Lowest grade in the grade book is 65
Highest grade in the grade book is 100

Overall grade distribution:
00-09:
10-19:
20-29:
30-39:
40-49:
50-59:
60-69:
70-79:
80-89:
90-99:
100:

```csharp
using System;

class GradeBook
{
    private int[,] grades;
    public string GradeName { get; }

    public GradeBook(string name, int[,] gradesArray)
    {
        GradeName = name;
        grades = gradesArray;
    }

    public void displayMessage()
    {
        Console.WriteLine($"Welcome to the grade book for {GradeName}!");
    }

    public void ProcessGrades()
    {
        Console.WriteLine($"Highest grade in the grade book is {GetMaximum()}");
        Console.WriteLine($"Lowest grade in the grade book is {GetMinimum()}");
        OutputChart();
    }

    public int GetMinimum()
    {
        int lowGrade = grades[0, 0];
        foreach (var grade in grades)
        {
            if (grade < lowGrade)
            {
                lowGrade = grade;
            }
        }
        return lowGrade;
    }

    public int GetMaximum()
    {
        int highGrade = grades[0, 0];
        foreach (var grade in grades)
        {
            if (grade > highGrade)
            {
                highGrade = grade;
            }
        }
        return highGrade;
    }

    public double getAverage(int student)
    {
        int gradeCount = grades.GetLength(1);
        double total = 0.0;
        for (var exam = 0; exam < gradeCount; ++exam)
        {
            total += grades[student, exam];
        }
        return total / gradeCount;
    }

    public void OutputChart()
    {
        Console.WriteLine("Overall grade distribution:");
        int[] frequency = new int[11];
        for (int student = 0; student < grades.GetLength(0); ++student)
        {
            for (int exam = 0; exam < grades.GetLength(1); ++exam)
            {
                int grade = grades[student, exam];
                if (grade == 100) frequency[10]++;
                else frequency[grade / 10]++;
            }
        }
        for (int i = 0; i < 10; ++i)
        {
            Console.WriteLine($"{i * 10}-{(i * 10) + 9}: {frequency[i]}");
        }
        Console.WriteLine($"100: {frequency[10]}");
    }
}
```
