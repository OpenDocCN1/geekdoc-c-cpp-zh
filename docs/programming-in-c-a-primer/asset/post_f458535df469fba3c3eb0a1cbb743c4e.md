
Program 11.6 will output the following:
    d1 = 0
    d2 = 10
    d3 = 11
    d4 = 12

## Case Study

## Problem Statement

CompTech is a medium sized organisation that is involved in the sale of computer hardware. It also has a small software development department, which develops customised software and Web sites for different organisations. CompTech has been till now manually maintaining the records of its employees, which is time consuming and decreases the efficiency of the HR department staff. How can CompTech solve the problem?

## Solution

CompTech requests one of the programmers, Harsh, who has been working for the past two years in the software development department, to create an application, which will enable the HR department to automate the task of entering employee data. In order to judiciously utilise memory space, Harsh decides to use the structure feature of C#. A structure is a value type that allows us to organise related data of different data types. After much research, Harsh creates the following C# application.

```
using System;
using System.Collections.Generic;
using System.Text;
namespace StructureExample
{
    public struct Employee
    {
        private string emp_details;

        public string Write
        {
            get { return emp_details; }
            set { emp_details = value; }
        }
        public string Read()
        {
            return Console.ReadLine();
        }
    }
    public struct EmployeeDetails
    {
        Employee name;
        Employee address;
        Employee telephone;
        Employee dept;
        Employee sal;
        public Employee Name
        {
            get { return name; }
            set { name = value; }
        }
        public Employee Address
        {
            get { return address; }
            set { address = value; }
        }
        public Employee Telephone
        {
            get { return telephone; }
            set { telephone = value; }
        }
        public Employee Department
        {
            get { return dept; }
            set { dept = value; }
        }
        public Employee Salary
        {
            get { return sal; }
            set { sal = value; }
        }
        public void ShowAllDetails()
        {
            Employee emp = new Employee();
            Console.WriteLine("Employee Details Registration System.");
            Console.WriteLine("----------------------------");
            Console.Write("Enter the Name of the Employee: ");
            name.Write = emp.Read();
            Console.Write("Enter the Address of the Employee: ");
            address.Write = emp.Read();
            Console.Write("Enter the Telephone of the Employee: ");
            telephone.Write = emp.Read();
            Console.Write("Enter the Department of the Employee: ");
            dept.Write = emp.Read();
            Console.Write("Enter the Salary of the Employee: ");
            sal.Write = emp.Read();
        }
    }
    class ShowEmployeeDetails
    {
        static void Main(string[] args)
        {
            string input = "";
            EmployeeDetails emp1 = new EmployeeDetails();
            emp1.ShowAllDetails();
            Console.WriteLine();
            Console.WriteLine("Showing Employee Details");
            Console.WriteLine("--------------------");
            Console.WriteLine("Name: {0}", emp1.Name.Write);
            Console.WriteLine("Address: {0}", emp1.Address.Write);
            Console.WriteLine("Telephone: {0}", emp1.Telephone.Write);
            Console.WriteLine("Department: {0}", emp1.Department.Write);
            Console.WriteLine("Salary: {0}", emp1.Salary.Write);
            Console.WriteLine("--------------------");
            Console.WriteLine("Press y to save the record....");
            input = Console.ReadLine();
            if (input == "y")
            {
                Console.WriteLine("Record Saved.");
            }
            else
            {
                Console.WriteLine("Record not saved.");
            }
        }
    }
```

Remarks The use of structure in a C# application allows you to manage the memory of a computer efficiently as all related data is organised in a structure. It also increases the performance of a C# application.

## Common Programming Errors

- Placing the semicolon at the end of structure definition.
- Using the upper case S in the keyword struct.
- Giving initial values to data fields inside struct definition.
- Trying to access a private member outside the struct definition.
- Assigning a structure of one type to a structure different type.
- Attempting to access a struct member by using only the member name.
- Placing the semicolon at the end of enum definition.
- Placing a comma after the last item in the enum list.
- Forgetting to use the dot operator to access enum members.
- In method calls, forgetting to cast int type values to enum type
- In method calls, passing the values outside the range of valid enum values.

## Review Questions

11.1 State whether the following statements are true or false. If false, correct the statement to make it true.
(a) Struct type data are stored on heap.
(b) It is faster to manipulate struct type data compared class type data.
(c) We cannot initialize a data field inside a struct definition.
(d) Structs are implicitly sealed and therefore no class or struct can derive from the struct.
(e) Like classes, structs support inheritance.

```
float b = MathOperation.divide(a,2.0F);
Console.WriteLine("b = " + b);
}
```

Output of Program 12.3:
    b = 10.0

Note that the static methods are called using class names. In fact, no objects have been created for use. Static methods have several restrictions:

- They can only call other static methods.
- They can only access static data.
- They cannot refer to this or base in any way. (Refer Section 12.17)

## 12.12 STATIC CONSTRUCTORS

Like any other static members, we can also have static constructors. A static constructor is called before any object of the class is created. This is useful to do any housekeeping work that needs to be done once. It is usually used to assign initial values to static data members.

A static constructor is declared by prefixing a static keyword to the constructor definition. It cannot have any parameters. Example:

```
class Abc
{
static Abc ()        //No parameters
{
    ....            //set values for static members here
}
....
}
```

Note that there is no access modifier on static constructors. It cannot take any. A class can have only one static constructor.

## 12.13 PRIVATE CONSTRUCTORS

C# does not have global variables or constants. All declarations must be contained in a class. In many situations, we may wish to define some utility classes that contain only static members. Such classes are never required to instantiate objects. Creating objects using such classes may be prevented by adding a private constructor to the class.

## 12.14 COPY CONSTRUCTORS

A copy constructor creates an object by copying variables from another object. For example, we may wish to pass an Item object to the Item constructor so that the new Item object has the same values as the old one.

price = item.price;

The copy constructor is invoked by instantiating an object of type Item and passing it the object to be copied. Example:

```
Item item2 = new Item (item1);
```

Now, item2 is a copy of item1.

## 12.15 DESTRUCTORS

A destructor is opposite to a constructor. It is a method called when an object is no more required. The name of the destructor is the same as the class name and is preceded by a tilde (~). Like constructors, a destructor has no return type. Example:

```
class Fun
{
    ...
    ~Fun () //No arguments
    {
        ...
    }
}
```

Note that the destructor takes no arguments.

C# manages the memory dynamically and uses a garbage collector, running on a separate thread, to execute all destructors on exit. The process of calling a destructor when an object is reclaimed by the garbage collector is called finalization.

## 12.16 MEMBER INITIALIZATION

In addition to using constructors and methods to provide initial values to the objects, C# also allows us to assign initial values to individual data members at the time of declaration. Example:

```
class Initialization
{
    int number = 100;
    static double x = 1.0;
    string name = "John";
    Vehicle car = new vehicle (800, "maruti");
    ...
}
```

Note that other object-oriented languages like C++ and Java do not support this feature. When the variables are provided with the initial values at the time of declaration, the values are assigned as follows:

- Static variables are assigned when the class is loaded.
- Instance variables are assigned when an instance is created.

If the variables are not provided with the initial values as above, then they are assigned default values as dictated by their types. This is done as follows:

- Static variables are initialized to their default values when the class is loaded.
- Instance variables are initialized to their default values when an instance is created.

Thus a variable is never "uninitialized" in C#.
