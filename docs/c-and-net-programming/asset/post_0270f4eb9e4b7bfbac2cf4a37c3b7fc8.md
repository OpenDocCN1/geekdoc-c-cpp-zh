
Overriding is the same method names with the same arguments and return types associated with the class and its child class.

## Q.4 What are the access modifiers ?
Ans. : Access modifiers determine the scope of the method or variables that can be accessed from other various objects or classes. There are five types of access modifiers, and they are as follows :
- Private
- Protected
- Public
- Friend
- Protected Friend

## Q.5 Can you return multiple values from a function in C# ?
Ans. : Multiple values can be returned from functions in C# using output parameters. A return statement can be used for returning only one value from a function. However, using output parameters, you can return two values from a function.

## Q.6 Write a C# program to find the length of the Jagged Array using predefined functions.
AU : May-18, Marks 8

Ans. :

```
/*
 * C# Program to Find the Length of the Jagged Array using Predefined Functions
 */
using System;
class Program
{
    public static void Main()
    {
        byte[][] numbers = new byte[5][];
        for (int i = 0; i < numbers.Length; i++)
        {
            numbers[i] = new byte[i + 3];
        }
        for (int i = 0; i < numbers.Length; i++)
        {
            Console.WriteLine("Length of row {0} is {1}", i, numbers[i].Length);
        }
        Console.Read();
    }
}
```

## Long Answered Questions
- Q.1 What are static methods in C# ? (Refer section 5.2)
- Q.2 Discuss anonymous methods in C#. (Refer section 5.4)
- Q.3 Write a note on 'Method Overriding'. (Refer section 5.6)
- Q.4 Discuss method hiding. (Refer section 5.1)
- Q.5 What are sealed methods in C# ? (Refer section 5.6)
- Q.6 Differentiate static and non-static members of a class. AU : Dec.-18

**Ans. :** A static method belongs to the class and a non-static method belongs to an object of a class. The static methods can be accessed directly from the class, while non-static methods (or instance methods) have to be accessed from an instance.

- A static method is shared by all instances of the class. Whenever a method is called in C++/Java/C#, an implicit argument "this" reference is passed along with/without the other parameters. In case of a static method call, the "this" reference is not passed as static methods belong to a class and hence do not have the "this" reference.
- A non-static method can only be called on an object of a class that it belongs to. A static method can access only static members. A non-static method can access both static and non-static members because at the time when the static method is called, the class might not be instantiated (if it is called on the class itself). In the other case, a non-static method can only be called when the class has already been instantiated.
- The objects of the class cannot have the copy of these fields. These fields are referred by the class name. Ex : Employee. company. Without creating an instance of a class, these fields can be accessed.
- **The Static and Non-static variables in C# -** Whenever a variable is declared by using the static modifier or when variable is declared inside any static block then those variables are considered as static variables whereas the rest of the other are considered as non-static variables.
- If one wants a variable to have the same value throughout all instances of a class then it is needed to declare that variable as a static variable. So, the static variables are going to hold the application level data which is going to be the same for all the objects.
- A non-static field is accessed by all objects of the class. Each object has one copy of non-static field. To use non static fields, an instance of the class should be created.
- **Static and Non-Static Constructor in C# -** If the constructor is written explicitly by the static modifier, then it is called as static constructor and the rest of the others are the non-static constructors. The most important point that one needs to remember is the static constructor is the first block of code which gets executed under a class. No matter how many numbers of objects created for the class the static constructor is executed only once. On the other hand, a non-static constructor gets executed only when the object of the class is created and that is too for each and every object of the class.

- It is not possible to create a static constructor with parameters. This is because the static constructor is the first block of code which is going to execute under a class. And this static constructor is called implicitly, even if parameterized there is no chance of sending the parameter values.
- Understanding the Static class in C# - The class which is created by using the static modifier is called a static class. A static class can contain only static members in it. It is not possible to create an instance of a static class. This is because it contains only static members those can be accessed by the other static members of a class by using the class name.

Q.7 Explain virtual methods and overriding. (Refer section 5.6)

AU : May-19, Marks 13

## Notes

## Unit - I

## CHAPTER - 6

## C# - ARRAYS, STRINGS, STRINGBUILDERS AND TUPLES

**Syllabus :** Arrays and Tuples.

| Section No. | Topic Name | Page No. |
|---|---|---|
| 6.1 | C# Arrays | 6 - 2 |
| 6.2 | Array Class | 6 - 12 |
| 6.3 | ArrayList Class | 6 - 18 |
| 6.4 | String Class | 6 - 20 |
| 6.5 | StringBuilder Class | 6 - 26 |
| 6.6 | Tuple | 6 - 28 |
|  | Two Marks Questions with Answers | 6 - 33 |
|  | Long Answered Questions | 6 - 35 |

## 6.1 C# Arrays

### 6.1.1 Concept

Array is a collection of the data elements or values of same data type.

### Explanation

- 1. In C# array is a reference type.
- 2. Each array in C# is an object.
- 3. Each array is inherited from the class System.Array.
- 4. The individual values present in an array are called as array elements.
- 5. Individual array element is accessed using the name of array and the index number representing the position of element in an array.
- 6. Memory allocation of array - Array consists of the contiguous memory locations. Lower address memory location represents first element and highest address memory location represents last element. This is depicted in the following figure.

![](img/3005a4307e6d8f3bb7e76eea28a92357_177_0.png)

Fig. 6.1.1 Arrays

7. Using arrays

### 7.1 Declaration of array

```
datatype[] arrayname;
```

- datatype can be any primitive or reference data type like int, float, string etc.
- [] represents the size of the array.
- arrayname is the name given to the array.
- Array declaration examples

```
int[] marks[5];
string name[3];
float area[2];
```

### 7.2 Creation of an array

- Only declaration of an array is not sufficient to use arrays. One needs to create the array for using the array in the program.
- For creating an array ‘new’ keyword is used using which actual memory is allocated for array elements.
- Array creation syntax

```
datatype[] arrayname = new datatype[size]
```

Size here represents the size of an array.

- Array creation examples

```
int [] marks= new int[5];
float[] area=new float[4];
char[] name=new char[60];
```

### 7.3 Initialization and Assigning value to the elements of array

- Before using array one needs to assign values to the elements of an array.
- Value can be assigned to the array element by using its index number.

```
string[] days =new string[7];
days[0]="Monday";
```

- Value can be assigned to the elements of array at the time of declaration or creation of array.

```
int[] number=new int[3] {1,2,3};//at creation time
float area={2.45,56.88};//at declaration time
int distance=new int[]{10,20,30};//without giving size

string[] array = new string[2]; // creates array of length 2, default values
string[] array = new string[] { "A", "B" }; // creates populated array of length 2
string[] array = { "A", "B" }; // creates populated array of length 2
```

### 7.4 Traversing and Accessing element stored in array

- Array elements are accessed by writing the name of array with the index of the element to be accessed, in the square bracket.
- By default the array index value in C# starts from 0.
- To access the value stored in the second element of the array named days (which is stored at index value 1), following statements is used,

```
string[] days=new
string[7]{"Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"};
string today;
today=days[1];
```
