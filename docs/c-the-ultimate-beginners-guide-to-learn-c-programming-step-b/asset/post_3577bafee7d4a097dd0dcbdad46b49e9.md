
```csharp
}
```

The code gives the following result:

The *for* loop helped us fill 10 values into the array, with the first element being 100 and the last one being 109. The *foreach* loop helped us access all the elements of the array right from index 0 to the last index. Note that the variable *x* has been used for filling the array values while the variable *y* has been used for iterating through the elements of the array. The code returns the output given below:

```text
Element[0] = 100
Element[1] = 101
Element[2] = 102
Element[3] = 103
Element[4] = 104
Element[5] = 105
Element[6] = 106
Element[7] = 107
Element[8] = 108
Element[9] = 109
```

## Multidimensional Arrays

The concept of multidimensional arrays is supported in C#. Such arrays are also known as rectangular arrays. A multidimensional array is a two-dimensional series organized in the form of rows and columns. The following is an example of a multidimensional array:

```csharp
int[,] array1 = new int[3,2]{
            {1, 5},
            {2, 5},
            {5, 7}
        };

// or

int[,] array1 = { {1, 5}, {2, 5}, {5, 7} };
```

As you can see in the above example, to initialize a multidimensional array, you must define it in terms of the number of rows and the number of columns. The [3,2] means that the array will have 3 rows and 2 columns.

To access the elements of a multidimensional array, we use two indexes. The first index identifies the row while the second one identifies the column. Note that both indexes begin from 0. Let us demonstrate this using an example:

```text
1
5
2
5
5
7
```

That is how we can access the elements. The *array1[2,1]* returns the element located at row 2 and column 1 of the array.

## Jagged Arrays

A jagged array is simply an array of arrays. These arrays are storing arrays instead of data type values directly. To initialize a jagged array, we use two square brackets [] []. In the first bracket, we specify the size of the array while in the second bracket, we specify the dimension of the array which is to be stored as values. Here is an example to show the declaration and initialization of a jagged array:

```csharp
using System;

public class MyArray
{
    public static void Main()
    {
        int[][] jaggedArray = new int[2][];

        jaggedArray[0] = new int[4]{1, 2, 3, 4};

        jaggedArray[1] = new int[3]{5, 6, 7};

        Console.WriteLine(jaggedArray[0][0]);

        Console.WriteLine(jaggedArray[0][2]);

        Console.WriteLine(jaggedArray[1][1]);
    }
}
```

We have declared and initialized our jagged array in the above code. The code will give you the following result:

```text
1
3
6
```

A jagged array can also store a multidimensional array as a value. We can use [,] in the second bracket to indicate a multi-dimensional. Here is an example:

```csharp
using System;

public class MyArray
{
    public static void Main()
    {
        int[][,] jaggedArray = new int[3][,];

        jaggedArray[0] = new int[3, 2] { { 1, 5 }, { 2, 6 }, { 4, 8 } };
        jaggedArray[1] = new int[2, 2] { { 3, 5 }, { 4, 6 } };
        jaggedArray[2] = new int[2, 2];

        Console.WriteLine(jaggedArray[0][1,1]);
        Console.WriteLine(jaggedArray[1][1,0]);

        Console.WriteLine(jaggedArray[1][1,1]);
    }
}
```

The code will return the following:

```text
6
4
6
```

In case an additional bracket is added, then this will become an array of array of array. This is demonstrated in the following example:

```csharp
using System;

public class MyArray
{
    public static void Main()
    {
        int[][][] jaggedArray = new int[2][][]
        {
            new int[2][]
            {
                new int[3] { 2, 3, 5 },
                new int[2] { 1, 5 }
            },
            new int[1][]
            {
                new int[3] { 7, 6, 8 }
            }
        };

        Console.WriteLine(jaggedArray[0][0][0]);

        Console.WriteLine(jaggedArray[0][1][1]);

        Console.WriteLine(jaggedArray[1][0][2]);
    }
}
```

The code returns the following:

