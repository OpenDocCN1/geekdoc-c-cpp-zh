```
set { propertyVar = value; }
}
}
```

The *public* keyword before the class is an Access Specifier, specifying how the class will be accessed. By being public, it means that it will be accessible by all other classes within the same project. We have given the class the name *TestClass*.

We have also defined a field in the class named *field1*. Below this, we have created a constructor for the class. Note that the constructor takes the same name as the class itself, hence the constructor’s name is *TestClass()*. Inside this class, we have also defined a method named *TestMethod()*, and this method takes in two parameters, *param1* and *param2*, with the former being an integer and the latter being a string.

Here is another example demonstrating how to declare and use a class:

```
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
            Cube1.length = 5.0;
            Cube1.breadth = 8.0;
            // cube 2 specification
            Cube2.height = 8.0;
            Cube2.length = 12.0;
            Cube2.breadth = 14.0;
```