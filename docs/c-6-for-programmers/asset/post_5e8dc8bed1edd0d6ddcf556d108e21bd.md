
then the method call

```csharp
ModifyArray(hourlyTemperatures);
```

passes the reference of array `hourlyTemperatures` to method `ModifyArray`. Every array object "knows" its own length (and makes it available via its `Length` property). Thus, when we pass an array object’s reference to a method, we need not pass the array length as an additional argument.

### Specifying an Array Parameter

For a method to receive an array reference through a method call, the method’s parameter list must specify an array parameter. For example, the method header for method `ModifyArray` might be written as

```csharp
void ModifyArray(double[] b)
```

indicating that `ModifyArray` receives the reference of an array of doubles in parameter `b`. The method call passes array `hourlyTemperatures`’ reference, so when the called method uses the array variable `b`, it refers to the same array object as `hourlyTemperatures` in the calling method.

### Pass-By-Value vs. Pass-By-Reference

When an argument is an entire array or an individual array element of a reference type, the called method receives a copy of the reference. However, when an argument to a method is an individual array element of a value type, the called method receives a copy of the element’s value. To pass an individual array element to a method, use the indexed name of the array as an argument (e.g., `hourlyTemperatures[2]`). If you want to pass a value-type array element to a method by reference, you must use the `ref` keyword as shown in Section 7.18.

### Passing an Entire Array vs. Passing a Single Array Element

Figure 8.13 demonstrates the difference between passing an entire array and passing a value-type array element to a method. The `foreach` statement at lines 16–19 outputs the five `int` elements of `array`. Line 21 invokes method `ModifyArray`, passing `array` as an argument. Method `ModifyArray` (lines 38–44) receives a copy of `array`’s reference and uses the reference to multiply each of `array`’s elements by 2. To prove that `array`’s elements (in `Main`) were modified, the `foreach` statement at lines 25–28 outputs the five elements of `array` again. As the output shows, method `ModifyArray` doubled the value of each element.

```csharp
// Fig. 8.13: PassArray.cs
// Passing arrays and individual array elements to methods.
using System;

class PassArray
{
    // Main creates array and calls ModifyArray and ModifyElement
    static void Main()
    {
        int[] array = {1, 2, 3, 4, 5};

        Console.WriteLine("Effects of passing reference to entire array:");
        Console.WriteLine("The values of the original array are:");

        // output original array elements
        foreach (var value in array)
        {
            Console.Write($"{value,5}");
        }

        ModifyArray(array); // pass array reference
        Console.WriteLine("\n\nThe values of the modified array are:");

        // output modified array elements
        foreach (var value in array)
        {
            Console.Write($"{value,5}");
        }

        Console.WriteLine("\n\nEffects of passing array element value:\n" +
            $"array[3] before ModifyElement: {array[3]}");

        ModifyElement(array[3]); // attempt to modify array[3]
        Console.WriteLine($"array[3] after ModifyElement: {array[3]}");
    }

    // multiply each element of an array by 2
    static void ModifyArray(int[] array2)
    {
        for (var counter = 0; counter < array2.Length; ++counter)
        {
            array2[counter] *= 2;
        }
    }

    // multiply argument by 2
    static void ModifyElement(int element)
    {
        element *= 2;
        Console.WriteLine($"Value of element in ModifyElement: {element}");
    }
}
```

Fig. 8.13 | Passing arrays and individual array elements to methods. (Part 1 of 2.)

```text
Effects of passing reference to entire array:
The values of the original array are:
  1   2   3   4   5
The values of the modified array are:
  2   4   6   8  10
Effects of passing array element value:
array[3] before ModifyElement: 8
Value of element in ModifyElement: 16
array[3] after ModifyElement: 8
```

Figure 8.13 next demonstrates that when a copy of an individual value-type array element is passed to a method, modifying the copy in the called method does not affect the original value of that element in the calling method’s array. To show the value of `array[3]` before invoking method `ModifyElement`, lines 30–31 display the value of `array[3]`, which is 8. Line 33 calls method `ModifyElement` (lines 47–51) and passes `array[3]` as an argument. Remember that `array[3]` is actually one `int` value (8) in `array`. Therefore, the app passes a copy of the value of `array[3]`. Method `ModifyElement` multiplies the value received as an argument by 2, stores the result in its parameter `element`, then outputs the value of `element` (16). Since method parameters, like local variables, cease to exist when the method in which they’re declared completes execution, the method parameter `element` is destroyed when method `ModifyElement` terminates. When the app returns control to `Main`, line 34 displays the unmodified value of `array[3]` (i.e., 8).

## 8.8 Case Study: GradeBook Using an Array to Store Grades

We now present the first version of a `GradeBook` class that instructors can use to maintain students’ grades on an exam and display a grade report that includes the grades, class average, lowest grade, highest grade and a grade distribution bar chart. The version of class `GradeBook` presented in this section stores the grades for one exam in a one-dimensional array. In Section 8.10, we present a second version of class `GradeBook` that uses a two-dimensional array to store students’ grades for several exams.

### Storing Student Grades in an Array in Class GradeBook

Figure 8.14 shows the output that summarizes the 10 grades we store in an object of class `GradeBook` (Fig. 8.15), which uses an array of integers to store the grades of 10 students for a single exam. The array `grades` is declared as an instance variable in line 7 of Fig. 8.15—therefore, each `GradeBook` object maintains its own set of grades.

```text
Welcome to the grade book for
CS101 Introduction to C# Programming!

The grades are:

Student  1:  87
Student  2:  68
Student  3:  94
Student  4: 100
Student  5:  83
Student  6:  78
Student  7:  85
Student  8:  91
Student  9:  76
Student 10:  87

Class average is 84.90
Lowest grade is 68
Highest grade is 100
```

Fig. 8.14 | Output of the GradeBook example that stores one exam’s grades in an array. (Part 1 of 2.)

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

Fig. 8.14 | Output of the GradeBook example that stores one exam’s grades in an array. (Part 2 of 2.)

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

    // sum students' grades
    foreach (var grade in grades)
    {
        total += grade;
    }

    // return average of grades
    return total / grades.Length;
}

// output bar chart displaying grade distribution
public void OutputBarChart()
{
    Console.WriteLine("Grade distribution:");

    // stores frequency of grades in each range of 10 grades
    var frequency = new int[11];

    // for each grade, increment the appropriate frequency
    foreach (var grade in grades)
    {
        ++frequency[grade / 10];
    }

    // for each grade frequency, display bar in chart
    for (var count = 0; count < frequency.Length; ++count)
    {
        // output bar label ("00-09: ", ..., "90-99: ", "100: ")
        if (count == 10)
        {
            Console.Write(" 100: ");
        }
        else
        {
            Console.Write($"{count * 10:D2}-{count * 10 + 9:D2}: ");
        }

        // display bar of asterisks
        for (var stars = 0; stars < frequency[count]; ++stars)
        {
            Console.Write("*");
        }

        Console.WriteLine(); // start a new line of output
    }
}

// output the contents of the grades array
public void OutputGrades()
{
    Console.WriteLine("The grades are:\n");
```

Fig. 8.15 | Grade book using an array to store test grades. (Part 1 of 4.)
