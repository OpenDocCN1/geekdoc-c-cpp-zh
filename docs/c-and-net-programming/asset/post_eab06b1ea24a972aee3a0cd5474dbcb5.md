
Here, "Tuesday" will be stored in the string type variable 'today'.

### Example

```csharp
// Illustration of array
using System;
namespace arrayconcept
{
    class Usingarray
    {
        static void Main()
        {
            int[] numbers; //declaration of array
            numbers = new int[6] { 100, 200, 300, 400, 500, 600 }; //creation and initialization of array
            Console.WriteLine("Numbers in the Array");
            for (int cnt = 0; cnt < 6; cnt++)
            {
                Console.WriteLine("\nNumber Element {0} of array = {1}", cnt + 1, numbers[cnt]);
                //accessing the array elements
            }
            Console.ReadLine();
        }
    }
}
```

Input Nil

### Output

Numbers in the Array
Number Element 1 of array = 100
Number Element 2 of array = 200
Number Element 3 of array = 300
Number Element 4 of array = 400
Number Element 5 of array = 500
Number Element 6 of array = 600

## 7.5 Accessing array elements using for each loop

- foreach looping statement can be used to iterate through an array.

### Example

```csharp
//illustration of foreach loop for Array
using System;
namespace arrayconcept
{
    class ArrayUsingForEach
    {
        static void Main(string[] args)
        {
            int[] numbers = new int[5]; /*numbers is an array of 5 integers */
            /* initialization of array elements */
            for (int cnt = 0; cnt < 5; cnt++)
            {
                numbers[cnt] = cnt + 50;
            }

            int num;
            /* print each array element */
            Console.WriteLine("Array Elements ");
            foreach (num in numbers)
            {
                Console.WriteLine("{0}", num);
            }
            Console.WriteLine();
        }
    }
}
```

Input Nil

### Output

Array Elements
50
51
52
53
54

## 6.1.2 Types of Array

### 6.1.2.1 Concept

In C# there are four types of array as explained below.

| Types of arrays | Description |
|---|---|
| One Dimensional Array | A simple array which contains only one dimension known as one dimensional array. |
| MultiDimensional Array | Array which contains more than one dimension is known as MultiDimensional Array. Simplest form of multidimensional array is ‘two-dimensional array’. |
| Jagged Array | Jagged array is "array of array". |
| Param Array | Param array is used to pass unknown number of parameter to a method |

### 6.1.2.2 One Dimensional Array

**Concept**

An array which contains only one dimension (1 row) is known as one dimensional array.

**Explanation**

1 Dimensional array declaration

```csharp
datatype[] arrayname
```

### 6.1.2.3 Multidimensional Array

**Concept**

An array which contains more than one dimension (multiple rows and columns) is known as Multidimensional array.

**Explanation**

- 1. For programming, two-dimensional array is widely used which is the simplest form of the multi dimensional array.
- 2. Multidimensional array declaration
- 3. Example
- 4. Two-dimensional array

```csharp
datatype[,] arrayname;//two-dimensional array
datatype[,,] arrayname;//three-dimensional array
```

```csharp
int[,] distances;// two dimensional array
string[,,] names;//three dimensional array
```

**Concept**

Two-dimensional array is a simplest form of the multidimensional array. Which has two dimensions (interpreted as 1 row and 1 column) is known as two-dimensional array.

**Explanation**

- 3. Following is two-dimensional array of size (4*3) means a matrix of 4 rows and 3 columns each whose elements are represented as follows,

|  | Column0 | Column1 | Column2 | Column3 |  |
|---|---|---|---|---|---|
|  | Arr[0][0]=1 | Arr[0][1]=4 | Arr[0][2]=9 | Arr[0][3]=5 | Row0 |
|  | Arr[1][0]=4 | Arr[1][1]=4 | Arr[1][2]=1 | Arr[1][3]=2 | Row1 |
|  | Arr[2][0]=6 | Arr[2][1]=3 | Arr[2][2]=7 | Arr[2][3] | Row2 |

- 4. Each element in the two dimensional array is represented as arrayname[rowno][colno]. Here rowno and colno shows the value of row and column respectively.

- 5. Initialization of two-dimensional array :
  - Two-dimensional array is initialized in the same way as one dimensional array as shown below.

```csharp
int[,] matrix =
{
    {101, 102, 103, 104}, //row1 elements
    {105, 106, 107, 108}, //row2 elements
    {109, 110, 111, 112}  //row3 elements
};
//It is matrix of 3 rows and 4 columns
```

- 6. Accessing the element of two dimensional array :
  - Two-dimensional array elements can be accessed by using the array name with its two index-numbers, row index and column index as shown below.

Element stored at position, row 2 column 3, is accessed as `matrix[1, 2]`

### Example

