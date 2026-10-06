# TWO TRUTHS & A LIE

# Understanding Constructors

+   1. Every class you create is automatically supplied with a public constructor with no parameters.

+   2. If you write a constructor for a class, you do not have a default constructor for the class.

+   3. Any constructor you write must have the same name as its class, and constructors cannot have a return type.

> The false statement is #2. If you write a parameterless constructor for a class, then the no longer becomes the default constructor, and you lose the automatically supplied version. If you only constructors that require parameters, then contains a default constructor.

# You Do It

# Adding Overloaded Constructors to a Class

In these steps, you add overloaded constructors to the Student class.

+   1. Open the file that contains the Student class if it is not still open on your screen. Just before the closing curly brace for the Student class, add the following constructor. It takes three parameters and assigns them to the appropriate fields:
```java
public Student(int id, string name, double gpa)
{
IdNumber = id;
LastName = name;
GradePointAverage = gpa;
}
```

+   2. Add a second parameterless constructor. It calls the first constructor, passing 0 for the ID number, "XXX" for the name, and 0.0 for the grade point average. Its body is empty.
```java
public Student() : this(0, "XXX", 0.0)
{
```

(continues)