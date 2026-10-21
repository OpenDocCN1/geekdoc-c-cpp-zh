The variables of the fundamental types don’t allow you to model real-world objects (or even imaginary objects) adequately. It’s hard to model a box in terms of an int, for example; however, you can use the members of a struct to define a set of attributes for such an object. You could define variables, length, width, and height to represent the dimensions of the box and bind them together as members of a Box structure, as follows:

```
struct Box
{
    double length;
    double width;
    double height;
};
```

With this definition of a new data type called Box, you define variables of this type just as you did with variables of the basic types. You can then create, manipulate, and destroy as many Box objects as you need to in your program. This means that you can model objects using structs and write your programs around them. So — that’s object-oriented programming all wrapped up then?

Well, not quite. You see, object-oriented programming (OOP) is based on a number of foundations (famously encapsulation, polymorphism, and inheritance) and what you have seen so far doesn’t quite fit the bill. Don’t worry about what these terms mean for the moment — you’ll be exploring that in the rest of this chapter and throughout the book.

The notion of a struct in C++ goes far beyond the original concept of struct in C — it incorporates the object-oriented notion of a class. This idea of classes, from which you can create your own data types and use them just like the native types, is fundamental to C++, and the new keyword class was introduced into the language to describe this concept. The keywords struct and class are almost identical in C++, except for the access control to the members, which you will find out more about later in this chapter. The keyword struct is maintained for backwards compatibility with C, but everything that you can do with a struct and more, you can achieve with a class.

Take a look at how you might define a class representing boxes:

```
class CBox
{
    public:
        double m_Length;
        double m_Width;
        double m_Height;
};
```

When you define CBox as a class you are essentially defining a new data type, similar to when you defined the Box structure. The only differences here are the use of the keyword class instead of struct, and the use of the keyword public followed by a colon that precedes the definition of the members of the class. The variables that you define as part of the class are called data members of the class, because they are variables that store data.

You have also called the class CBox instead of Box. You could have called the class Box, but the MFC adopts the convention of using the prefix C for all class names, so you might as well get used to it. MFC also prefixes data members of classes with m_ to distinguish them from other variables, so I’ll use this