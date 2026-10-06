```
void SphereColor::setColor(Color newColor)
{
    sphereColor = newColor;
    // setColor
}
Color SphereColor::getColor() const
{
    return sphereColor;
    // getColor
}
```

Notice how the constructors for the class SphereInColor and Sphere(initialRadius). The derived class needs the initialization of the data members in the base class that the base-class constructors can provide. The derived-class constructors then add initializations that are specific to the derived class.

Here is a function that uses the class SphereColor:

```
void useSphereInColor()
{
    SphereInColor ball(RED);
    ball.setRadius(5.0);
    cout << "The ball diameter is " << ball.getDiameter() << endl;
    ball.setColor(BLUE);
}
```

An instance of a derived class can invoke public methods of the base class

This function uses the constructor and the method setColor from the derived class SphereInColor. It also uses the methods setRadius and getDiameter that are defined in the base class Sphere.

# A.9 Libraries

One of the advantages of modular programming is that you can implement modules independently of other modules. You might find it possible for several programs to use a particular module. As a result, you can build a library of modules that you can include in future programs.

Any library—a C++ standard library or one you write—has a corresponding header that provides information about the contents of the library. For standard libraries, the header is simply an abstraction that the compiler can map to a file or handle in a different manner. When using the standard libraries, you do not see the .h extension that extends the name of your header files.

You have already seen standard libraries, such as the ones that provide and output services. To use the modules in a library, use the include directive with the name of the header associated with the library. For example, you

```
#include <iostream>
using namespace std;
```

Appendix H provides a list of available headers.

User-defined libraries are typically organized into two files. One file, the header file, contains a definition for each class in the library that is available to your program. This file could also contain, for example, function declarations, constant definitions, typedef statements, enumerations, and other include statements. By convention, the name of a header file associated with a user-defined library ends in .h. The other file—the implementation file—contains definitions of the class methods that the header file declares. Typically, the name of an implementation file is in .cpp.

The assumption, of course, is that the files are in source form—that is, they need to be compiled. It would be much more efficient to compile the method definitions once, independent of any