```csharp
//illustration of 2-D array
using System;
namespace arrayconcept
{
    class Twodimensionalarray
    {
        static void Main()
        {
            int[,] squarematrix = new int[3, 3] { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
            //initialization of two dimensional array
            int row, col;
            for (row = 0; row < 3; row++)
            {
                for (col = 0; col < 3; col++)
                {
                    Console.WriteLine("\n squarematrix[{0},{1}] = {2}",
                        row, col, squarematrix[row, col]); //accessing 2-D array elements
                }

                Console.ReadLine();
            }
        }
    }
}
```

Input Nil

### Output

squarematrix[0,0] =1
squarematrix[0,1] =2
squarematrix[0,2] =3
squarematrix[1,0] =4
squarematrix[1,1] =5
squarematrix[1,2] =6
squarematrix[2,0] =7
squarematrix[2,1] =8
squarematrix[2,2] =9

### 6.1.2.4 Jagged Array

**Concept**

- 1. In C#, a Jagged array is an array of array in which each row of jagged array contains its own array and the length of each array can be different.

**Explanation**

- 2. Jagged array declaration

```csharp
int[][] jaggedArray;
jaggedArray = new int[3][];
jaggedArray[0] = new int[4];
jaggedArray[1] = new int[2];
jaggedArray[2] = new int[5];
```

In above example the jaggedArray has 3 arrays in it, with first array having 4 elements, second array having 2 elements and third array 5 elements.

- 3. Jagged array initialization

Before using the jagged array it has to be initialized as given below,

```csharp
int[][] JaggedArray = new int[3][]
{
    new int[] {2, 3, 5, 7},
    new int[] {4, 9},
    new int[] {1, 3, 5, 7, 9}
};
```

- 4. Accessing the element of jagged array

Element of a jagged array are accessed using array name and its index as shown below.

```csharp
JaggedArray[row][col];
```

### Example

```csharp
//illustration of jagged array
using System;
namespace arrayconcept
{
    class jaggedarrays
    {
        static void Main()
        {
            // jagged array with 3 rows.
            int[][] jaggedNumbers = new int[3][];

            // Create a new array in the jagged array, and assign values to it.
            //set row 1
            jaggedNumbers[0] = new int[2];
            jaggedNumbers[0][0] = 1;
            jaggedNumbers[0][1] = 2;

            // set row 2, initialized to zero.
            jaggedNumbers[1] = new int[1];
            jaggedNumbers[1][0] = 3;

            // Set row 3, using array initializer.
            jaggedNumbers[2] = new int[] { 4, 5, 6 };

            // Access elements and Print all elements in the jagged array.
            for (int row = 0; row < jaggedNumbers.Length; row++)
            {
                int[] innerArray = jaggedNumbers[row]; //copying array reference
                Console.WriteLine("Inner Array {0} Elements ", row + 1);
                for (int index = 0; index < innerArray.Length; index++)
                {
                    Console.Write(innerArray[index] + " ");
                }
                Console.WriteLine();
            }
        }
    }
}
```

Input Nil

### Output

```csharp
Inner Array 1 Elements 1 2
Inner Array 2 Elements 3
Inner Array 3 Elements 4 5 6
```

### 6.1.2.5 Param Array

**Concept**

While dealing with the method when it is not sure about the number of parameters of the method then Param array can be used effectively.

**Explanation**

Param array is used to pass unknown number of parameter to a method.

### Example

```csharp
//illustration of param array
using System;
namespace arrayConcept
{
    class Paramarray
    {
        static int multiply(params int[] numbers)
        {
            int product = 1;
            foreach (int n in numbers)
            {
                product = product * n;
            }
            return product;
        }

        static void Main(string[] args)
        {
            int product;
            // passing 3 parameters
            product = Paramarray.multiply(2, 6, 8);
            Console.WriteLine("multiplication of 2,6,8 is {0}", product);

            // passing 5 parameters
            product = Paramarray.multiply(2, 4, 6, 8, 10);
            Console.WriteLine("Multiplication of 2,4,6,8,10 is {0}", product);
            Console.ReadLine();
        }
    }
}
```

Input Nil

### Output

Multiplication of 2, 6, 8 is 96.
Multiplication of 2,4,6,8,10 is 3840

## 6.1.3 Passing Array as Parameter

**Concept**

Array can be passed to a method just like other parameters in C#.

### Example

```csharp
//illustration of array passed as parameter to a method
using System;
namespace arrayconcept
{
    class PassingarrayAsParameter
    {
        static void averagearrayelement(int[] avgarray)
        {
            int cnt, sum = 0;
            for (cnt = 0; cnt < 4; cnt++)
            {
                sum = sum + avgarray[cnt];
            }
            Console.WriteLine("Average of elements of array is {0}", sum / (avgarray.Length));
        }

        static void Main(string[] args)
        {
            int[] numbers = new int[4] { 11, 22, 33, 44 };
            //Passing array as parameter
            PassingarrayAsParameter.averagearrayelement(numbers);
            Console.ReadLine();
        }
    }
}
```

Input Nil
