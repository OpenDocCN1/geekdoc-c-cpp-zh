
- A static member function can have access to the static members declared in the same class and can be called using the class name.
- C++ allows us to have arrays of objects.
- We may use objects as function arguments.
- A function declared as a **friend** is not in the scope of the class to which it has been declared as friend. It has full access to the private members of the class.
- A function can also return an object.
- If a member function does not alter any data in the class, then we may declare it as a **const** member function. The keyword **const** is appended to the function prototype.
- It is also possible to define and use a class inside a function. Such a class is called a local class.

## Key Terms

abstract data type | arrays of objects | **class** | class declaration | class members | class variables | **const** member functions | data hiding | data members | dereferencing operator | dot operator | elements | encapsulation | **friend** functions | inheritance | **inline** functions | local class | member functions | Nesting of member functions | objects | pass-by-reference | pass-by-value | period operator | **private** | prototype | **public** | scope operator | scope resolution | static data members | static member functions | static variables | **struct** | structure | structure members | structure name | structure tag | template

## Review Questions

- 5.1 How do structures in C and C++ differ?
- 5.2 What is a class? How does it accomplish data hiding?
- 5.3 How does a C++ structure differ from a C++ class?
- 5.4 What are objects? How are they created?
- 5.5 How is a member function of a class defined?
- 5.6 Can we use the same function name for a member function of a class and an outside function in the same program file? If yes, how are they distinguished? If no, give reasons.
- 5.7 Describe the mechanism of accessing data members and member functions in the following cases:
  - (a) Inside the main program.
  - (b) Inside a member function of the same class.
  - (c) Inside a member function of another class.
- 5.8 When do we declare a member of a class static?
- 5.9 What is a friend function? What are the merits and demerits of using friend functions?
- 5.10 Can we pass class objects as function arguments? Explain with the help of an example.
- 5.11 State whether the following statements are TRUE or FALSE.
  - (a) Data items in a class must always be private.
  - (b) A function designed as private is accessible only to member functions of that class.
  - (c) A function designed as public can be accessed like any other ordinary functions.
  - (d) Member functions defined inside a class specifier become inline functions by default.
  - (e) Classes can bring together all aspects of an entity in one place.
  - (f) Class members are public by default.
  - (g) Friend functions have access to only public members of a class.
  - (h) An entire class can be made a friend of another class.
  - (i) Functions cannot return class objects.
  - (j) Data members can be initialized inside class specifier.

## Debugging Exercises

### 5.1 Identify the error in the following program.

```cpp
#include <iostream.h>
struct Room
{
    int width;
    int length;
    void setValue(int w, int l)
    {
        width = w;
        length = l;
    }
};
void main()
{
    Room objRoom;
    objRoom.setValue(12, 1,4);
}
```

### 5.2 Identify the error in the following program.

```cpp
#include <iostream.h>
class Room
{
int width, height;
void setValue(int w, int h)
{
width = w;
height = h;
}
};
void main()
{
Room objRoom;
objRoom.width = 12;
}
```

### 5.3 Identify the error in the following program.

```cpp
#include <iostream.h>
class Item
{
private:
static int count;
public:
Item()
{
count++;
}
int getCount()
{
return count;
}
int* getCountAddress()
{
return count;
}
};
int Item::count = 0;
void main()
{
 Item objItem1;
 Item objItem2;
 cout << objItem1.getCount() << ' ';
 cout << objItem2.getCount() << ' ';
 cout << objItem1.getCountAddress() << ' ';
 cout << objItem2.getCountAddress() << ' ';
}
```

### 5.4 Identify the error in the following program.

```cpp
#include <iostream.h>
class staticFunction
{
 static int count;
 public:
 static void setCount()
 {
  count++;
 }
 void displayCount ()
 {
  cout << count;
 }
};
int staticFunction::count = 10;
void main()
{
 staticFunction obj1;
 obj1.setCount(5);
 staticFunction::setCount();
 obj1.displayCount();
}
```

