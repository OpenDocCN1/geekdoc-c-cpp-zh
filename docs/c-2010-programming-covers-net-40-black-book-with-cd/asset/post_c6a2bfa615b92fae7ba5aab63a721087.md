
![](img/e073a4882197be4ab61103cbe0bcb394_132_0.png)

## Figure 2.2: Showing the New Console Application

8. Add the code given in Listing 2.6 to the Program.cs file of your application:

## Listing 2.6: Showing the Code of the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace DeclaringVariable
{
    class Program
    {
        static void Main(string[] args)
        {
            short x;    //Declaring short type variable
            int y;      //Declaring integer type variable
            double z;   //Declaring double type variable
            x = 6;
            y = 10;
            z = x + y;
            Console.WriteLine("x = {0}, Y = {1}, Z = {2}", x, y, z);
            Console.ReadLine();
        }
    }
}
```

In Listing 2.6, we have declared some variables, assigned values to them, and then print the result. We have called the WriteLine() method of the System.Console object to display the values of the variables. The output of Listing 2.6 is shown in Figure 2.3:

![](img/e073a4882197be4ab61103cbe0bcb394_132_1.png)

## Figure 2.3: Displaying the Output of DeclaringVariable Application

## Initializing Variables

After creating a variable, you must initialize it with some value. Variables can be initialized in several ways—at the time they are declared, within the application with a fixed value, or by copying the value of another variable into them. Now, let's create a new C# 2010 Console application, named InitializingVariable (also available on the CD-ROM) by performing the steps given in the heading, Declaring Variables, earlier in this chapter. After creating the InitializingVariable application, add the code, shown in Listing 2.7, in its Program.cs file to initialize variables:

## Listing 2.7: Showing the Code for the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace InitializingVariable
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a variable at declaration
            short x = 5;
            // Initialize a variable as a copy of another
            int y = x;
            double z = y + 10.25; //assigning an integer value with a floating-point value
            int a = (int)z; // converting the floating-point number to integer
            Console.WriteLine("X = {0} Y = {1} Z = {2}", x, y, z);
            Console.WriteLine("A = {0}", a);
            Console.ReadLine();
        }
    }
}
```

In Listing 2.7, we have assigned the sum of an integer value and a floating-point value to a floating-point variable. Next, we have converted the floating-point number to an integer. This conversion requires an explicit cast because it can lose precision during execution.

Suppose that you had written the statement, int a = (int)z;, of Listing 2.7, as shown in the following code snippet:

```
int a = z;
```

When you run the application with the preceding code snippet, the compiler would generate an error message Cannot implicitly convert type 'double' to 'int'. By forcing you to specifically cast the floating-point number to an integer, the compiler ensures that you understand the consequences of your actions. It is hard to overestimate the number of occasions in which invalid conversions in applications have introduced bugs that caused serious damage and were difficult to track down.

The output of Listing 2.7 is shown in Figure 2.4:

![](img/e073a4882197be4ab61103cbe0bcb394_133_0.png)

Figure 2.4: Showing the Output of the InitializingVariable Application

Now, let's learn how to declare constants.

## Declaring Constants

There are times while creating a C# application; you need a fixed value for a variable. This value cannot be changed throughout the execution of this application. The constants are mostly used while performing the mathematical calculations where the value of e, pi, √2, √3, and so on is pre-calculated. Now, let's create a new C# 2010 Console application, named Constants (also available on the CD) by performing the steps given in the heading, Declaring Variables, earlier in this chapter. The Constants application shows how to declare and initialize the constant value within your application. Add the code, shown in Listing 2.8, in the Program.cs file:

## Listing 2.8: Showing the Code for the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Constants
{
    class Program
    {
        static void Main(string[] args)
        {
            const double pi = 3.1472; //Declaring constant variable
            int r;
            Console.WriteLine("Enter the value of r");
            r = int.Parse(Console.ReadLine());
            double circleArea = pi * r * r;
            Console.WriteLine("The area of circle is " + circleArea);
            Console.ReadLine();
        }
    }
}
```

In Listing 2.8, we have declared a constant variable, pi, of double data type by using the const keyword. The use of the const keyword states that the value of the pi variable is constant, i.e. 3.1472.

The output of Listing 2.8 is shown in Figure 2.5:

![](img/e073a4882197be4ab61103cbe0bcb394_134_0.png)

Figure 2.5: Showing the Output of the Constants Application

Now, let’s learn how to declare the nullable type variables.

## Declaring Nullable Type Variables

You can assign the normal range of values as well as a null value to a nullable type. These values are specified for the underlying value type of the nullable type. For example, you can assign a value from -2147483648 to 2147483647 or null value to Nullable<Int32> (pronounced as nullable of Int32). You can assign the values true, false, or null to Nullable<bool>. To understand this concept better, let’s create a new C# 2010 Console application, named NullableTypes (also available on the CD-ROM) by performing the steps given in the heading, Declaring Variables, earlier in this chapter. After creating the NullableTypes application, add the code, shown in Listing 2.9, in the Program.cs file:

## Listing 2.9: Showing the Code for the Program.cs File of NullableTypes Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace NullableTypes
{
    class Program
    {
        static void Main(string[] args)
        {
            int? var1 = null; //Declaring nullable type variable
            int var2 = 5;
            var1 = var2;  //valid
            // int? is Nullable where underlying type is int
            if (var1.HasValue == true)
            {
                Console.WriteLine("var1 = " + var1.Value);
            }
            else
            {
                Console.WriteLine("var1 = Null");
            }
            Console.ReadLine();
        }
    }
}
```

In Listing 2.9, the value of var1 is printed as 5 on the console. This is because the value of var2 is assigned to var1. If no value is assigned to var1, the output will be displayed as var1=null. The HasValue property provided by nullable types checks the value of the null variable. The output of Listing 2.9 is shown in Figure 2.6:

![](img/e073a4882197be4ab61103cbe0bcb394_135_0.png)

Figure 2.6: Showing the Output of the NullableTypes Application

Now, let’s learn how to use the ?? (null coalescing) operator.

## Using the ?? (Null Coalescing) Operator

The null coalescing operator (??) is mostly used with the nullable value types and reference types. The ?? operator is used between two operands where the first operand must be a nullable type. The second operand must be of the same type as the first operand or of the type that can be implicitly converted to the first type. It checks whether the value of the first operand is null or not. If the value of the first operand is null, it returns the value of the second operand else returns the value of the first operand. In case, if you declare the second operand to the type that cannot be implicitly converted to the type of the first operand, a compile-time error is generated. Now, let’s create a new C# 2010 Console application, named NullCoalescing (also available on the CD-ROM) to make the concept of ?? operator more clear. Create the application by performing the steps given in the heading, Declaring Variables, earlier in this chapter and add the code, shown in Listing 2.10 in the Program.cs file of the application to use the null coalescing operator:

## Listing 2.10: Showing the Code for Using the Null Coalescing Operator

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace NullCoalescing
{
    class Program
    {
        static void Main(string[] args)
        {
            int? i = null; //Nullable variable
            int? j = 30;   //Nullable variable
            int k;
            k = i ?? 25; //Using ?? operator to check for null values
            Console.WriteLine("The value of k is " + k);
            k = j ?? 25; //Using ?? operator to check for null values
            Console.WriteLine("Now the value of k is " + k);
            Console.ReadLine();
        }
    }
}
```
