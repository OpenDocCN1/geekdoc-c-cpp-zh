
```cpp
int main() {
    Base* pBase = new Derived();
    pBase->print(); // calls Base::print
    delete pBase;
    return 0;
}
```

output:
Base class print()

If this result troubles you, then your instincts are correct, because it serves no useful purpose to be "locked" into the base class world, even though the base class pointer can legitimately point to a variety of derived class objects.

This is especially troubling if you consider any kind of container object, such as an array, linked list, queue, stack, tree, etc. that might hold base class pointers as its data.

For example, suppose we are running a used car lot and we have declared a base class Vehicle and derived multiple classes from the Vehicle class (Lexus, Ford, BMW). So we've also created an array of Base class pointers, i.e., pointers to Vehicle objects, and have initialized each base class pointer to point to a dynamically created derived object (Lexus, Ford, BMW). So our inventory consists of a collection of "pointers" to the various cars on our lot. Someone then asks us to provide an inventory of all the cars present. So we then proceed to scan the collection of pointers and send some kind of identify yourself message to each car, rightfully expecting that each car will identify itself in some unique fashion. Unfortunately, as things now stand, the only type of response that we'll get back from all cars is, in effect, I AM A VEHICLE. The message gets sent to the base class identify() function and never reaches the identify() functions in the derived classes. Not very useful!

How we are going to free ourselves from this situation is the topic of polymorphism and virtual functions.

# Container Relationships & Inheritance Homework

1. Create two classes, A and B, with default constructors that announce themselves. Inherit a new class called C from A, and create a member object of B in C, but do not create a constructor for C. In main(), create an object of class C and explain the results.

2. Create a three-level hierarchy of classes with default constructors, along with destructors, both of which announce themselves to cout. Verify that for an object of the most derived type, all three constructors and destructors are automatically called. Explain the order in which the calls are made.

3. As part of a military video game, a designer has created a vehicle class hierarchy. The base class is Vehicle, and it has AirVehicle, LandVehicle, and SeaVehicle as derived classes. The class SeaPlane inherits from both AirVehicle and SeaVehicle. Specifically, what design issues had to be considered in developing the SeaPlane class?

4. Without executing the code below, give the output for the program.

```cpp
class A {
protected:
    int fa;
public:
    A(int va = 0) : fa(va) {
        cout << "A constructor" << endl;
    }
    A(const A& va) : fa(va.fa) {
        cout << "A copy constructor " << endl;
    }
    ~A() {
        cout << "A destructor" << endl;
    }
    A& operator=(const A& va) {
        cout << "A operator" << endl;
        fa = va.fa;
        return *this;
    }
};
```

```cpp
class B : public A {
  protected:
    int fb;
  public:
    B(int va = 0, int vb = 0) : fb(vb), A(va) {
      cout << "B constructor " << endl;
    }
    B(const B& vb) : fb(vb.fb), A(vb) {
      cout << "B copy constructor " << endl;
    }
    ~B() {
      cout << "B destructor" << endl;
    }
    B& operator=(const B& vb) {
      cout << "B operator" << endl;
      A::operator=(vb.fb);
      return *this;
    }
};

int main() {
  B b1(1, 2);
  B b2;
  b2 = b1;
  B b3(b1);
}
```

# Inheritance Lab (String Class)

One of the most popular classes to define in C++ is the one that emulates a string literal in C. The reason is that a string is not a built-in type in C, and yet it is used all the time. Thus, to perform the various manipulations on strings, you must call upon functions in the library string.h that perform operations such as copy, duplicate, compare, etc. In C++, this need is obviated by the use of function and operator overloading. In order to represent the state of a String object, you will use two data members:

- the length, length, of the string as an int
- a pointer, buf, to the string literal of type char*

A pointer to a character (char*) is used instead of a fixed-length character array so that memory can be allocated at run-time (via the operator new) and, therefore, there are no restrictions placed upon the length of the string (too big or too small). The length field is not strictly mandatory since it can always be obtained from the string pointer via the strlen() function. However, it's probably a good idea to have avoid repeated calls to strlen().

# Overloaded Constructor Functions

The creation of each String instance involves allocation of space on the heap, copying the string literal, and setting the length data member accordingly. Because there are many different ways in which a String object can be initialized, the constructor for the String class must be overloaded to accommodate all the situations.

First, if a String object is created with no initialization, then the default constructor (the one called with no arguments) will be called. It makes sense that the invoking instance point to an empty string whose length is zero.

```cpp
String();
```

Second, because there is such close relationship between a string literal (char*) and the String class, it should be easy to create a String object based upon that literal. In this case a separate copy of the literal must be made so that it can be encapsulated as part of the class.

```cpp
String(const char*);
```

Third, it might be useful to create a String object from a character.

```cpp
String(char);
```

Fourth, here is a constructor that creates a String object from an int. This implies allocating int bytes from the heap, and setting the first byte to NULL. Note that a value less than zero should be interpreted as zero.

```cpp
String(int);
```

Recall from our discussion on copy constructors that the compiler automatically supplies one if you fail to write one. This is fine if a class contains no pointer members, but will cause a big problem if at least one pointer member is present. The reason for this is that two or more pointer members may point to the same space on the heap, and, as a result, the pointer would then be pointing to the same space on the heap. Therefore, it is now necessary to create one for the String class.

```cpp
String(const String&);
```

Finally, it might be useful to create and initialize a String object with a character number of times.

```cpp
String(char, int);
```

# Destructor Function

When the String object goes out of scope, the destructor function must release the space on the heap. Otherwise, we will have a severe case of "memory leakage".

```cpp
~String();
```

# Assigning One String Instance To Another String Instance

Another function that we need in the String class is one that can assign one String instance to another instance (every C programmers dream!). In order to do this successfully, you must overload the assignment operator for the data members. Why is this necessary since the compiler automatically supplies a default assignment operator that is used to copy all of the data members? For much the reason that we had to write an explicit copy constructor, i.e., without one the address in the pointer would get copied into the corresponding pointer data member of the receiving instance and, as a result, the pointer would then be pointing to the same space on the heap. This could cause trouble when the destructor function attempts to release this space. Therefore, the default assignment operator that the compiler supplies in this situation obviously is not good enough and needs to be overloaded. Remember, this must be done as a binary member function.

```cpp
String& operator=(const String&);
```

# Implicit Type Conversion

In addition to assigning one String instance to another String instance, it makes sense to have the capability to assign a string literal (char*) to a String instance.
