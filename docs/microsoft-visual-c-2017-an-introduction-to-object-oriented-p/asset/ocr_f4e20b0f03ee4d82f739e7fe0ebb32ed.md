# CHAPTER 10 Introduction to Inheritance

The Object class contains other nonfiction and nonistance (static) methods in addition to the four methods listed in Table 10-1. The C# documentation provides details on these methods.

# Using the Object Class's GetType() Method

The GetType() method returns an object's type, or class. For example, if you have created an Employee object named someWorker, then the following statement displays *Employee: WriteLine(someWorker.GetType());*

If an object's class is defined in a namespace, then GetType() returns a string composed of the namespace, date, and the class name.

# Using the Object Class's ToString() Method

The Object class methods are not very useful as they stand. For example, when you use the Object class's ToString() method with an object, it simply returns a string that holds the name of the class, just as GetType(). That is, if *someWorker* is an Employee, then the following statement displays Employee:

*WriteLine(someWorker.ToString());*

When you create a class as Employee, you often want to override the Object class's ToString() method with your own, more useful version—perhaps one that returns an Employee's ID number, or a combination of two. To do the same thing—perhaps GetEmployeeIdentification() or ConvertEmployeeToString(). However, by naming your class method ToString(), you make the class easier for others to understand and use; when you use it with objects, you can provide a useful set of information. A class *ToString()* method is often a useful debugging aid.

For example, you might create an Employee class ToString() method, as shown in Figure 10-23. This method assumes that IdNum and *Name* are *Employee* properties with access. The returned *string* will have a value such as *Employee: 234 Johnson.

```
public override string ToString()
{
    return(getType() + ": " + IdNum + " " " " + Name);
}
```

**Figure 10-23** An Employee class ToString() method

You have using an overloaded version of the ToString() method since Chapter 2, where you can format numeric output when you pass a string such as "F3" or "C2" to the ToString()

method.