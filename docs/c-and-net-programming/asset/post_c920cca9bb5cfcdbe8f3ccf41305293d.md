
`>>=` is a composite operator. It shifts the binary representation of the value by 1 to the right and assigns the resulting value to the same variable. The `for` loop is executed until the value of variable `i` drops to 0.

## Q.5 What is the output of following program?

**Ans.:**

```c
#include <stdio.h>
int main()
{
    int i = 3;
    switch (i)
    {
        case 0+1: printf("T");
            break;
        case 1+2: printf("Love");
            break;
        default: printf("India");
    }
    return 0;
}
```

Program outputs 'Love'. The given expression gets evaluated in cases. The control goes to the second case block after evaluating 1 + 2 = 3.

## Long Answered Questions

- Q.1 What is a control statement? (Refer section 4.1)
- Q.2 Discuss various condition checking statements provided by C#. (Refer section 4.1)
- Q.3 What is use of break and continue? (Refer section 4.4)
- Q.4 What is necessary for any looping statement? (Refer section 4.3)
- Q.5 What is the purpose of using statement? (Refer section 4.5)
- Q.6 Write a C# program to check whether the entered year is a Leap year or not.

**AU:** May-18, Marks 5

**Ans.:**

```csharp
/* Program to check whether the entered year is Leap year or not */
using System;

namespace CheckLeapYear
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Enter Year :");
            int Year = int.Parse(Console.ReadLine());
            if (((Year % 4 == 0) && (Year % 100 != 0)) || (Year % 400 == 0))
                Console.WriteLine("{0} is a Leap Year.", Year);
            else
                Console.WriteLine("{0} is not a Leap Year.", Year);
            Console.ReadLine();
        }
    }
}
```

### Q.7 Write a C# program to Get a Number and Display the Number in its Reverse order.

**AU:** Dec.-18, Marks 7

**Ans.:**

```csharp
/* C# program to reverse a number */
using System;

namespace ReverseNo
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Enter a No. to reverse");
            int Number = int.Parse(Console.ReadLine());
            int Reverse = 0;
            while (Number > 0)
            {
                int remainder = Number % 10;
                Reverse = (Reverse * 10) + remainder;
                Number = Number / 10;
            }
            Console.WriteLine("Reverse No. is {0}", Reverse);
            Console.ReadLine();
        }
    }
}
```

### Q.8 Write a C# program to Sort a List of Names in Alphabetical Order.

**AU:** Dec.-18, Marks 6

**Ans.:**

```csharp
/*
 * C# Program to Sort a List of Names in Alphabetical Order
 */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ConsoleApplication1
{
    class ProgramSort
    {
        static void Main()
        {
            List<string> names = new List<string>();
            names.Add("Riya");
            names.Add("Bina");
            names.Add("Abha");
            names.Add("Gita");
            names.Add("Tina");
            names.Sort();
            foreach (string s in names)
                Console.WriteLine(s);
            Console.ReadLine();
        }
    }
}
```

## Unit - I

## CHAPTER - 5

## CORE C# - PART IV - FUNCTIONS AND METHODS

**Syllabus:** Core C#.

| Section No. | Topic Name | Page No. |
|---|---|---|
| 5.1 | Methods | 5 - 2 |
| 5.2 | Static Methods | 5 - 13 |
| 5.3 | Instance Methods | 5 - 14 |
| 5.4 | Anonymous Methods | 5 - 15 |
| 5.5 | Method Overloading | 5 - 16 |
| 5.6 | Hiding Methods, Overriding Methods and Sealed Methods | 5 - 16 |
| 5.7 | Unsafe Method or Unsafe Block | 5 - 16 |
|  | Two Marks Questions with Answers | 5 - 18 |
|  | Long Answered Questions | 5 - 20 |

### 5.1 Methods

**Concept**

- 1. A method is a group/block of statements that together perform a task.

**Explanation**

