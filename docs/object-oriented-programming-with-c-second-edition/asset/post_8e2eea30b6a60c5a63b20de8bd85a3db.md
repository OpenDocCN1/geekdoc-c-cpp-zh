
```cpp
void A::setx(const int p)
{
    x=p;
}
```

```cpp
int A::getx() const
{
    return x;
}
```

```cpp
/*End of A.cpp*/
/*Beginning of B.h*/
#include "B.h"
```

```cpp
class B : public A
{
    int y;
public:
    B(const int q=0);
    void sety(const int q=0);
    int gety(const int);
};
```

```cpp
/*Beginning of B.cpp*/
#include "B.h"
```

```cpp
B::B(const int q)
{
    y=q;
}
```

```cpp
void B::sety(const int q)
{
    y=q;
}
```

```cpp
int B::gety() const
{
    return y;
}
```

```cpp
/*End of B.cpp*/
```

```cpp
/*Beginning of baseinit1.cpp*/
#include "B.h"
#include <iostream.h>
```

```cpp
void main()
{
    B B1(20);
    cout << B1.getx() << endl
         << B1.gety() << endl;
}
```

```cpp
/*End of baseinit1.cpp*/
```

# Output

0
20

The output is explained by the simple observation that the statement B1(20);

Inheritance 131

gets converted to the following:

B1; //memory allocated for the object
B1.A(); //base class constructor called
B1.B(20); //derived class constructor called

As we can see, base class data members of the derived class object get initialized through the base class constructor with the default value being passed to it. Thus, 'B1.y' get initialized to 20 (the value passed). But 'B1.x' get initialized to 0 (the default value). While creating an object of the derived class, we would like to pass a value explicitly to the base constructor. Thus, in Listing 5.15, the constructor of class B should take not one but two parameters. One of these should be passed to 'y' while the other should be used to initialize 'x'. For this, the prototype and definition of the constructor of class B should be modified as shown in Listing 5.16.

## Listing 5.16 Modifying the derived class constructor to ensure successful initialization of the base class members

```cpp
/*Beginning of B.h*/
#include "A.h"
class B : public A
{
public:
    B(const int p=0, const int q=0);
    /*
    rest of the class B
    */
};
/*End of B.h*/

/*Beginning of B.cpp*/
#include "B.h"
B::B(const int p, const int q) : A(p) //passing value to base
//class constructor
{
    y=q;
}
/*
    Definitions of the remaining member functions of class B
*/
/*End of B.cpp*/
```

An object of class B can be declared by passing two parameters to its constructor. One of them is assigned to 'x'. The other is assigned to 'y'.

## Listing 5.17 Base class initialization

```cpp
/*Beginning of baseinit02.cpp*/
#include <iostream.h>
void main()
{
    B B1(10,20);
    cout << B1.getx() << endl << B1.gety() << endl;
```

# Object-Oriented Programming with C++

```cpp
}
/*End of baseinit02.cpp*/
```

# Output
10
20

Again, the output of Listing 5.17 can be explained by noting that due to the modified definition of the constructor of class B, the statement

```cpp
B B1(10,20);
```

gets converted to

```cpp
B B1;                               //memory allocated for the object
B1.A(10);                              //base class constructor called
B1.B(20);                               //derived class constructor called
```

As per the definition of the derived class constructor in Listing 5.17, the first parameter passed to it was in turn passed to the base class constructor. But this is not necessary. Any of the parameters passed to the derived class constructor can be passed to the base class constructor.

## 5.5 Protected Access Specifier

Apart from the public and private access specifiers, there is a third access modifier in C++ known as protected. Protected members are inaccessible to non-member functions. However, they are accessible to the member functions of their own class and to member functions of the derived classes. Listing 5.18 along with its accompanying comments illustrates this.

- Listing 5.18 Accessing protected members

```cpp
/*Beginning of A.h*/
class A
{
private:
int x;
protected:
int y;
public:
int z;
};
/*End of A.h*/
```

