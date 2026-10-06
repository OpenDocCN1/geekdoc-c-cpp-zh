
3. Add two properties that get and set idNumber and lastName. By convention, properties have an identifier that is the same as the field they service, except they start with a capital letter.

```csharp
public int IdNumber
{
    get {
        return idNumber;
    }
    set {
        idNumber = value;
    }
}
public string LastName
{
    get {
        return lastName;
    }
    set {
        lastName = value;
    }
}
```

4. Add the following set accessor in the property for the gradePointAverage field. It sets limits on the value assigned, assigning 0 if the value is out of range.

```csharp
public double GradePointAverage
{
    get {
        return gradePointAverage;
    }
    set {
        if(value >= LOWEST_GPA && value <= HIGHEST_GPA)
            gradePointAverage = value;
        else
            gradePointAverage = LOWEST_GPA;
    }
}
```

# CHAPTER 9 Using Classes and Objects

(continued)

- 5. Add a closing brace for the class. Save the file as CreateStudents.cs.

- 6. At the top of the file, begin a program that creates two Student objects, assigns some values, and displays the Students.

```csharp
using System;
using System.Console;
class CreateStudents
{
```

- 7. Add a Main() method that declares two Students. Assign field values, including one "illegal" value—a grade point average that is too high.

```csharp
static void Main()
{
Student first = new Student();
Student second = new Student();
first.IdNumber = 123;
first.LastName = "Anderson";
first.GradePointAverage = 3.5;
second.IdNumber = 789;
second.LastName = "Daniels";
second.GradePointAverage = 4.1;
```

- 8. Instead of creating similar Line() statements to display the two Students, call a method with each Student. You will create the method to accept a Student argument in the next step. Add a closing brace for the Main() method.

```csharp
Display(first);
Display(second);
}
```

- 9. Write the Display() method so that the passed-in Student's IdNumber, LastName, and GradePointAverage are displayed and aligned. Add a closing brace for the class.

```csharp
static void Display(Student stu)
{
WriteLine("{0, 5} {-10}{2, 6}", stu.IdNumber, stu.LastName, stu.GradePointAverage.ToString("F1"));
}
```

Recall that field contents are left-aligned when you use a minus sign before the field size. Also recall that the "F1" argument to the ToString() method causes the value to be displayed with one decimal place.

(continues)

# More About public and private Access Modifiers

(continued)

- 10. Save the file, and compile and execute the program. Figure 9-13 shows each Student has unique data values and uses the same Display() method. Notice how the second Student's grade point average was forced to 0 by the set accessor in the property for the field.

| 123 Anderson | 3.5 |
|---|---|
| 789 Daniels | 0.0 |

**Figure 9-13** Output of the CreateStudents program

When a property's get returns the corresponding field's value, and its set accessor simply assigns a value to the appropriate field, you can reduce the code in your classes using auto-implemented properties. In the Student class, both IdNumber and LastName are candidates for this shortcut, so you can replace the full versions of these properties with auto-implemented versions. The GradePointAverage property cannot take advantage of auto-implementation because additional code is required for the property to fulfill its intended function.

- 1. Open the file that contains the Student class if it is not open on your screen. Remove the properties for IdNumber and LastName and replace them with auto-implemented versions:
```csharp
public int IdNumber {get; set;}
public string LastName {get; set;}
```
- 2. Remove the declarations for the fields IdNumber and LastName.
- 3. Save the file, and recompile and execute. The output is the same as when the program used the original version of the Student class in Figure 9-13.

# More About public and private Access Modifiers

Most of the time, a class's data fields are private and its methods are public. This technique ensures that data will be used and changed only in the ways provided by accessors. Novice programmers might make a data field public to avoid having a property containing get and set accessors. However, doing so violates a basic principle of object-oriented programming. Data should be hidden when possible, and access to it should be controlled by well-designed accessors.

Although private fields and public methods are the norm, occasionally you need to create public fields or private methods. Consider the Carpet class shown in Figure 9-14. Although it contains several private data fields, this class also contains one public field (shaded). Following the three property declarations, one private method is defined (also shaded).

```csharp
class Carpet {
    public const string MOTTO="Our carpets are quality-made";
    private int length;
    private int width;
    private int area;
    public int length {
        get {
            return length;
        }
        set {
            length = value;
            CalcArea();
        }
    }
    public int width {
        get {
            return width;
        }
        set {
            width = value;
            CalcArea();
        }
    }
    public int Area {
        get {
            return area;
        }
    }
    private void CalcArea() {
        area = length * width;
    }
}
```

**Figure 9-14** The Carpet class

When you create Carpet objects from the class in 9-14, each Carpet will have its own length, width, and area, but all Carpet objects have the same MOTTO. The field MOTTO is preceded by the keyword const, meaning MOTTO is constant. That is, no program can change its value. Making a constant public does not violate information hiding in the way that making an object's data fields public does.

When you define a named constant within a class, it is always static, even though you use the keyword static as modifier. In other words, the field belongs to the entire class, not to any particular instance of the class. When you create a static field, only one copy is stored for the entire class, no matter how many objects instantiate. When you use a static constant in a client class, you use the class name and dot rather than an object name, as in Carpet.MOTTO. Built-in C# classes contain useful constants, such as Math.PI, which contains the value of pi. You do not create a Carpet object to use pi; therefore it is static.

Throughout this book, you have been using static to describe the Main() method of a class. You do not need to create an object of any class that contains a Main() method to be able to use Main().

Figure 9-15 shows a program that instantiates and uses a Carpet object, and Figure 9-16 shows the results when the program executes. Notice, although the output statements require an object to use the Width, Length, and Area properties, MOTTO is referenced using the class name only.

```csharp
using static System.Console;
class TestCarpet
{
    static void Main()
    {
        Carpet aRug = new Carpet();
        aRug.Width = 12;
        aRug.Length = 14;
        Write("The {0}x{1}", aRug.Width, aRug.Length);
        WriteLine("has an area of {0}", aRug.Area);
        WriteLine("Our motto is: {0}", Carpet.MOTTO);
    }
}
```

**Figure 9-15** The TestCarpet program

# CHAPTER 9 Using Classes and Objects

The 12 X 14 carpet has an area of 168
Our motto is: Our carpets are quality-made

**Figure 9-16** Output of the TestCarpet

The Carpet class contains one private method named CalcArea(). As you examine the code in the TestCarpet class in Figure 9-15, notice that Width and Length are set using an assignment operator but Area is not. The TestCarpet class can make assignments to Width and Length because these properties are public. However, you would not want a client program to assign a value to Area because the assigned value might not agree with the Width and Length values. Therefore, the Area property is a read-only property—it does not contain a setter, and no assignments by clients are allowed. Instead, when Width or Length properties are changed, the private CalcArea() method is called from the accessor. Area method is defined as private because there is no reason for a client class to call CalcArea(). Programmers probably create private methods more frequently than they create public data fields. Some programmers feel that the best style is to use public methods that are nothing but a list of method calls with descriptive names. Then, the methods that actually do the work are all private.

# TWO TRUTHS & A LIE

# More About public and private Access Modifiers

- 1. Good object-oriented techniques require that data should usually be hidden and access to it should be controlled by well-designed accessors.
- 2. Although private fields, methods, and accessors are the norm, occasionally you need to create public versions of them.
- 3. When you define a named constant within a class, it is always static; that is, the field belongs to the entire class, not to any particular instance of the class.

> The false statement is #2. Although private methods are the norm, occasionally you need to create public versions of private fields and accessors. private methods.
