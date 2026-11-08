# Chapter 18

While defining a class, first we need to provide the access modifier to state whether the class will be accessible from every file in the application or its access is restricted. Note that while using a console application, we need to write the Main() method to execute the code.

Now, let's learn how to write member variables and methods for a class using C#. Listing 18.2 shows the C# code containing the complete class definition:

Listing 18.2: Showing the Class Definition for the Employee Class

```
    using System;
    namespace Employee
    {
        class Program
        {
            public static void Main()
            {
                Employee emp = new Employee("George", "Mathew",
                                             "Associate", 20000, 100, 222);
                emp.IncrementSalary();
            }
        }
        public class Employee
        {
            //Declaring member variables
            public int Employee_ID;
            public string first_name;
            public string last_name;
            public string designation;
            public long salary;
            public int manager_ID;
            public int project_ID;
            //Declaring Constructors
            public Employee()
            {
            }
            //Declaring parameterized constructor
            public Employee(string firstName, string lastName,
                    string designation, long salary, int managerID, int projectID)
            {
                this.first_name = firstName;
                this.last_name = lastName;
                this.designation = designation;
                this.salary = salary;
                this.manager_ID = managerID;
                this.project_ID = projectID;
            }
            //Declaring member methods
            public void IncrementSalary()
            {
                if (designation == "Trainee")
                {
                    salary += 5000;
                    Console.WriteLine("The revised salary is {0}", salary);
                }
                else if (designation == "Associate")
                {
                    salary += 10000;
                    Console.WriteLine("The revised salary is {0}", salary);
                }
                else if (designation == "Manager")
```