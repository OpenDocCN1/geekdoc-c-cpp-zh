# Class Inheritance and Virtual Functions

The solution is simple. You need the calls to be resolved dynamically — as the program is executed. You can organize this by using virtual destructors in your classes. As I said when I first discussed virtual functions, it's sufficient to declare a base class function as virtual to ensure that all functions in any derived classes with the same name, parameter list and return type are virtual as well. This applies to destructors just as it does to ordinary member functions. You need to add the keyword virtual to the definition of the destructor in the class CContainer in Container.h so that the class definition is as follows:

```
class CContainer        // Generic base class for containers
{
    public:

        // Destructor
        virtual ~CContainer()
        { cout << "CContainer destructor called" << endl; }

        // Rest of the class as before
};
```

Now the destructors in all the derived classes are automatically virtual, even though you don't explicitly specify them as such. Of course, you're free to specify them as virtual if you want the code to be absolutely clear.

If you rerun the example with this modification, it produces the following output:

```
CBox usable volume is 24
Delete CBox
CBox destructor called
CContainer destructor called

CBox usable volume is 102
Delete CGlassBox
CGlassBox destructor called
CBox destructor called
CContainer destructor called

Volume is 45.9458
CBox usable volume is 20.4
CGlassBox destructor called
CBox destructor called
CContainer destructor called
CCan destructor called
CContainer destructor called
```

As you can see, all the objects are now destroyed with a proper sequence of destructor calls. Destroying the dynamic objects produces the same sequence of destructor calls as the automatic objects of the same type in the program.

The question may arise in your mind at this point, can constructors be declared as virtual? The answer is no — only destructors and other member functions.