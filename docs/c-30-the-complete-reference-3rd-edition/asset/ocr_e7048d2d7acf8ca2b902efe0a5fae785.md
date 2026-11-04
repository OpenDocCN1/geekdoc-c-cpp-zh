# # 11 CHAPTER

# Inheritance

Inheritance is one of the three foundational principles of object-oriented programming because it allows the creation of hierarchical classifications. Using inheritance, you can create a general class that defines traits common to a set of related items. This class can then be inherited by other, more specific classes, each adding those things that are unique to it.

In the language of C#, a class that is inherited is called a *base class*. The class that does the inheriting is called a *derived class*. Therefore, a derived class is a specialized version of a base class. It inherits all of the variables, methods, properties, and indexers defined by the base class and adds its own unique elements.

# ## Inheritance Basics

C# supports inheritance by allowing one class to incorporate another class into its declaration. This is done by specifying a base class when a derived class is declared. Let’s begin with an example. The following class called **TwoDShape** stores the width and height of a two-dimensional object, such as a square, rectangle, triangle, and so on.

```
    // A class for two-dimensional objects.
    class TwoDShape {
        public double Width;
        public double Height;

        public void ShowDim() {
            Console.WriteLine("Width and height are " +
                              Width + " and " + Height);
        }
    }
```

**TwoDShape** can be used as a base class (that is, as a starting point) for classes that describe specific types of two-dimensional objects. For example, the following program uses **TwoDShape** to derive a class called **Triangle**. Pay close attention to the way that **Triangle** is declared.

```
    // A simple class hierarchy.
```