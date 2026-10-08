
# Defining Methods 249

```cs
// A revised SetName():
public static void SetName(Student student, string name)
{
    student = new Student(); // Doesn't replace student outside SetName()
    student.name = name;
}
```

# Defining Methods

A class is supposed to collect the elements that describe a real-world object or concept. For example, a Vehicle class may contain data elements for maximum velocity, weight, and carrying capacity for example. However, a Vehicle has active properties—behaviors—as well as the ability to start and stop. These active properties are described by the methods related to their vehicular data. These methods are just as much a part of the Vehicle class as the data elements.

# Defining a static method

For example, you could rewrite the program from the previous section in a slightly better way:

```cs
// StudentClassWithMethods -- Demonstrate putting methods that
// operate on a class's data inside the class. A class is
// responsible for its own data and any operations on it.
// using System;
namespace StudentClassWithMethods
{
    // Now the OutputName and SetName methods are members of
    // class Student, not class Program.
    public class Student
    {
        public string name;
        // OutputName -- Output the student's name.
        public static void OutputName(Student student)
        {
            Console.WriteLine("Student's name is ({0})", student.name);
        }

        // SetName -- Modify the object's name.
        public static void SetName(Student student, string name)
        {
            student.name = name;
        }
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            Student student = new Student();
            // Set the name by accessing it directly.
            Console.WriteLine("The first time:");
            student.name = "Madeleine";
        }
    }
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_274_0.png)

# 250 Defining Methods

```cs
Student.OutputName(student); // Method now belongs to Student.
// Change the name using a method.
Console.WriteLine("After being modified:");
Student.SetName(student, "Willa");
Student.OutputName(student);
// Wait for user to acknowledge.
Console.WriteLine("Press Enter to terminate...*
Console.Read();
```

Other than its name, this program has one significant change from the PassObject in the previous section: I put the OutputName() and SetName() methods in the Student class.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_275_0.png)

Because of that change, Main() must refer the Student class in the calls to SetName() and OutputName(). The methods are now members of the class Student and not Program, the class in which Main() resides.

This step is small but significant. Placing OutputName() within the class leads to a higher level of reuse: Outside methods that need to display the object can find OutputName() right as part of the class. It doesn't have to be written separately by each program using the Student class.

This solution is also better on a philosophical level. Class Program shouldn't need to worry about how to initialize the name of a Student object nor how to output important material. The Student class should contain that information. Objects are responsible for themselves.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_275_1.png)

In fact, Main() shouldn't initialize the name to Madeline in the first place. It should call SetName() instead.

From within Student, one member method can invoke without explicitly applying the class name. SetName() could invoke OutputName() without needing to reference the class name. If you leave the class name, C# ensures that the method being accessed is in or on the same class.

# Defining an instance method

Although OutputName() and SetName() are static methods, they could be either nonstatic, or instance, methods.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_275_2.png)

All static members of a class are class members, and all nonstatic members are instance members. This includes methods.

The nonstatic data members of an object — an instance of a class — are accessed with the object and not the class. Thus, you may say

```cs
Student student = new Student(); // Create an instance of Student.
student.name = "Madeleine"; // Access the member via the instance.
```

C# enables you to invoke nonstatic methods in the same way:

```cs
student.SetName("Madeleine");
```

The following example demonstrates this technique:

```cs
// InvokeMethod -- Invoke a method through the object.
using System;
namespace Student
class Student
{
    // The name information to describe a student
    public string firstName;
    public string lastName;
    // SetName - Save name information. (Nonstatic).
    public void SetName(string fName, string lName)
    {
        firstName = fName;
        lastName = lName;
    }
    // ToName -- Convert the student object into a
    // string for display. (Nonstatic).
    public string ToName()
    {
        string s = firstName + " * " + lastName;
        return s;
    }
    public static void Main()
    {
        Student student = new Student();
        student.SetName("Stephen", "David"); // Call instance method.
        Console.WriteLine("Student's name is " + student.ToName());

        // Wait for user to acknowledge.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_276_0.png)

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_276_1.png)

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_276_2.png)

The output from this program is this simple line:

Student's name is Stephen David

Other than having a much shorter name, this program is quite similar to the earlier StudentClassWithMethods program. This version uses nonstatic methods to manipulate both a first and last name.

# 252 Defining Methods

The program begins by creating a new Student object, student. The program invokes the SetName() method, which stores the strings "Stephen" and "Davis" into the data members firstName and lastName. Finally, the program calls the member method ToString(), which returns the name of the student by concatenating the strings.

Look again at the SetName() method, which updates the first and last name fields in the Student object. To see how SetName() modifies this example:

```cs
Student christa = new Student();           // Here's one student.
Student sarah = new Student();              // And here's a completely different one.
christa.SetName("Christa", "Smith");
sarah.SetName("Sarah", "Jones");
```

The first call to SetName() updates the first and last name of the christa object. The second call updates the sarah object.

Thus, C# methods that operate on the current object. In the first call, the current object is christa; in the second, it's sarah.

# Expanding a method's full name

A subtle but important problem exists with method description. To see the problem, consider this sample:

```cs
public class Person {
    public void Address()
    {
        Console.WriteLine("Hi");
    }
}
public class Letter {
    string address;
    // Store the address.
    public void Address(string newAddress)
    {
        address = newAddress;
    }
}
```

Any subsequent discussion of Address() is now ambiguous. The problem lies not with the methods themselves, but with description. In fact, no Address() exists as an independent entity — only Person.Address() and Letter.Address(). Attaching the class name to the beginning of the method clearly indicates which is intended.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_277_0.png

This description is quite similar to people's names. Within my family, I am known as Stephen. (Actually, within my family, I am known by my middle name, but you get the point.) No other Stephens are within my family (at least not within close family). However, two other Stephens work where I do.

If I'm at lunch with coworkers and the other Stephens aren't present, the name 'Stephen' clearly refers to me. Back in the trenches (or cubicles), shouting 'Stephen' is ambiguous because it can refer to any one of us. In context, you need to yell out 'Stephen Davis' as opposed to 'Stephen Williams' or 'Stephen Lewis'.

Thus, you can consider Address() to be the first name or nickname of a method, with its class as the family name.

# Accessing the Current Object 253

Consider the following Student.SetName() method:

```cs
class Student {
    // The name information to describe a student
    public string firstName;
    public string lastName;
    // setName Save name information.
    public void SetName(string firstName, string lastName) {
        firstName = firstName;
        lastName = lastName;
    }
}
class Program {
    public static void main() {
        Student student1 = new Student();
        student1.SetName("Joseph", "Smith");
        Student student2 = new Student();
        student2.SetName("John", "Davis");
    }
}
```

The method uses the SetName() method to update first student1 and then student2. But you don't have a reference to each other object within SetName() itself. In fact, no reference to a Student object exists. A method is said to operate on "the current object." How does a method know which one is the current object? Will the current object please stand up?

The answer is simple. The current object is passed as an implicit argument in a call to the method — for example:

```cs
student1.SetName("Joseph", "Smith");
```
