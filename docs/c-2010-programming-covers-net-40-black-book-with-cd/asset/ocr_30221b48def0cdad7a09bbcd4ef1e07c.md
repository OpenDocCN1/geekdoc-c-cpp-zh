```
//Converting nullable double to nullable int and assigning the value to nullable integer variable
int? c = (int?)b;
Console.WriteLine("The value of nullable integer variable is " + c);
//Converting nullable int to integer type and assigning value to integer variable
int n = (int)c;
Console.WriteLine("The value of integer variable is " + n);
Console.ReadLine();
} }
```

In Listing 2.17, we have declared a variable, m, of integer data type and assigned a value of 123 to it, which is further assigned to the nullable variable a. The data types of both these variables are same; therefore, there is no need for type conversion. The code line double? b=a assigns the value of a to a nullable double variable b by implicitly converting its type. Note that when we assign the value of nullable variable b to the nullable integer variable c, explicit type conversion is required, because the double type cannot be implicitly converted to the integer type. Finally, we convert the nullable integer type to integer type. The output of Listing 2.17 is shown in Figure 2.14:

![](bbox=[0.18, 0.34, 0.72, 0.44])

Figure 2.14: Showing the Output of the NullableConversion Application

Now, let’s learn about using the is and as operators.

# Using the is and as Operators

The is operator checks whether an object is compatible with the given type or not and returns a Boolean result, i.e. either true or false. The object may either be of the same type or may be derived from that particular given type. The as operator converts the reference types explicitly into a specific type. If the reference type is compatible with the specified type, it performs successful conversion; otherwise, it returns the null value. Note that the as operator does not throw an exception. Let’s create a new C# 2010 Console application, named IsandAs (also available on the CD-ROM) by performing the steps given in the heading, Declaring Variables, to learn how to use the is and as operators. Listing 2.18 shows the code to add in the Program.cs file of the IsandAs application:

Listing 2.18: Showing the Code for the IsandAs Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace IsandAs
{
    class Program
    {
        static void Main(string[] args)
        {
            object i = 25;
            object str = "Kogent Learning Solutions";    //Checking compatibility
            if (i is string)
                Console.WriteLine("i is a string type");
            else
                Console.WriteLine("i is an integer type");
            string str1 = i as string;    //Casting i to string
            string str2 = str as string;  //Casting str to string
            Console.WriteLine("The value of str1 is " + str1);
```