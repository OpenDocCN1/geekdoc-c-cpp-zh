```
    Clutter(string name)
    {
        ChildName = name;
        Toys = 0;
    };
```

The compiler will figure out which overloaded constructor to use, based on the parameters. Therefore the overloaded constructors must differ in their parameter lists — specifically, this means the types of parameters; just changing the names doesn't count! If the parameter lists don't differ, the compiler won't be able to distinguish them, and you will get an error when it tries to compile the class definition.

![](bbox=[0.112, 0.333, 0.209, 0.397])

If your constructor doesn't have a parameter provided by other constructors, you should initialize the associated variable within the constructor code. For example, the second constructor doesn't include a parameter for Toys, so the constructor code initializes this variable to 0. As an alternative, you can use an initializer as described in the "Initializing members" section of the chapter.

![](bbox=[0.112, 0.439, 0.208, 0.505])

Having multiple constructors makes your class much more flexible and easy to use. Multiple constructors give the users of your class more ways to use the class, allowing them to configure the instances differently, depending on their situations. Further, the constructors force the user to configure the instances only in the ways your constructors allow.

# ### Initializing members

When C++ originally came out, any time you wanted to initialize a member variable, you had to put it inside a constructor. This created some interesting problems. The main problem had to do with references: You can put reference variables in a class, but normally reference variables must be initialized. You can't just have a reference variable floating around that doesn't refer to anything. But if you put a reference variable inside a class and create an instance of the class, the application will first create the instance and then call the constructor. Even if you initialize the reference in the first line of the constructor, there's still a moment when you have an uninitialized reference! Oh, what to do, what to do?

The ANSI standard uses a single approach for setting up member variables: initializers. An initializer goes on the same line as the constructor in the class definition; or, if the constructor isn't inline — defined within the class code block — the initializer goes with the constructor in the code outside the class definition.