- 2. When class is created, the fields are meant to describe the properties of the class. Besides the characteristics used to describe it, an object can perform actions or assignments and manipulations.
- 3. An action performed by a class is called a function or a method.
- 4. A method allows to encapsulate a piece of code and call it from other parts of the code. A method is simply a section of code in which particular detail for the functionality of the class is written.
- 5. One can create as many methods as required in a class.
- 6. Every C# program has at least one class with a method named `Main`.
- 7. For using a method, one needs to:
  - Define the method and then
  - Call the method

### 5.1.1 Defining Method in C#

- 1. By defining a method, it means to declare the elements of its structure.
- 2. Syntax for defining a method in C#:

```csharp
<visibility/Access Specifier> <Return Type> <Method Name>(Parameter List)
{
    Method Body
}
```

Where,

- **Access Specifier** determines the visibility of a variable or a method from another class. The visibility is optional. If not specified, then the method would be private.
- If the method is to be accessed only by members of the same class, it is marked as **private** or left without an access modifier.
- If the method is to be accessed by members of the class and other parts of the same program but not outside of the program, it is marked with the **internal** keyword.
- If the method is to be accessed by the members of the same class, other parts of the same program, and other parts of other programs, it is marked as **public**.
- **Return type** is the data type of the value the method returns. A method may return a value. If the method is not returning any values, then the return type is **void**.
- A method can also return an expression, provided the expression produces a value that is conform to the return type. Here is an example:

```csharp
class Exercise
{
    double? Operate()
    {
        return 24.55 * 4.16;
    }
}
```

- **Method name** is a unique identifier and it is case sensitive. It cannot be same as any other identifier declared in the class.
- **Parameter list** is enclosed between parentheses and the parameters are used to pass and receive data from a method. The parameter list refers to the type, order, and number of the parameters of a method. Parameters are optional; that is, a method may contain no parameters.
- **Method body** contains the set of instructions needed to complete the required activity.

**Example**

```csharp
/* Following code snippet shows a function *FindMin* that takes two integer values and returns the smaller of the two.
It has public access specifier, so it can be accessed from outside the class using an instance of the class. */
class NumberManipulatorClass
{
    public int FindMin(int num1, int num2)
    {
        /* local variable declaration */
        int result;

        if (num1 < num2)
            result = num1;
        else
            result = num2;

        return result;
    }

    // ...
}
```

### 5.1.2 Calling Method in C#

- 1. A method is called using the name of the method as shown below.
- 2. A public method can be called from other classes by using the instance of the class to which the method belongs.

**Example**

```csharp
//Illustration of method call
using System;

namespace methodsdemo
{
    class NumberManipulatorClass
    {
        static void Main(string[] args)
        {
            /* local variable definition */
            int no1 = 50;
            int no2 = 60;
            int min;
            NumberManipulatorClass obj = new NumberManipulatorClass();

            //calling the FindMin method
            min = obj.FindMin(no1, no2);
            Console.WriteLine("Minimum number is : {0}", min);
            Console.ReadLine();
        }
    }
}
```

Input: Nil

**Output**

Minimum number is 50

**Example**

```csharp
//Illustration of class method
using System;

namespace methodsdemo
{
    class NumberManipulatorClass
    {
        public int FindMax(int num1, int num2)
        {
            /* local variable declaration */
            int result;

            if (num1 > num2)
                result = num1;
            else
                result = num2;

            return result;
        }
    }

    class Test
    {
        static void Main(string[] args)
        {
            /* local variable definition */
            int no1 = 50;
            int no2 = 60;
            int max;
            NumberManipulatorClass obj = new NumberManipulatorClass();

            //calling the FindMax method
            max = obj.FindMax(no1, no2);
            Console.WriteLine("Maximum number is : {0}", max);
            Console.ReadLine();
        }
    }
}
```

Input: Nil

**Output**

Maximum number is 60

### 5.1.3 Passing Parameters to a Method

**Concept**

- 1. There are three ways that parameters can be passed to a method while calling the method.

**Explanation**

- 2. These three methods are as follows.
  - 2.1 Passing parameters by value - This method copies the actual value of an argument into the formal parameter of the function. In this case, changes made to the parameter inside the function have no effect on the argument.