```cpp
/*Beginning of B.h*/
#include "A.h"
class B : public A                               //derived class
{
public:
void xyz();
}
/*End of B.h*/
/*Beginning of B.cpp*/
#include "B.h"
void B::xyz()                                     //member function of derived class
```

```cpp
{
  x=1; //ERROR: private member of base class
  y=2; //OK: protected member of base class
  z=3; //OK: public member of base class
}
```

```cpp
/*Beginning of protected.cpp*/
#include "A.h"
void main() {
  A * Aptr;
  Aptr->x=10; //ERROR: private member
  Aptr->y=20; //ERROR: protected member
  Aptr->z=30; //OK: public member
}
/*End of protected.cpp*/
```

## 5.6 Deriving by Different Access Specifiers

### 5.6.1 Deriving by the Public Access Specifier

Deriving by the public access specifier retains the access level of base class members.

**Private members:** Member functions of the derived class cannot access. Member functions of the subsequently derived classes cannot access them. Non-member functions cannot access them.

**Protected members:** Member functions of the derived class can access them. Member functions of the subsequently derived classes can also access them. Non-member functions cannot access them.

**Public members:** Member functions of the derived class can access them. Member functions of the subsequently derived classes can also access them. The non-member functions can also access them.

Errors are encountered when compiling Listing 5.19 make this evident.

- **Listing 5.19** Accessing the inherited members of an object of a class derived by public access specifier

```cpp
/*Beginning of publicInheritance.cpp*/
class A {
  private:
  int x;
  protected:
  int y;
  public:
  int z;
}
class B : public A //B is a public derived class of A
{
  public:
```

# 134 Object-Oriented Programming with C++

```cpp
void f1()
{
    x=1;
    y=2;
    z=2;
    //ERROR: private member remains private
    //OK: protected member remains protected
    //OK: public member remains public
}
```

```cpp
class C : public B
{
    public:
    void f2()
    {
        x=1; //ERROR: private member remains private
        y=2; //OK: protected member remains protected
        z=2; //OK: public member remains protected
    }
}
```

```cpp
void B::xyz()                                     //member function of derived class
{
  x=1; //ERROR: private member of base class
  y=2; //OK: protected member of base class
  z=3; //OK: public member of base class
}
```

```cpp
/*Beginning of protected.cpp*/
void main() {
  A * Aptr;
  Aptr->x=10; //ERROR: private member
  Aptr->y=20; //ERROR: protected member
  Aptr->z=30; //OK: public member
}
/*End of protected.cpp*/
```

- **Listing 5.21** Accessing the inherited members of an object of a class derived by protected access specifier

```cpp
/*Beginning of publicInheritance.cpp*/
class A {
  private:
  int x;
  protected:
  int y;
  public:
  int z;
};
class B : public A //B is a public derived class of A
{
  public:
void f1()
{
    x=1; //ERROR: private member remains private
    y=2; //OK: protected member remains protected
    z=2; //OK: public member remains public
}
}
class C : public B
{
    public:
    void f2()
    {
        x=1; //ERROR: private member remains private
        y=2; //OK: protected member remains protected
        z=2; //OK: public member remains protected
    }
}
```

An object of class B can be declared by passing two parameters to its constructor. One of them is assigned to 'x'. The other is assigned to 'y'.

## Listing 5.17 Base class initialization

```cpp
/*Beginning of baseinit02.cpp*/
#include <iostream.h>
void main()
{
    B B1(10,20);
    cout << B1.getx() << endl << B1.gety() << endl;
}
/*End of baseinit02.cpp*/
```

Again, the output of Listing 5.17 can be explained by noting that due to the modified definition of the constructor of class B, the statement

```cpp
B B1(10,20);
```

gets converted to

```cpp
B B1;                               //memory allocated for the object
B1.A(10);                              //base class constructor called
B1.B(20);                               //derived class constructor called
```

