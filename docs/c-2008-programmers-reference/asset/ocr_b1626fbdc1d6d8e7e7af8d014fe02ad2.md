# Inheritance

Inheritance is one of the fundamental concepts in object-oriented programming. Inheritance facilitates code reuse and allows you to extend the functionality of code that you have already written. This chapter looks at:

+   - [ ] How inheritance works
+   - [ ] Implementing inheritance in C#
+   - [ ] Defining abstract methods and classes
+   - [ ] Sealing classes and methods
+   - [ ] Defining overloaded methods
+   - [ ] The different types of access modifiers you can use in inheritance
+   - [ ] Using inheritance in interfaces

# Understanding Inheritance in C#

The following Employee class contains information about employees in a company:

```
```
public class Employee
{
    public string Name { get; set; }
    public DateTime DateofBirth { get; set; }
    public ushort Age()
    {
        return (ushort)(DateTime.Now.Year - this.DateofBirth.Year);
    }
}
```
```