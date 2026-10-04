
The following example demonstrates this technique:

![](img/6df7bb88e9302e98442acc219cfbd7fc_272_0.png)

```cs
// InvokeMethod -- Invoke a member method through the object.
using System;
namespace InvokeMethod
{
    class Student
    {
        // The name information to describe a student
        public string firstName;
        public string lastName;
        // SetName -- Save name information. (Nonstatic.)
        public void SetName(string fName, string lName)
        {
            firstName = fName;
            lastName = lName;
        }
        // ToNameString -- Convert the student object into a
        //      string for display. (Nonstatic.)
        public string ToNameString()
        {
            string s = firstName + " " + lastName;
            return s;
        }
    }
    public class Program
    {
        public static void Main()
        {
            Student student = new Student();
            student.SetName("Stephen", "Davis"); // Call instance method.
            Console.WriteLine("Student's name is "
                + student.ToNameString());
            // Wait for user to acknowledge.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
```

The output from this program is this simple line:

```
Student's name is Stephen Davis
```

Other than having a much shorter name, this program is quite similar to the earlier StudentClassWithMethods program. This version uses nonstatic methods to manipulate both a first and last name.

The program begins by creating a new Student object, student. The program then invokes the SetName() method, which stores the two strings "Stephen" and "Davis" into the data members firstName and lastName. Finally, the program calls the member method ToNameString(), which returns the name of the student by concatenating the two strings.

Book II
Chapter 4

Let Me Say This about this

Look again at the SetName() method, which updates the first and last name fields in the Student object. To see which object SetName() modifies, consider this example:

```cs
Student christa = new Student();  // Here's one student.
Student sarah = new Student();  // And here's a completely different one.
christa.SetName("Christa", "Smith");
sarah.SetName("Sarah", "Jones");
```

The first call to SetName() updates the first and last name of the christa object. The second call updates the sarah object.

Thus, C# programmers say that a method operates on the current object. In the first call, the current object is christa; in the second, it's sarah.

![](img/6df7bb88e9302e98442acc219cfbd7fc_273_0.png)

# Expanding a method's full name

A subtle but important problem exists with my description of method names. To see the problem, consider this sample code snippet:

```cs
public class Person
{
    public void Address()
    {
        Console.WriteLine("Hi");
    }
}
public class Letter
{
    string address;
    // Store the address.
    public void Address(string newAddress)
    {
        address = newAddress;
    }
}
```

Any subsequent discussion of the Address() method is now ambiguous. The Address() method within Person has nothing to do with the Address() method in Letter. If my programmer friend tells me to access the Address() method, which Address() does he mean?

The problem lies not with the methods themselves, but, rather, with my description. In fact, no Address() method exists as an independent entity — only a Person.Address() and a Letter.Address() method. Attaching the class name to the beginning of the method name clearly indicates which method is intended.

This description is quite similar to people's names. Within my family, I am known as Bill. (Actually, my family usually just yells, "Hey you," but this is just an example.) No other Bills are within my family (at least not within my close family). However, two other Bills work where I do.

If I’m at lunch with coworkers and the other two Bills aren’t present, the name Bill clearly refers to me. Back in the trenches (or cubicles), shouting “Bill” is ambiguous because it can refer to any one of us. In that context, you need to yell out “Bill Sempf” as opposed to “Bill Davis” or “Bill Rogers.”

Thus, you can consider Address() to be the first name or nickname of a method, with its class as the family name.

# Accessing the Current Object

Consider the following Student.SetName() method:

```cs
class Student
{
    // The name information to describe a student
    public string firstName;
    public string lastName;
    // SetName -- Save name information.
    public void SetName(string firstName, string lastName)
    {
        firstName = firstName;
        lastName  = lastName;
    }
}
public class Program
{
    public static void Main()
    {
        Student student1 = new Student();
        student1.SetName("Joseph", "Smith");
        Student student2 = new Student();
        student2.SetName("John", "Davis");
    }
}
```

The method Main() uses the SetName() method to update first student1 and then student2. But you don’t see a reference to either Student object within the method.

In C#, the `this` keyword is used to refer to the current instance of a class. When method parameters have the same name as data members, you use `this` to distinguish between the two. For example:

```cs
class Student
{
    public string firstName;
    public string lastName;
    public void SetName(string firstName, string lastName)
    {
        this.firstName = firstName;
        this.lastName = lastName;
    }
}
```

The addition of `this` clarifies which name is intended. Within `SetName()`, `firstName` refers to the method argument, but `this.firstName` refers to the data member.

# What is this?

You don't normally need to refer to this explicitly because it is understood where necessary by the compiler. However, two common cases require this. You may need it when initializing data members, as in this example:

```cs
class Person
{
    public string name; // This is this.name.
    public int id;      // And this is this.id.
    public void Init(string name, int id) // These are method arguments.
    {
        this.name = name; // Argument names same as data member names
        this.id = id;
    }
}
```

The arguments to the `Init()` method are named name and id, which match the names of the corresponding data members. The method is then easy to read because you know immediately which argument is stored where. The only problem is that the name name in the argument list obscures the name of the data member. The compiler needs `this` to resolve the ambiguity.