### 5.5 Identify the error in the following program.

```cpp
#include <iostream.h>
class Length
{
int feet;
float inches;
public:
Length()
{
feet = 5;
inches = 6.0;
}
Length(int f, float in)
{
feet = f;
inches = in;
}
Length addLength(Length l)
{
l.inches += this->inches;
l.feet += this->feet;
if(l.inches>12)
{
l.inches -= 12;
l.feet++;
}
return l;
}
int getFeet ()
{
return feet;
}
float getInches()
{
return inches;
}
};
void main()
{
    Length objLength1;
    Length objLength1(5, 6.5);
    objLength1 = objLength1.addLength(objLength2);
    cout << objLength1.getFeet() << ' ';
    cout << objLength1.getInches() << ' ';
}
```

### 5.6 Identify the error in the following program.

```cpp
#include <iostream.h>
class Room;
void Area()
{
    int width, height;
    class Room
    {
        int width, height;
    public:
        void setValue(int w, int h)
        {
            width = w;
            height = h;
        }
        void displayValues()
        {
            cout << (float)width << " " << (float)height;
        }
    };
    Room objRoom1;
    objRoom1.setValue(12, 8);
    objRoom1.displayValues();
}
void main()
{
    Area();
    Room objRoom2;
}
```

## Programming Exercises

**5.1** Define a class to represent a bank account. Include the following members:

**Data members**

- 1. Name of the depositor
- 2. Account number
- 3. Type of account
- 4. Balance amount in the account

**Member functions**

- 1. To assign initial values
- 2. To deposit an amount
- 3. To withdraw an amount after checking the balance
- 4. To display name and balance

Write a main program to test the program.

**5.2** Write a class to represent a vector (a series of float values). Include member functions to perform the following tasks:

- (a) To create the vector
- (b) To modify the value of a given element
- (c) To multiply by a scalar value
- (d) To display the vector in the form (10,20, 30, ...)

Write a program to test your class.

- 5.3 Modify the class and the program of Exercise 5.1 for handling 10 customers. . WEB

- 5.4 Modify the class and program of Exercise 5.2 such that the program would be able to add two vectors and display the resultant vector. (Note that we can pass objects as function arguments.)

- 5.5 Create two classes DM and DB which store the value of distances. DM stores distances in metres and centimetres and DB in feet and inches. Write a program that can read values for the class objects and add one object of DM with another object of DB. . WEB

Use a friend function to carry out the addition operation. The object that stores the results may be a DM object or DB object, depending on the units in which the results are required.

The display should be in the format of feet and inches or metres and centimetres depending on the object on display.

- 5.6 Refer Program 5.11 and write a function that receives two matrix objects as arguments and returns a new matrix object containing their multiplication result. . WEB

## Constructors and Destructors

### Key Concepts

Constructing objects | Constructors | Constructor overloading | Default argument constructor | Copy constructor | Constructing matrix objects | Automatic initialization | Parameterized constructors | Default constructor | Dynamic initialization | Dynamic constructor | Destructors

### 6.1 Introduction

We have seen, so far, a few examples of classes being implemented. In all the cases, we have used member functions such as **putdata()** and **setvalue()** to provide initial values to the private member variables. For example, the following statement

```cpp
A.input();
```

invokes the member function **input()**, which assigns the initial values to the data items of object **A**. Similarly, the statement

```cpp
x.getdata(100, 2.9, 9.95);
```

passes the initial values as arguments to the function **getdata()**, where these values are assigned to the private variables of object **x**. All these ‘function call’ statements are used with the appropriate objects that have already been created. These functions cannot be used to initialize the member variables at the time of creation of their objects.

Providing the initial values as described above does not conform with the philosophy of C++ language. We stated earlier that one of the aims of C++ is to create user-defined data types such as **class**, that behave very similar to the built-in types. This means that we should be able to initialize a **class** type variable (object) when it is
