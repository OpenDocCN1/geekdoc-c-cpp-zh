Program 11.6 will output the following:
    d1 = 0
    d2 = 10
    d3 = 11
    d4 = 12

# Case Study

# Problem Statement

CompTech is a medium sized organisation that is involved in the sale of computer hardware. It also has a small software development department, which develops customised software and Web sites for different organisations. CompTech has been till now manually maintaining the records of its employees, which is time consuming and decreases the efficiency of the HR department staff. How can CompTech solve the problem?

# Solution

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
```