
## Named Arguments

Named arguments are useful when a method holds quite a number of arguments. In this case, when we try to call this method, we may forget the order in which they appear. Therefore, the use of named arguments helps in remembering the order in which the arguments in the method appear. Listing 17.56 shows a simple example of named arguments:

### Listing 17.56: Showing an Example of Named Arguments

```csharp
using System;
class Program
{
    public static void Main()
    {
        //calculating Area normally
        Console.WriteLine(CalculateArea(100, 20));
        //calculating area using named arguments
        Console.WriteLine(CalculateArea(length:100, width:20));
        //shuffling the position of the named arguments
        Console.WriteLine(CalculateArea(width:20, length:100));
        //combining both positional and named arguments
        Console.WriteLine(CalculateArea(100, width:20));
    }
    public static int CalculateArea(int length, int width)
    {
        return (length * width);
    }
}
```

In the preceding program, we have declared a method named CalculateArea, which calculates the area using the length and width of an object. In the Main() method, we have first called this method by providing the values of length and width at the exact places that are referred to as positional arguments. Then, we have specified the name of the arguments along with their values, which implement the named arguments. Next, we have again called the same method by just shuffling the position of the named arguments and at last, we have called the method by providing both positional and named arguments. In these four cases, the output will be same.

## Optional Arguments

Optional arguments are used in case where a method contains some of the arguments that will be used optionally in few places in a program. These optional arguments may hold a constant value or a default value type so that, whenever the values are not specified, the execution will be carried out using the default or constant values. Listing 17.57 shows an example of optional arguments:

### Listing 17.57: Showing an Example of Optional Arguments

```csharp
using System;
class Employee
{
    public static void Main()
    {
        //Providing positional arguments
        Print(100, "Mr. A Roy", "Manager");
        //Using optional arguments
        Print(200, "Mr. J Sen");
    }
    public static void Print(int id, string name, string designation = "Member", long salary=10000)
    {
        Console.WriteLine("The Employee details are as follows...");
        Console.WriteLine("ID: {0}, Name: {1}, Designation:{2}", id, name, designation);
    }
}
```

In the preceding program, a static method named Print is defined to hold an optional argument designation, which is set to the default value Member. Within the Main() method, we have called the method twice, one by providing the value for optional argument and one by not providing its value. The output of the program is given as follows:

```text
The Employee details are as follows...
ID: 100, Name: Mr. A Roy, Designation: Manager
The Employee details are as follows...
ID: 200, Name: Mr. J Sen, Designation: Member
```

Now, let's learn about the namespace in C#.

## Namespace

In few cases where we need to declare a method in a class whose name matches with the C# Framework class methods, the code becomes ambiguous when we refer the method in the code. At that point, the compiler does not understand which method to call. To avoid this problem, namespace in a C# program is used. Namespace structures the program in such a way that we can simply avoid the naming clashes. The namespace keyword is used to declare a namespace in a C# program. It is a good practice to use namespaces in every C# program. Another utility of namespace is that we can refer any methods written inside a namespace to another code file by just referencing the namespace with the help of the using keyword.

There are three different ways to declare a namespace. The first way is a common way of declaring a namespace, as shown in Listing 17.58:

### Listing 17.58: Showing a Common Way to Declare a Namespace

```csharp
using System;
namespace Organization
{
    class Program
    {
        public static void Main()
        {
            //Statement
        }
    }
}
```

This declaration contains the name of the namespace after the namespace keyword and the namespace definition embeds in the class body.

There is another option where we can define nested namespace. This hierarchical structure allows us to manage our code more efficiently. In this case, we can put more general names at the top of the hierarchy and more specific names at the bottom. This minimizes the chances of naming clashes. Listing 17.59 shows an example of nested namespace:

### Listing 17.59: Showing an Example of Nested Namespace

```csharp
using System;
namespace Corporate
{
    namespace Organization
    {
        class Program
```

```csharp
    public Employee(int emp_ID, string emp_name)
    {
        empID = emp_ID;
        empName = emp_name;
    }
    public static void Print()
    {
        Console.WriteLine("The employee information is as follows:");
        Console.WriteLine("Employee ID: {0}", empID);
        Console.WriteLine("Employee Name: {0}", empName);
    }
    }
```

In the preceding program, we have copied the structure of the code shown in Listing 17.49 in the body of the Organization namespace. In addition, we have defined two classes: Program and Employee. The Employee class contains static members and a static member method, which prints the static members of the class. The Program class contains the Main() method, which calls the static member method of the Employee class with the help of the fully qualified namespace name. In this qualified namespace name, the name of the parent namespace comes first and separated with a dot operator from the name of the child namespace. Using this hierarchical structure, any class and their methods can be referenced. The output of the program is given as follows:

```text
The employee information is as follows:
Employee ID: 100
Employee Name: C. Thomas
```

If we do not want to write the fully qualified names of the namespace every time while referencing any class from that namespace, then we can implement this by means of the using directives instead. We have already used the using directive while referencing the System namespace, which is the base library of the C# language. Using the using directive, we can write the fully qualified namespace names and refer any class or method from that namespace. Listing 17.62 implements the using directive to call the namespace name:

### Listing 17.62: Calling a Namespace with the using Directive

```csharp
using System;
using Corporate.Organization;
class Program
{
    public static void Main()
    {
        Employee e = new Employee(100, "C. Thomas");
        //calling the Print() method of the Employee class using namespace
        Employee.Print();
    }
}
namespace Corporate
{
    namespace Organization
    {
        class Employee
        {
            static int empID;
            static string empName;
            public Employee(int emp_ID, string emp_name)
            {
                empID = emp_ID;
                empName = emp_name;
            }
            public static void Print()
            {
                Console.WriteLine("The employee information is as follows:");
                Console.WriteLine("Employee ID: {0}", empID);
                Console.WriteLine("Employee Name: {0}", empName);
            }
        }
    }
}
```

In the preceding program, we have declared the namespace names as “using Corporate.Organization”. Within the Main() method, we have directly called the Print() method. The output of this program will be same as the previous one.

Sometimes, it may happen that the namespace name is too large that we wish to have it shorter, which would improve readability as well as avoid naming clashes. This can be achieved by using alias. Listing 17.63 shows an example of using alias:

### Listing 17.63: Calling a Namespace with the Alias Directive

```csharp
using System;
//Defining alias namespace
using EmpNamespace = Corporate.Organization.Employee;
class Program
{
    public static void Main()
    {
        //Calling the Print() method of the Employee class using namespace
        EmpNamespace.Print();
    }
}
namespace Corporate
{
    namespace Organization
    {
        class Employee
        {
            public static void Print()
            {
                Console.WriteLine("The employee information is as follows:");
                Console.WriteLine("Employee ID: {0}", 100);
                Console.WriteLine("Employee Name: {0}", "C. Thomas");
            }
        }
    }
}
```

In the preceding program, we have first declared the namespace as “using EmpNamespace = Corporate.Organization.Employee”; therefore, by using the name EmpNamespace, we can directly call all the static methods inside the Employee class in the Organization.Employee namespace. Within the Main() method of the Program class, we can call the static method Print() by using the alias name. For this program, the output is same as that of Listing 17.62.

Now, if we modify the preceding program in such a way that the Main() method contains two Print() methods, then the one with the reference to the EmpNamespace namespace will print the desired text on the console while the other Print() method without any reference will actually print. Listing 17.64 shows an example of this ambiguous operation:
