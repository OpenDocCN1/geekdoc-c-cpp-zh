
## Calling a virtual method

A base class pointer that is bound to a specific derived class can be used to call derived class methods that have been inherited from the base class. Methods that are unique to the derived class must, however, be called via an instance object.

A base class pointer that is bound to a specific derived class can also be used to explicitly call a method in the base class using the :: scope resolution operator.

Most usefully, an inherited method in a derived class can override that in the base class when the base method has been declared as a “virtual” method. This is just a regular method declaration in the base class preceded by the **virtual** keyword. The declaration of a virtual method indicates that the class will be used as a base class from which another class will be derived, which may contain a method to override the virtual base method.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_135_0.png)

### virtual.cpp

- 1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use.

```cpp
#include <iostream>
using namespace std;
```

- 2. Declare a base class named “Parent”, containing a regular method declaration and a virtual method declaration.

```cpp
class Parent
{
    public:
        void Common() const
        { cout << "I am part of this family, "; }

        virtual void Identify() const
        { cout << "I am the parent" << endl; }
};
```

- 3. Declare a derived class named “Child”, containing a method to override the virtual base method.

```cpp
class Child : public Parent
{
    public:
        void Identify() const
        { cout << "I am the child" << endl; }
};
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_135_1.png)

Pointers to a base class cannot be used to call non-inherited methods in a derived class.

- 4. Declare a “Grandchild” class, derived from the “Child” class, containing a method to override the virtual base method and a regular method declaration.

```cpp
class Grandchild : public Child
{
    public:
        void Identify() const
        { cout << "I am the grandchild" << endl; }

        void Relate() const
        { cout << "Grandchild has parent and grandparent"; }
};
```

## Directing method calls

The great advantage of polymorphism with multiple derived class objects is that calls to methods of the same name are directed to the appropriate overriding method.

A base class may contain only virtual methods which each derived class may override with their own methods, but base class methods can still be called explicitly using the :: scope resolution operator. This can allow inconsistencies, however – this example would seem to imply that chickens can fly!

![](img/bf8dbdfb89042fadbaa73b4160c74bac_137_0.png)

### birds.cpp

- 1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use

```cpp
#include <iostream>
using namespace std;
```

- 2. Declare a base class named “Bird”, containing two virtual method declarations

```cpp
class Bird
{
public:
    virtual void Talk() const
    { cout << "A bird talks..." << endl; }

    virtual void Fly() const
    { cout << "A bird flies..." << endl; }
};
```

- 3. Declare a derived class named “Pigeon”, containing two methods to override those in the base class

```cpp
class Pigeon : public Bird
{
public:
    void Talk() const
    { cout << "Cool! Cool!" << endl; }

    void Fly() const
    { cout << "A pigeon flies away..." << endl; }
};
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_137_1.png)

Overriding methods in derived class may, optionally, include the virtual prefix – as a reminder it is overriding a base class method.

- 4. Declare a derived class named “Chicken”, containing two methods to override those in the base class

```cpp
class Chicken : public Bird
{
public:
    void Talk() const
    { cout << "Cluck! Cluck!" << endl; }

    void Fly() const
    { cout << "I\'m just a chicken – I can\'t fly!" << endl; }
};
```

- 5. Declare a main method containing a final **return** statement and creating base class pointers binding derived classes

```cpp
int main()
{
    Bird* pPigeon = new Pigeon;
    Bird* pChicken = new Chicken;
    // Add more statements here.
    return 0;
}
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_138_0.png)

- 6. In the main method, insert calls to each method

```cpp
pPigeon->Talk();
pPigeon->Fly();
pChicken->Talk();
pChicken->Fly();
pPigeon->Bird::Talk();
pChicken->Bird::Fly();    // Inappropriate call.
```

- 7. Save, compile, and run the program to see the output

![](img/bf8dbdfb89042fadbaa73b4160c74bac_138_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_138_2.png)

The backslash \ character is required to escape the apostrophe in strings.

## Providing capability classes

Classes whose sole purpose is to allow other classes to be derived from them are known as “capability classes” – they provide capabilities to the derived classes.

Capability classes generally contain no data, but merely declare a number of virtual methods that can be overridden in their derived classes.

The following example builds upon the previous example to demonstrate how the “Bird” class can be better written as a capability class. Its methods no longer contain output statements, but return a -1 (error) value if they are called explicitly.

It is necessary to change the return type of those methods from void to int and these changes must also be reflected in each overriding method in the derived classes.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_139_0.png)

### capability.cpp

- 1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use

```cpp
#include <iostream>
using namespace std;
```

- 2. Declare a base capability class named “Bird”, containing two virtual method declarations that will signal an error if called explicitly

```cpp
class Bird
{
  public:
    virtual int Talk() const { return -1; }
    virtual int Fly() const { return -1; }
};
```

- 3. Declare a derived class named “Pigeon”, containing two methods to override those in the base class

```cpp
class Pigeon : public Bird
{
  public:
    int Talk() const
    { cout << "Coo! Coo!" << endl; return 0; }

    int Fly() const
    { cout << "A pigeon flies away..." << endl; return 0; }
};
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_139_1.png)

The return value of overriding methods in derived classes must match those declared in the base class.

- 4. Declare a derived class named “Chicken” containing two methods to override those in the base class

```cpp
class Chicken : public Bird
{
  public:
    int Talk() const
    { cout << "Cluck! Cluck!" << endl; return 0; }

    int Fly() const
    { cout << "I\'m just a chicken – I can\'t fly!" << endl; return 0; }
};
```

- 5. Declare a main method creating base class pointers binding the derived classes

```cpp
int main()
{
    Bird* pPigeon = new Pigeon;
    Bird* pChicken = new Chicken;
```

- 6. In the main method, insert method calls and a statement to terminate the program when an error is met by explicitly calling a base class method

```cpp
pPigeon->Talk();
pChicken->Talk();

pPigeon->Bird::Talk();
if (-1) { cout << "Error! - Program ended."
                         << endl; return 0; }

pPigeon->Fly();       // Call will not be made.
pChicken->Fly();      // Call will not be made.
return 0;              // Statement will not be executed
}
```

- 7. Save, compile, and run the program to see the output

![](img/bf8dbdfb89042fadbaa73b4160c74bac_140_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_140_1.png)

Capability class methods are intended to be overridden in derived classes — they should not be called explicitly.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_140_2.png)

Refer back to here for more details on error handling.
