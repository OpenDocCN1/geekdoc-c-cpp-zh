# C++ INTERLUDE 2 Pointers, Polymorphism, Memory Allocation

Next, we must change the function placeInBox to accept a pointer to a PlainBox<string> object:

```
void placeInBox(PlainBox<string>* theBox, const string item)
{
    theBox->setItem(item);
} // end placeInBox
```

The last change is to free the memory used by the variables in the free store by adding the statements to the program:

```
delete myPlainBoxPtr;
myPlainBoxPtr = nullptr;
delete myMagicBoxPtr;
myMagicBoxPtr = nullptr;
```

Our function placeInBox will now call the correct version of setItem according to the type of box pointed to its first argument.

The use of virtual methods has a significant impact on future use of a class. Imagine that you had compiled the class PlainBox and its implementation before you wrote the derived class MagicBox. If you wrote new MagicBox, assuming access to the compiled PlainBox, you could override getItem because it is virtual in PlainBox. As a result, you could change the behavior of instances of MagicBox, even though PlainBox was already compiled. That is, classes that define virtual methods are extensible. You can add capabilities to a derived class without having access to the source statements.

![](bbox=[0.0, 0.485, 1.0, 1.0])

+   * A virtual method is one that a derived class can override.
* You must implement a class's virtual methods. (Pure virtual methods are not included in this requirement).
* A derived class does not need to override an implementation of an inherited virtual method.
* Any of the class's methods may be virtual. However, if you do not want a derived class to override a particular method, the method should not be virtual.
* Constructors cannot be virtual.
* Destructors and should be virtual. Virtual destructors ensure that future descendants of the object deallocate themselves correctly.
* A virtual method's return type cannot be overridden.

# C2.5 Dynamic Allocation of Arrays

When you declare an array in C++ by using statements such as

An ordinary C++ array is statically allocated

```
const int MAX_SIZE = 50;
double myArray[MAX_SIZE];
```

the compiler reserves a specific number—MAX_SIZE, in this case—of memory cells for the array. This memory allocation occurs before your program executes, so it is not possible to wait until execution to give MAX_SIZE a value. We have already discussed the problem this fixed-size data structure causes when your program has MAX_SIZE items to place into the array.