```text
2
5
8
```

Note that we have used three square brackets [][][], which means an array of array of

## Chapter 11: Classes[30]

A class can be seen as a blueprint for an object. Objects in the real world have characteristics like shape, color and functionalities. For example, X6 is an object of car type. A car has characteristics like color, speed, interior, shape etc. This means that any company that creates an object with the above characteristics will be of type car. This means that the Car is a class while each object, that is, a physical car, will be an object of type Car.

In object-oriented programming (not forgetting that C# is an object-oriented programming language) a class has fields, properties, methods, events etc. A class should define the types of data and the functionality that the objects should have.

With a class, you can create your own custom types by grouping variables of other types together as well as methods and events.

In C#, we use the *class* keyword to define a class[31]. Here is a simple example of this:

```csharp
public class TestClass
{
    public string field1 = string.Empty;

    public TestClass()
    {
    }

    public void TestMethod(int param1, string param2)
    {
        Console.WriteLine("The first parameter is {0}, and second parameter is {1}",
            param1, param2);
    }

    public int AutoImplementedPropertyTest { get; set; }
    private int propertyVar;

    public int PropertyTest
    {
        get { return propertyVar; }
        set { propertyVar = value; }
    }
}
```

The *public* keyword before the class is an Access Specifier, specifying how the class will be accessed. By being public, it means that it will be accessible by all other classes within the same project. We have given the class the name *TestClass*.

We have also defined a field in the class named *field1*. Below this, we have created a constructor for the class. Note that the constructor takes the same name as the class itself, hence the constructor’s name is *TestClass()*. Inside this class, we have also defined a method named *TestMethod()*, and this method takes in two parameters, *param1* and *param2*, with the former being an integer and the latter being a string.

Here is another example demonstrating how to declare and use a class:

```csharp
using System;

namespace CubeApplication {
    class Cube {
        public double length;  // Length of the cube
        public double breadth;  // Breadth of the cube
        public double height;  // Height of the cube
    }

    class Cubetester {
        static void Main(string[] args) {
            Cube Cube1 = new Cube();  // Declare Cube1 of type Cube
            Cube Cube2 = new Cube();  // Declare Cube2 of type Cube
            double volume = 0.0;  // Store the cube volume here

            // cube 1 specification
            Cube1.height = 4.0;
```

```csharp
class Cube {
    private double length;    // Length of a cube
    private double breadth;   // Breadth of a cube
    private double height;    // Height of a cube

    public void setLength( double len ) {
        length = len;
    }

    public void setBreadth( double brea ) {
        breadth = brea;
    }

    public void setHeight( double heig ) {
        height = heig;
    }

    public double getVolume() {
        return length * breadth * height;
    }
}

class Cubetester {
    static void Main(string[] args) {
        Cube Cube1 = new Cube();  // Declare Cube1 of type Cube
        Cube Cube2 = new Cube();
        double volume;

        // Declare Cube2 of type Cube
        // cube 1 specification
        Cube1.setLength(4.0);
        Cube1.setBreadth(6.0);
        Cube1.setHeight(8.0);

        // cube 2 specification
        Cube2.setLength(10.0);
        Cube2.setBreadth(14.0);
        Cube2.setHeight(12.0);
        // volume of cube 1
        volume = Cube1.getVolume();
        Console.WriteLine("Volume of Cube1 is: {0}" ,volume);

        // volume of cube 2
        volume = Cube2.getVolume();
        Console.WriteLine("Volume of Cube2 is: {0}", volume);
        Console.ReadKey();
    }
}
}
```

Here is the output from the code:

```text
Volume of Cube1 is: 192
Volume of Cube2 is: 1680
```

We used the *setter* methods to set the values of the various attributes of our two cubes. The *getVolume()* function has been called to calculate the volumes of the two cubes.

### Constructors

A constructor is simply a special member function of a class that is run anytime that we create new objects of the class. A constructor assumes the class name and it should not have a return type. The following example demonstrates how to use a constructor in C#:

```csharp
using System;
```
