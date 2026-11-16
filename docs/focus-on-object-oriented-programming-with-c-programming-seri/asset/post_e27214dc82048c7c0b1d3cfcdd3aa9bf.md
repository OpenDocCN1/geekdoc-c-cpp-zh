
- Another reason for not modifying the Counter class is that we might not have access to its source code, especially if it has been distributed as part of a class library.

To avoid these problems, we can use inheritance to create a new class based on Counter, without modifying Counter itself. We can derive a new class, CountDn, which adds a decrement operator to the Counter class:

```
class Counter {
 protected:
 int count;
 public:
 Counter() { count = 0; }
 Counter(int c) { count = c; }
 int getCount() { return count; }
 Counter operator++() {
 ++count;
 return *this;
 }
 };

class CountDn : public Counter {
 public:
 CountDn operator--() {
 --count;
 return *this;
 }
 };
```

Here's a breakdown of the syntax:

- The private access specifier in the Counter class has been replaced with the protected access specifier. More on this later.
- CountDn is the derived class name
- : specifies that CountDn is derived from Counter
- public refers to the type of inheritance which may be public, private, or protected. We'll look at this at a later time.
- Counter is the name of the base class

```
int main() {
  CountDn c;
  ++c;
  ++c;
  cout << c.getCount() << endl;
  --c;
  cout << c.getCount() << endl;
  return 0;
}
```

The output produced is:

2
1

Note that the new CountDn class inherits all the features of the Counter class. CountDn doesn't need a constructor, it doesn't need the getCount() function, and it doesn't need the operator++() function because they already exist in the base class Counter. Keep in mind that the public members of a public base class remain public in the derived class.

## Accessing Base Class Members

An important part to inheritance is knowing when a member function in the base class can be used by objects of the derived class. This is called accessibility. For example, in main(), we created an object of class CountDn:

```
CountDn c;
```

which caused c to be created as an object of class CountDn and initialized to 0. But wait! How is this possible? There is no constructor in the CountDn class specifier. So what entity carries out the initialization?

It turns out that under certain circumstances, if you don't specify a constructor, the derived class will use an appropriate constructor from the base class. Here, there's no constructor in CountDn, so the compiler uses the default constructor from the base class, Counter.

Note that object c of the CountDn class also uses the operator++() and getCount() member functions from the Counter class. If the compiler doesn't find these functions in the class of which c is a member, it uses member functions from the base class.

## Derived Class Constructors

There's a potential glitch in our program. What if we want to initialize a CountDn object to a value? Can the one-arg constructor in Counter be used? No it cannot!

Although the compiler will substitute a default constructor from the base class, it draws the line at more complex constructors. Therefore we must write a new set of constructors for the derived class:

```
class CountDn : public Counter {
public:
CountDn() : Counter() {}
CountDn(int c) : Counter(c) {}
CountDn operator--() {
--count;
return *this;
}
};

int main() {
CountDn c1, c2(100);
return 0;
}
```

Here,

```
CountDn() : Counter() {}
```

causes the CountDn default constructor to call the Counter default constructor in the base class and

```
CountDn(int c) : Counter(c)
```

causes the CountDn one-arg constructor to call the Counter one-arg constructor in the base class.

Note that the CountDn constructor could add additional statements of its own, but in this case it doesn't need to so the braces are empty. But if it defined a new data member, it could initialize it here and then call the base class constructor to initialize the rest of the object. More on this later.

## Protected Access Specifier

- Member functions of a class can access both private and public members.
- Objects of a class can access only public members.
- Private members are private.

This is all we need to know if we don't use inheritance. With inheritance, there are new possibilities. The question that concerns us at the moment is this:

Can member functions of the derived class access data members of the base class? For example, can `operator--()` in `CountDn` access `count` in `Counter`?

The answer is that member functions can access members of the base class if the members are `public` or `protected`. They can't access `private` members.

We don't want to make `count` `public` since that would allow it to be accessed by any function anywhere in the program and eliminate the advantages of data-hiding. A `protected` member, on the other hand, can be accessed by member functions in its own class, or in any class derived from its own class. It can't be accessed from functions outside the class, such as `main()` which is just what we want!

So a `protected` class member is a cross between a `private` and a `public` member.

- Like `private` members, `protected` members are accessible only to other class member functions. Outside of the class, `protected` members are invisible.
- Like `public` members, `protected` members are inherited by the derived class and are accessible to member functions in the derived class.

Keep the following rules in mind when deciding whether to make members `private`, `protected`, or `public`:

- A `private` member is accessible only to members of the class in which the `private` member is declared.
- A `protected` member is accessible to members of its own class and to any members in a derived class.
- A `public` member is accessible to the class's own members, to a derived class's members, and to all other users of the class.

| Access Specifier | Accessible From Own Class | Accessible From Derived Class | Accessible From Objects Outside Class |
|---|---|---|---|
| private | yes | no | no |
| protected | yes | yes | no |
| public | yes | yes | yes |

The moral is that if you are writing a class that you suspect might be used, at any point in the future, as a base class for other classes, then any data that the derived class might need to access should be made `protected` rather than `private`. This ensures that the class is "inheritance ready", to adapt a phrase from TV set advertising.

Note that inheritance doesn't work in reverse. The base class and its objects don't know anything about any classes derived from the base class. For instance, in the declaration:

```
Counter c;
```

object `c` cannot use the `operator--()` function defined in `CountDn`. If you want a counter that you can decrement, it must be of class `CountDn` and not class `Counter`.

## Employee Class

Consider the Employee base class below:

```
// employee.h

#ifndef _EMPLOYEE_H
#define _EMPLOYEE_H

using namespace std;

class Employee {
  protected:
    char *name;
    char *address;
    int age;
    int dependent;
    int jobClass;

  public:
    Employee(char *, char *, int, int, int);
    ~Employee();
    void display();

    int getAge() { return age;}
    int getDependent() { return dependent;}
    int getJobClass() { return jobClass;}
};

#endif

// employee.cpp

#include <iostream>
#include <string.h>
#include "employee.h"

Employee::Employee(char *nm, char *ad, int ag, int dp, int jc) {
  name = new char[strlen(nm)+1];
  strcpy(name, nm);
  address = new char[strlen(ad)+1];
  strcpy(address, ad);
  age = ag;
  dependent = dp;
  jobClass = jc;
}

Employee::~Employee() {
  delete [] name;
  delete [] address;
}
```

```
void Employee::display() {
    cout << name << endl;
    cout << address << endl;
}
```

The base class Employee is set up like any other class. However, because we intend that this class have a class derived from it, we put the data members in the protected access region because we want the derived class member functions to have direct access to these data. Note that this class has a constructor, a destructor, output functions, and three access functions.

Occasionally very little is done with a base class. We may not even declare any objects of a base class because a base class object is not required to declare a derived object. Base classes can be created to provide data members and member functions that will be shared by a variety of different derived class definitions. The derived class looks like this:

```
// workdata.h

#ifndef WORKDATA_H
#define WORKDATA_H

#include "employee.h"

class Workdata : public Employee {
    private:
        char *occupation;
    public:
        Workdata(char *, char *, char *, int, int, int);
        ~Workdata() { delete [] occupation; }
        char * getOccupation() { return occupation; }
        void display();
        int getAge() { return age; }
};

#endif
```
