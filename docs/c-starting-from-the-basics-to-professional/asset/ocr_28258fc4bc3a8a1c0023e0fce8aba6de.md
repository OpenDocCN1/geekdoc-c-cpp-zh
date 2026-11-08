The definitions of the member functions of the Truckload class need to be changed to access the member variables of the Package class directly. This is trivial. Just replace all occurrences of getBox(), getNext(), and setNext() in Truckload.cpp with code that directly accesses the corresponding member variable. The resulting Truckload class definition with Package as a nested class will work with the Ex12_17.cpp source file. A working example is available in the code download as Ex12_18.

> > **Note** Nesting the Package class inside the Truckload class simply defines the Package type in the context of the Truckload class. Objects of type Truckload aren't affected in any way—they'll have the same members as before.

Member functions of a nested class can directly reference static members of the enclosing class, as well as any other types or enumerators defined in the enclosing class. Other members of the enclosing class can be accessed from the nested class in the normal ways: via a class object or a pointer or a reference to a class object. When accessing members of the outer class, the member functions of a nested class have the same access privileges as member functions of the outer class; that is, member functions of a nested class are allowed to access the private members of objects of the outer class.

# ## Nested Classes with Public Access

Of course, you could put the Package class definition in the public section of the Truckload class. This would mean that the Package class definition was part of the public interface so it *would* be possible to create Package objects externally. Because the Package class name is within the scope of the Truckload class, you can't use it by itself. You must qualify the Package class name with the name of the class in which it is nested. Here's an example:

```
```cpp
Truckload::Package myPackage{ myBox };    // Define a Package object
```
```

Of course, making the Package type public in the example would defeat the rationale for making it a nested class in the first place! That said, there can be other circumstances where a public nested class makes sense. We'll see one such example in the next subsection.

# ## A Better Mechanism for Traversing a Truckload: Iterators

The getFirstBox() and getNextBox() members allowed you to traverse all Boxes stored in a Truckload. It is not unheard of to add analogous members to a class—we have encountered it on at least two occasions in real code—but this pattern has some serious flaws. Perhaps you can already think of one?

Suppose you find—rightly so—that the main() function of Ex12_17 is too long and crowded and you decide to split off some of its functionality in reusable functions. A good first candidate would then be a helper function to find the largest Box in a Truckload. A natural way to write this is as follows:

```
```cpp
SharedBox findLargestBox(const Truckload& truckload)
{
    SharedBox largestBox{ truckload.getFirstBox() };

    SharedBox nextBox{ truckload.getNextBox() };
    while (nextBox)
```
```