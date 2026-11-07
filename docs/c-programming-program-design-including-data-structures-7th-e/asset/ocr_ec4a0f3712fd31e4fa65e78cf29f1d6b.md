In Chapter 9, you learned how to group data items that are of different types by using a `struct`. The definition of a `struct` given in Chapter 9 is similar to the definition of a C-struct. However, the members of a C++ `struct` can be data items as well as functions. C++ provides another structured data type, called a `class`, which is specifically designed to group data and functions. This chapter first introduces classes and explains how to use them and then discusses the similarities and differences between a `struct` and a `class`.

> > **NOTE**
> >
> > Chapter 9 is not a prerequisite for this chapter. In fact, a struct and a class have similar capabilities, as discussed in the section “A struct versus a class” in this chapter.

# ## Classes

Chapter 1 introduced the problem-solving methodology called **object-oriented design (OOD)**. In OOD, the first step is to identify the components, called **objects**. An object combines data and the operations on that data in a single unit. In C++, the mechanism that allows you to combine data and the operations on that data in a single unit is called a class. Now that you know how to store and manipulate data in computer memory and how to construct your own functions, you are ready to learn how objects are constructed. This and subsequent chapters develop and implement programs using OOD. This chapter first explains how to define a class and use it in a program.

A **class** is a collection of a fixed number of components. The components of a class are called the **members** of the class.

The general syntax for defining a class is:

```
~~~cpp
class classIdentifier
{
    classMembersList
};
~~~
```

in which `classMembersList` consists of variable declarations and/or functions. That is, a member of a class can be either a variable (to store data) or a function (to manipulate data).

For example, the following statements define the `class courseType`, with variables and functions, to implement the basic properties of a course.

```
~~~cpp
class courseType
{
public:
    void setCourseInfo(string cName, string cNo, int credits);
    void print() const;
    int getCredits();
    string getCourseNumber();
    string getCourseName();
};
~~~
```