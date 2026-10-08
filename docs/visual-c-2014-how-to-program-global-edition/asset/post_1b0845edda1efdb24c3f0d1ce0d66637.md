
## 8.9 Multidimensional Arrays

```csharp
// Main method begins app execution
static void Main() {
    // one-dimensional array of student grades
    int[] gradesArray = {87, 68, 94, 100, 83, 78, 85, 91, 76};
    var myGradeBook = new GradeBook(
        "CS101 Introduction to C# Programming", gradesArray);
    myGradeBook.DisplayMessage();
    myGradeBook.ProcessGrades();
}
```

Figure 16. Create a GradeBook object using an array of grades. (Part 2 of 2.)

Multidimensional arrays are often used to represent tables of values consisting of information arranged in rows and columns. To identify a particular element, we specify two indices. By convention, the first identifies the row and the second its column. Multidimensional arrays can have more than two dimensions, but such arrays are beyond the scope of this book. C# supports two types of two-dimensional arrays—rectangular arrays and jagged arrays.

### 8.9.1 Rectangular Arrays

Rectangular arrays are used to represent information in the form of rows and columns, where each row has the same number of columns. Figure 8.17 illustrates a rectangular array containing three rows and four columns. In general, an array with m rows and n columns is called an m-by-n array.

| | Column 0 | Column 1 | Column 2 | Column 3 |
| :--- | :--- | :--- | :--- | :--- |
| Row 0 | a[0,0] | a[0,1] | a[0,2] | a[0,3] |
| Row 1 | a[1,0] | a[1,1] | a[1,2] | a[1,3] |
| Row 2 | a[2,0] | a[2,1] | a[2,2] | a[2,3] |

Figure 8.17. Rectangular array with three rows and four columns.

#### Array-Access Expression for Two-Dimensional Rectangular Array

Every element in an array is identified by an array-access of the form `array[row, column]`; `array` is the name of the array, and `row` and `column` are the indices that uniquely identify each element. The names of the elements in row 0 have a first index of 0, and the names of the elements in column 3 have a second index of 3.

#### Array Initializer for Two-Dimensional Rectangular Array

Like one-dimensional arrays, multidimensional arrays can be initialized with initializers. A rectangular array with two rows and two columns could be declared and initialized with nested initializers grouped by braces:

```csharp
int[,] b = {{1, 2}, {3, 4}};
```

So, 1 and 2 initialize `b[0,0]` and `b[0,1]`, respectively, and 3 and 4 initialize `b[1,0]` and `b[1,1]`. The compiler counts the number of nested initializers (represented by sets of curly braces) in the initializer list to determine the number of rows in array `b`. The compiler counts the values in the nested array initializer for a row to determine the number of columns in that row. The compiler will generate an error if the number of initializers in a row is not the same, because every row of a rectangular array must have the same length (i.e., the same number of columns).

### 8.9.2 Jagged Arrays

A jagged array is maintained as a one-dimensional array in which each element refers to one-dimensional array. The manner in which jagged arrays are represented makes them quite flexible because the lengths of the rows in the array need not be the same. For example, jagged arrays could be used to store a student's grades across multiple courses, where the number of exams may vary from course to course.

#### Array Initializer for Two-Dimensional Jagged Array

We can access elements of a jagged array by an array-access expression of the form `arrayName[row][column]`—similar to the array-access expression for rectangular arrays, but with a separate set of square brackets for each dimension. A jagged array with three different lengths could be declared and initialized as follows:

```csharp
int[][] jagged = {
    new int[] {1, 2},
    new int[] {3},
    new int[] {4, 5, 6}
};
```

In this statement, 1 and 2 initialize `jagged[0][0]` and `jagged[0][1]`, respectively; 3 initializes `jagged[1][0]`; and 4, 5 and 6 initialize `jagged[2][0]`, `jagged[2][1]` and `jagged[2][2]`. Therefore, the jagged array in the preceding declaration is actually composed of three separate one-dimensional arrays—one represents the rows, containing the values in the first row (1, 2), the value in the second row ({3}) and the values in the third row (4, 5, 6). Thus, jagged itself is an array of three, each a reference to a one-dimensional array of int values.

#### Diagram of a Two-Dimensional Jagged Array in Memory

Observe the differences between the array-creation expressions for rectangular arrays and jagged arrays. Two sets of square brackets follow the type of jagged, indicating that this is an array of int arrays. Furthermore, in an array initializer, C# requires the keyword `new` to create an array object for each row. Figure 8.18 illustrates the array reference `jagged` after it's been declared and initialized.

![](img/57baed2319be0bb1b5f98674846f2711_371_0.png)

**Fig. 8.18** Jagged array with three rows of different lengths.

#### Creating Two-Dimensional Arrays with Array-Creation Expressions

A rectangular array may be created with an array-creation expression. For example, the following lines declare variable `b` and assign a reference to a three-by-four rectangular array:

```csharp
int[,] b;
b = new int[3, 4];
```

In this case, we use the literal values 3 and 4 to specify the number of rows and number of columns, but this is not required—apps can also use variables and expressions to specify arrays. As with one-dimensional arrays, the elements of a rectangular array are initialized when the array object is created.

A jagged array cannot be completely created with a single array-creation expression. Instead, each one-dimensional array must be initialized separately:

```csharp
int[][] c;
c = new int[2][];
c[0] = new int[5];
c[1] = new int[3];
```

### 8.9.3 Two-Dimensional Array Example: Displaying Element Values

Figure 8.19 demonstrates initializing rectangular and jagged arrays and using nested loops to traverse the arrays (i.e., visit every element).

```csharp
// Fig.8.19: InitArray.cs
// Initializing rectangular and jagged arrays.
using System;
class InitArray {
    // create and output rectangular and jagged arrays
    static void Main() {
        // with rectangular arrays,
        // every row must be the same length.
        int[,] rectangular = {{1, 2, 3}, {4, 5, 6}};

        // with jagged arrays,
        // we need to use "new int[]" for every row,
        // every row does not need to be the same length.
        int[][] jagged = {
            new int[] {1, 2},
            new int[] {3},
            new int[] {4, 5, 6}
        };

        OutputArray(rectangular); // displays rectangular array by row
        Console.WriteLine(); // output a blank line
        OutputArray(jagged); // displays jagged array by row
    }

    // output rows and columns of a rectangular array
    static void OutputArray(int[,] array) {
        Console.WriteLine("Values in the rectangular array by row are ");
        for (var row = 0; row < array.GetLength(0); ++row) {
            // loop through columns of current row
            for (var column = 0; column < array.GetLength(1); ++column) {
                Console.Write($"{array[row, column]} ");
            }
        }
        Console.WriteLine(); // start new line of output
    }

    // output rows and columns of a jagged array
    static void OutputArray(int[][] array) {
        Console.WriteLine("Values in the jagged array by row are ");
        // loop through each row
        foreach (var row in array) {
            foreach (var element in row) {
                Console.Write($"{element} ");
            }
            Console.WriteLine();
        }
    }
}
```