As per the definition of the derived class constructor in Listing 5.17, the first parameter passed to it was in turn passed to the base class constructor. But this is not necessary. Any of the parameters passed to the derived class constructor can be passed to the base class constructor.

## 5.5 Protected Access Specifier

Apart from the public and private access specifiers, there is a third access modifier in C++ known as protected. Protected members are inaccessible to non-member functions. However, they are accessible to the member functions of their own class and to member functions of the derived classes. Listing 5.18 along with its accompanying comments illustrates this.

- Listing 5.18 Accessing protected members

```cpp
/*Beginning of A.h*/
class A
{
private:
int x;
protected:
int y;
public:
int z;
};
/*End of A.h*/
```

```cpp
/*Beginning of B.h*/
#include "A.h"
class B : public A                               //derived class
{
public:
void xyz();
}
/*End of B.h*/
/*Beginning of B.cpp*/
#include "B.h"
void B::xyz()                                     //member function of derived class
```

```cpp
{
  x=1; //ERROR: private member of base class
  y=2; //OK: protected member of base class
  z=3; //OK: public member of base class
}
```

```cpp
/*Beginning of protected.cpp*/
#include "A.h"
void main() {
  A * Aptr;
  Aptr->x=10; //ERROR: private member
  Aptr->y=20; //ERROR: protected member
  Aptr->z=30; //OK: public member
}
/*End of protected.cpp*/
```

## 5.6 Deriving by Different Access Specifiers

### 5.6.1 Deriving by the Public Access Specifier

Deriving by the public access specifier retains the access level of base class members.

**Private members:** Member functions of the derived class cannot access. Member functions of the subsequently derived classes cannot access them. Non-member functions cannot access them.

**Protected members:** Member functions of the derived class can access them. Member functions of the subsequently derived classes can also access them. Non-member functions cannot access them.

**Public members:** Member functions of the derived class can access them. Member functions of the subsequently derived classes can also access them. The non-member functions can also access them.

Errors are encountered when compiling Listing 5.19 make this evident.

- **Listing 5.19** Accessing the inherited members of an object of a class derived by public access specifier

```cpp
/*Beginning of publicInheritance.cpp*/
class A {
  private:
  int x;
  protected:
  int y;
  public:
  int z;
}
class B : public A //B is a public derived class of A
{
  public:
```

# 134 Object-Oriented Programming with C++

```cpp
void f1()
{
    x=1;
    y=2;
    z=2;
    //ERROR: private member remains private
    //OK: protected member remains protected
    //OK: public member remains public
}
```

```cpp
class C : public B
{
    public:
    void f2()
    {
        x=1; //ERROR: private member remains private
        y=2; //OK: protected member remains protected
        z=2; //OK: public member remains protected
    }
}
```

## 5.6.2 Deriving by the Protected Access Specifier

Deriving by the protected access specifier reduces the access level of public base class members to protected while the access level of protected and private base class members remain unchanged.

**Private members:** Member functions of the derived class cannot access. Member functions of the subsequently derived classes cannot access them. Non-member functions cannot access them.

**Protected members:** Member functions of the derived class can access them. Member functions of the subsequently derived classes can also access them. Non-member functions cannot access them.

**Public members:** Member functions of the derived class can access them (but they are now protected in the derived class).

Errors encountered while compiling Listing 5.21 demonstrates this.

- **Listing 5.21** Accessing the inherited members of an object of a class derived by protected access specifier

```cpp
/*Beginning of publicInheritance.cpp*/
class A {
  private:
  int x;
  protected:
  int y;
  public:
  int z;
};
class B : public A //B is a public derived class of A
{
  public:
void f1()
{
    x=1; //ERROR: private member remains private
    y=2; //OK: protected member remains protected
    z=2; //OK: public member remains protected
}
}
class C : public B
{
    public:
    void f2()
    {
        x=1; //ERROR: private member remains private
        y=2; //OK: protected member remains protected
        z=2; //OK: public member remains protected
    }
}
```
