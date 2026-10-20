
## Perspective

In this chapter, you learned how to work with interfaces. Depending on the type of programming that you’re doing, you may or may not need to define your own interfaces. However, understanding interfaces is critical to working with .NET and to using an object-oriented language like C#.

You also learned how to define classes and interfaces that use generics. This allows you to create collection classes and interfaces that can accept any data type and still be type-safe. Again, depending on the type of programming that you’re doing, you may never need to create these types of custom collection classes. However, understanding generics helps you understand the inner workings of the generic .NET collection classes.

Now that you’ve completed this chapter, you have all of the critical skills you need for developing object-oriented programs. In the next chapter, though, you’ll learn some new skills for documenting and organizing these classes. This will make it easier for you to share the classes that you develop with other programmers.

## Terms

- interface
- implement an interface
- multiple inheritance
- default interface member
- shallow copy
- deep copy
- default method
- generics
- constraint

## Exercise 15-1    Implement the ICloneable interface

In this exercise, you’ll create an application that includes a Customer class that implements the ICloneable interface. This application creates a List<> that contains clones of a pre-defined Customer object and displays the cloned customers in a list box as shown below. To make this application easier to develop, we’ll give you the starting form and classes.

### The design of the Clone Customer form

![](img/844f608d10a44654833ea5efc8a2e7a7_547_0.png)

### Development procedure

1. Open the application in the C:\C#\Chapter 15\CloneCustomer directory.
2. Display the code for the form, and notice that the Load event handler creates a Customer object, stores it in a variable named customer, and displays the customer in the label at the top of the form.
3. Modify the Customer class so it implements the ICloneable interface.
4. Add an event handler for the Click event of the Clone button. This event handler should use the methods in the Validator class to check the value in the Copies text box to be sure it’s an integer. Then, it should create a List<> object that contains the required number of clones of the Customer object. Finally, it should display the cloned customers in the list box.
5. Run the application and test it to make sure it works properly.

## Exercise 15-2   Implement an enumerator

In this exercise, you’ll modify your solution to exercise 15-1 so the clones are stored in a CustomerList object that implements an enumerator.

1. If it isn’t already open, open the application in the C:\C#\Chapter 15\Clone-Customer directory.
2. Implement the IEnumerable<Customer> interface for the CustomerList class. (This class wasn’t used by the previous exercise.) To do that, implement the GetEnumerator() method as described in figure 15-12.
3. Modify the code in the form class so it stores the cloned Customer objects in a CustomerList object rather than in a List<Customer> object.
4. Run the application and test it to be sure it works properly.

## How to organize, document, and test your classes

In the last four chapters, you learned how to develop object-oriented programs that use classes. Now, you’ll learn how to organize, document, and test your classes, and you’ll learn how to store your classes in class libraries. This makes it easier for other programmers to use your classes.

- **How to organize your classes** ..................................................528
- **How to code multiple classes in a single file** ..................................................528
- **How to split a single class across multiple files** ..................................................530
- **How to work with namespaces** ..................................................532
- **How to document your classes** ..................................................534
- **How to add XML documentation to a class** ..................................................534
- **How to view the XML documentation** ..................................................536
- **How to create and use class libraries** ..................................................538
- **How class libraries work** ..................................................538
- **How to create a class library project** ..................................................540
- **How to add a reference to a class library** ..................................................542
- **How to use the classes in a class library** ..................................................542
- **How to implement unit testing** ..................................................544
- **How unit testing works** ..................................................544
- **How to create a unit test project** ..................................................546
- **How to code unit tests** ..................................................548
- **How to run unit tests** ..................................................550
- **Perspective** ..................................................552

## How to organize your classes

In this topic, you’ll learn how to organize applications that use multiple classes by coding more than one class per file, by splitting a single class across multiple files, and by working with namespaces.

### How to code multiple classes in a single file

In most cases, you’ll code each class that’s required by an application in a separate file. If two or more classes are closely related, however, you might want to consider storing them in the same file. Figure 16-1 shows two ways you can do that.

First, you can simply code the class declarations one after the other as shown in the first example. The advantage of doing that is that it makes it easier to manage the files that make up the application. If the classes are large, however, you should place them in separate files even if they are closely related. Otherwise, it may be difficult to locate the code for a specific class.

You can also code two or more classes in a single file by nesting one class within another class. *Nested classes* are useful when one class only makes sense within the context of the other class. The second example in this figure illustrates how to nest two classes. Here, the class named InnerClass is nested within a class named OuterClass.

If you want to refer to the inner class from a class other than the outer class, you have to qualify it with the name of the outer class like this:

```
OuterClass.InnerClass ic = new OuterClass.InnerClass();
```

However, you typically only need to refer to the inner class from the outer class, and you can do that without qualifying the name of the inner class.

**A file with two classes coded one after the other**

```
public class Class1
{
    // Body of Class1
}

public class Class2
{
    // Body of Class2
}
```

**A file with nested classes**

```
public class OuterClass
{
    InnerClass ic = new InnerClass();    // code that uses the inner class
    // Body of OuterClass

    public class InnerClass
    {
        // Body of InnerClass
    }
}
```

**Description**

- When two classes are closely related, it sometimes makes sense to code them in the same file, especially if the classes are relatively small. That way, the project consists of fewer files.
- One way to code two classes in a single file is to code them one after the other as shown in the first example above.
- Another way to code two classes in a single file is to *nest* one class within the other as shown in the second example above. This is useful when one class is used only within the context of another class.
- To refer to a nested class from another class, you must qualify it with the name of the class it’s nested within like this:
  `OuterClass.InnerClass`
