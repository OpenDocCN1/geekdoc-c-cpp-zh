# Accessing the Current Object 253

This description is quite similar to people's names. Within my family, I am known as Stephen. (Actually, within my family, I am known by my middle name, but you get the point.) No other Stephens are within my family (at least not within close family). However, two other Stephens work where I do.

If I'm at lunch with coworkers and the other Stephens aren't present, the name 'Stephen' clearly refers to me. Back in the trenches (or cubicles), shouting 'Stephen' is ambiguous because it can refer to any one of us. In context, you need to yell out 'Stephen Davis' as opposed to 'Stephen Williams' or 'Stephen Leija'.

Thus, you can consider Address() to be the first name or nickname of a method, with its class as the family name.

# Accessing the Current Object

Consider the following Student.SetName() method:

```
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

```
student1.SetName("Joseph", "Smith");
```