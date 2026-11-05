
- 7.1.3) These value types are stored in "stack" memory and these value types are fixed in size. If a value assigned to a variable is reassigned to another variable, it will create two copies.
- 7.1.4) Value type variables are of byte, short, int, float, double, long, char, bool, DateTime.
- 7.1.5) Primitive data types are value types except string, object.
- 7.1.6) Object type is superior to all types. It can store any type or any size of data. It helps in inheritance process.
- 7.1.7) Struct, enum are value types.

## 7.2 Reference types

- 7.2.1) Reference type is the one in which a variable holds a reference to the value. The reference types do not contain the actual data stored in a variable, but they contain a reference to the variables.
- 7.2.2) In other words, they refer to a memory location. Using multiple variables, the reference types can refer to a memory location.
- 7.2.3) If the data in the memory location is changed by one of the variables, the other variable automatically reflects this change in value.
- 7.2.4) These reference types are stored in "heap" memory and these types are not fixed in size. They are maintained in system managed heap but it also use stack to store reference of the heap.
- 7.2.5) Example of built-in reference types are: object, dynamic, and string.

### 7.2.5.1) Object Type

- i) The Object Type is the ultimate base class for all data types in C# Common Type System (CTS).
- ii) Object is an alias for System.Object class.
- iii) The object types can be assigned values of any other types, value types, reference types, predefined or user-defined types. However, before assigning values, it needs type conversion.
- iv) When a value type is converted to object type, it is called boxing and on the other hand, when an object type is converted to a value type, it is called unboxing.
- v) Example

```
object obj;
obj = 874; // this is boxing
```

### 7.2.5.2) Dynamic Type

- i) One can store any type of value in the dynamic data type variable.
- ii) Type checking for these types of variables takes place at run-time.
- iii) Syntax for declaring a dynamic type is,

```
dynamic <variable_name> = value;
```

Example,

```
dynamic id = 35;
```

- iv) Dynamic types are similar to object types except that type checking for object type variables takes place at compile time, whereas that for the dynamic type variables takes place at run time.

### 7.2.5.3) String Type

- i) The String Type allows assign any string values to a variable.
- ii) The string type is an alias for the System.String class. It is derived from object type. The value for a string type can be assigned using string literals in two forms: quoted and @quoted.
- iii) Example

```
String name = "Anil Kumble";
```

- A @quoted string literal looks as follows,

```
@"Anil Kumble";
```

- 7.2.6) The user-defined reference types are namely, class, interface, or delegate.

## 7.3 Pointer Type

- 7.3.1) Pointer type variables store the memory address of another type. Pointers in C# have the same capabilities as the pointers in C or C++.
- 7.3.2) Syntax for declaring a pointer type is,

```
type * identifier;
```

Example,

```
float* fptr;
int* iptr;
```

### Example

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Variables_Examples
{
class Program
{
    static void Main(string[] args)
    {
        string name;
        string city;
        sbyte age;
        int pin;
        // \n is used for line-break
        Console.WriteLine("Enter Voter's name\n");
        name = Console.ReadLine();

        Console.WriteLine("Enter City\n");
        city = Console.ReadLine();

        Console.WriteLine("Enter age\n");
        age = sbyte.Parse(Console.ReadLine());

        Console.WriteLine("Enter pin\n");
        pin = Int32.Parse(Console.ReadLine());

        // Printing message to console
        //formatting output
        Console.WriteLine("=================");
        Console.WriteLine("Voter's Complete Information");
        Console.WriteLine("=================\n");

        Console.WriteLine("Name = {0}", name);
        Console.WriteLine("City = {0}", city);
        Console.WriteLine("Age = {0}", age);
        Console.WriteLine("Pin = {0}", pin);
        Console.WriteLine("=================");

        Console.ReadLine();
    }
}
}
```

## 2.9 Type Conversion and Casting

### Concept

- 1. Type conversion is a way or method to convert one data type into another data type.

### Explanation

- 2. In C# type conversion can be done in following two ways:
  - i. Implicit Type Conversion
  - ii. Explicit Type Conversion

### 2.1) Implicit Type Conversion

### Concept

- 1. In implicit type conversion method one data type is converted into another data type automatically.

### Explanation

- 2. There is no data loss in the Implicit Type conversion therefore it is a type safe conversion.
- 3. Implicit Type Conversion is generally recommended and used where smaller data type is converted into larger data type.

### Example

```csharp
//Implicit Type Conversion

using System;
namespace DemoTypeConversion
{
    class ImplicitConversion
    {
        static void Main()
        {
            float f = 4.5f;
            double d1 = f; // Implicit Conversion
            Console.WriteLine("f is float = {0}\n d1 is double = {1}",f,d1);
            Console.ReadLine();
        }
    }
}
```

Input - Nil

### Output

```
f is float=4.5f
d1 is double=4.5
```

### 2.2) Explicit Type Conversion

### Concept

- 1. In explicit Data Type Conversion method one data type is converted into another data type with the help of some predefined functions.

### Explanation

- 2. Explicit type conversion is carried out with the help of casting.
- 3. In explicit type of conversion data loss occurs as the conversion is done forcefully. Hence it is not a type safe conversion.

### Example

```csharp
//Explicit Type Conversion
using System;
namespace DemoTypeConversion
{
    class ExplicitConversion
    {
        static void Main()
        {
            //Explicit Conversion
            float f = 4.5f;
            //Explicit type conversion of float to integer.
            int d1 = (int)f;

            //Explicit type conversion of float to string by ToString Method.

            string str = f.ToString();
            Console.WriteLine("f is float = {0}\n d1 is integer = {1}\n str is string = {2}",f,d1,str);
            Console.ReadLine();
        }
    }
}
```

Input - Nil

### Output

```
f is float =4.5
d1 is integer=4
str is string=4.5
```

In this example ToString method is used in order to convert float value into string. It is a built-in type conversion method.

### 3. Built-in Methods of Type Conversion in C#

Listed below are various type conversion methods which are widely used in C#.

| Method | Description |
| :--- | :--- |
| ToBoolean | This method converts a data type to Boolean data type. |
| ToByte | This method converts a data type to Byte data type. |
| ToChar | This method converts a data type to Char data type. |
| ToDateTime | This method converts a data type to (Integer or String) to date-time format. |
| ToDecimal | This method converts a data type to (Integer or Float) to decimal type. |
| ToDouble | This method converts a data type to Double data type. |
| ToInt16 | This method converts a data type to 16-bit integer |
| ToInt32 | This method converts a data type to 32-bit integer. |
| ToInt64 | This method converts a data type to 64-bit integer |
| ToSByte | This method converts a data type to Signed Byte type. |
| ToSingle | This method converts a data type to small floating point number. |
| ToString | This method converts a data type to String type. |
| ToType | This method converts a data type to specific type. |
| ToUInt16 | This method converts a data type to Unsigned 16-bit integer. |
| ToUInt32 | This method converts a data type to Unsigned 32-bit integer. |
| ToUInt64 | This method converts a data type to Unsigned 64-bit integer. |

**Table 2.9.1 Built-in-methods of type conversion in C#**

### 2.10 Boxing and Unboxing

- 1. Boxing and unboxing are specific types of type-conversion in C#.
- 2. Boxing

### Concept

2.1 Boxing is the process of converting a value type to the type object or to any interface type implemented by this value type.
