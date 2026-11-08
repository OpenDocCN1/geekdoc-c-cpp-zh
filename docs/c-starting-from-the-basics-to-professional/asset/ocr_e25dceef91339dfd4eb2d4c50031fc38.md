constructor is *always* a reference to a `const` object of the same class type. In other words, the form of the copy constructor is the same for any class:

```
    MyClass::MyClass(const MyClass& object)
        : // Initialization list to duplicate all member variables
    {
        // Possibly some additional code to duplicate the object...
    }
```

Of course, the copy constructor may also delegate to other, non-copy constructors as well. Here's an example:

```
    Box::Box(const Box& box) : Box(box.m_length, box.m_width, box.m_height)
    {}
```

> > **Caution**
> > You should normally never write this copy constructor of `Box` yourself. The compiler already generates one just like it by default, so all that could come from defining one yourself are bugs (forgetting to copy one of the member variables) or maintenance issues (forgetting to update the copy constructor if member variables are added). Like we said, this was just to show you how you can define one. We'll return to the when you should in later chapters. (Spoiler alert: you should do so as little as possible; just let the compiler do all the work!)

# ## Deleting the Copy Constructor

So the compiler normally generates a copy constructor for every class, but what if that is not what you want? What if your `Box` objects contain highly precious cargo, barred by international copyright and trademark laws from being copied? All kidding aside, there can be any number of good reasons you do not want certain objects to be copied. If so, you can instruct the compiler not to generate a copy constructor by adding `= delete;` to its declaration in the class definition. For `Box`, this would look as follows:

```
    class Box
    {
    public:
        Box() = default;
        Box(double length, double width, double height);
        Box(const Box& box) = delete;  // Prohibit copy construction

        // Rest of the class as always...
    };
```

Once the copy constructor is deleted, statements such as the following will no longer compile:

```
    Box box3 {box2};   // Error: use of deleted constructor Box(const Box&)
```

Note that if any member variable of a class has a deleted or private copy constructor, the default copy constructor of that class is automatically implicitly deleted. In fact, even an explicitly defaulted copy constructor (which you can define using `=default;`) is then deleted.