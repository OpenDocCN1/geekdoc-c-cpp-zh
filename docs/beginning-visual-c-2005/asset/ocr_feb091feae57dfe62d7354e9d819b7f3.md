The volume of box1 is calculated using the member function Volume() as in the previous example and is then displayed on the screen. You also display the value of the volume of cigarBox. The output from the example is:

```
Constructor called.
Constructor called.
Volume of box1 = 33696
Volume of cigarBox = 40
```

The first two lines are output from the two calls of the constructor CBox(), once for each object declared. The constructor that you have supplied in the class definition is automatically called when a CBox object is declared, so both CBox objects are initialized with the initializing values appearing in the declaration. These are passed to the constructor as arguments, in the sequence that they are written in the declaration. As you can see, the volume of box1 is the same as before and cigarBox has a volume looking suspiciously like the product of its dimensions, which is quite a relief.

# The Default Constructor

Try modifying the last example by adding the declaration for box2 that we had previously:

```
CBox box2;    // Declare box2 of type CBox
```

Here, we’ve left box2 without initializing values. When you rebuild this version of the program, you get the error message:

```
error C2512: 'CBox': no appropriate default constructor available
```

This means that the compiler is looking for a default constructor for box2 (also referred to as the no-arg constructor because it doesn’t require arguments when it is called) because you haven’t supplied any initializing values for the data members. A default constructor is one that does not require any arguments to be supplied, which can be either a constructor that has no parameters specified in the constructor definition, or one whose arguments are all optional. Well, this statement was perfectly satisfactory in Ex7_02.cpp, so why doesn’t it work now?

The answer is that the previous example used a default no-argument constructor that was supplied by the compiler, and the compiler provided this constructor because you didn’t supply one. Because in this example you did supply a constructor, the compiler assumed that you were taking care of everything and didn’t supply the default. So, if you still want to use declarations for CBox objects that aren’t initialized, you have to include the default constructor yourself. What exactly does the default constructor look like? In the simplest case, it’s just a constructor that accepts no arguments; it doesn’t even need to do anything:

```
CBox()    // Default constructor
{}        // Totally devoid of statements
```

You can see such a constructor in action.