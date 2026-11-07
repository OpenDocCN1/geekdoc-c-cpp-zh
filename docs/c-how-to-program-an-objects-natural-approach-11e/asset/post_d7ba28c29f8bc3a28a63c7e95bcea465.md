
```cpp
15    private:
16       std::string m_firstName; // composition: member object
17       std::string m_lastName; // composition: member object
18       Date m_birthDate; // composition: member object
19       Date m_hireDate; // composition: member object
20    };
```

**Fig. 9.25** | Employee class definition showing composition. (Part 2 of 2.)

```cpp
1    // Fig. 9.26: Employee.cpp
2    // Employee class member-function definitions.
3    #include <format>
4    #include <iostream>
5    #include "Employee.h" // Employee class definition
6    using namespace std;
7
8    // constructor uses member initializer list to pass initializer
9    // values to constructors of member objects
10   Employee::Employee(std::string_view firstName, std::string_view lastName,
11      const Date &birthDate, const Date &hireDate)
12      : m_firstName{firstName}, m_lastName{lastName},
13        m_birthDate{birthDate}, m_hireDate{hireDate} {
14      // output Employee object to show when constructor is called
15      std::cout << std::format("Employee object constructor: {} {}\n",
16         m_firstName, m_lastName);
17   }
18
19   // gets string representation of an Employee object
20   std::string Employee::toString() const {
21      return std::format("{}, {} Hired: {} Birthday: {}", m_lastName,
22         m_firstName, m_hireDate.toString(), m_birthDate.toString());
23   }
24
25   // output Employee object to show when destructor is called
26   Employee::~Employee() {
27      cout << std::format("Employee object destructor: {}, {}\n",
28         m_lastName, m_firstName);
29   }
```

**Fig. 9.26** | Employee class member-function definitions.

### Employee Constructor's Member-Initializer List

The Employee constructor's prototype (Fig. 9.25, lines 11–12) specifies that the constructor has four parameters (firstName, lastName, birthDate and hireDate). In the constructor's definition (Fig. 9.26, lines 12–13), the first two parameters are passed via member initializers to the string constructor for data members firstName and lastName. The last two are passed via member initializers to class Date's constructor for data members birthDate and hireDate. The data members are constructed in the order that they're declared in class Employee, not in the order they appear in the member-initializer list. Again, for clarity, the C++ Core Guidelines recommend listing the member initializers in the order they're declared in the class.<sup>33</sup>

### Date Class’s Default Copy Constructor

As you study class Date (Fig. 9.23), notice it does not provide a constructor with a Date parameter. So, why can the Employee constructor’s member-initializer brace initialize the `m_birthDate` and `m_hireDate` objects by passing Date objects to their constructors? As mentioned in Section 9.15, the compiler provides each class with a default copy constructor that copies each data member of the constructor’s argument into the corresponding member of the object being initialized. Chapter 11 discusses how to define customized copy constructors.

### Testing Classes Date and Employee

Figure 9.27 creates two Date objects (lines 9–10), then passes them as arguments to the constructor of the Employee object created in line 11. When an Employee is created, its constructor makes

- two calls to the string class’s constructor (line 12 of Fig. 9.26) and
- two calls to the Date class’s default copy constructor (line 13 of Fig. 9.26).

Line 13 of Fig. 9.27 displays the Employee’s data to show that it was initialized correctly.

```cpp
// Fig. 9.27.cpp
// Demonstrating composition—an object with member objects.
#include <format>
#include <iostream>
#include "Date.h" // Date class definition
#include "Employee.h" // Employee class definition

int main() {
  const Date birth{1987, 7, 24};
  const Date hire{2018, 3, 12};
  const Employee manager{"Aisha", "Khan", birth, hire};

  std::cout << std::format("{:}\n\n", manager.toString());
}
```

```text
Date object constructor: 1987-07-24
Date object constructor: 2018-03-12
Employee object constructor: Aisha Khan

Khan, Aisha  Hired: 2018-03-12  Birthday: 1987-07-24

Employee object destructor: Khan, Aisha
Date object destructor: 2018-03-12
Date object destructor: 1987-07-24
Date object destructor: 2018-03-12
Date object destructor: 1987-07-24
```

**Fig. 9.27** | Demonstrating composition—an object with member objects.

33. C++ Core Guidelines, “C.47: Define and Initialize Member Variables in the Order of Member Declaration.” Accessed April 14, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-order.

When each Date object is created in lines 9–10, the Date constructor (lines 11–24 of Fig. 9.24) displays a line of output to show that the constructor was called (see the first two lines of the sample output). However, line 11 of Fig. 9.27 causes two Date copy-constructor calls (line 13 of Fig. 9.26) that do not appear in this program’s output. Since the compiler can define a class’s copy constructor, it does not contain any output statements to demonstrate when it’s called.

Class Date and class Employee each include a destructor (lines 32–34 of Fig. 9.24 and lines 26–29 of Fig. 9.26, respectively) that prints a message when an object of its class is destructed. The destructors help us show that objects are destructed from the outside in. The Date member objects are destructed after the enclosing Employee object.

Notice the last four lines in the output of Fig. 9.27. The last two lines are the outputs of the Date destructor running on Date objects hire (Fig. 9.27, line 10) and birth (line 9), respectively. The outputs confirm that the three objects created in main are destructed in the reverse order of their construction. The Employee destructor output is five lines from the bottom. The fourth and third lines from the bottom show the destructors running for the Employee’s member objects m_hireDate (Fig. 9.25, line 19) and m_birthDate (line 18).

These outputs confirm that the Employee object is destructed from the outside in. The Employee destructor runs first (see the output five lines from the bottom). Then the member objects are destructed in the reverse order from which they were constructed. Class string’s destructor does not contain output statements, so we do not see the firstName and lastName objects being destructed.

### What Happens When You Do Not Use the Member-Initializer List?

If you do not initialize a member object explicitly, its default constructor will be called implicitly to initialize it. If there is no default constructor, a compilation error occurs. Values set by the default constructor can be changed later—for example, by set functions. However, this approach may require significant additional work and time for complex initialization. Initializing member objects via member initializers eliminates the overhead of “doubly initializing” member objects.

### Checkpoint

- **1. (True/False)** A class’s constructor can pass arguments to member-object constructors via member initializers.  
  **Answer:** True.
- **2. (True/False)** Data members are constructed in the order they appear in the member-initializer list.  
  **Answer:** False. Actually, the order of the member initializers does not matter. Data members are constructed in the order that they’re declared in the class, not in the order they appear in the member-initializer list. For clarity, the C++ Core Guidelines recommend listing the member initializers in the order they’re declared in the class.
- **3. (True/False)** Objects are generally destructed from the outside in.  
  **Answer:** True.

## 9.18 friend Functions and friend Classes

A friend function has access to a class’s public and non-public members. A class may have as friends

- stand-alone functions,
- entire classes (and thus all their functions) or
- specific member functions of other classes.

This section presents a mechanical example of how a friend function works. In Chapter 11, Operator Overloading, Copy/Move Semantics and Smart Pointers, we’ll show friend functions that overload operators for use with objects of custom classes. You’ll see that sometimes a member function cannot be used to define certain overloaded operators.

### Declaring a friend

To declare a non-member function as a friend of a class, place the function prototype in the class definition and precede it with the keyword friend. To declare all member functions of an existing class ClassTwo as friends of class ClassOne, place in ClassOne’s definition a declaration of the form:

```cpp
friend class ClassTwo;
```

### Friendship Rules

These are the basic friendship rules:

- **Friendship is granted, not taken**—For class B to be a friend of class A, class A must declare that class B is its friend.
- **Friendship is not symmetric**—If class A is a friend of class B, you cannot infer that class B is a friend of class A.
- **Friendship is not transitive**—If class A is a friend of class B and class B is a friend of class C, you cannot infer that class A is a friend of class C.

### friends Are Not Subject to Access Modifiers

Member access notions of `public`, `protected` (Chapter 10) and `private` do not apply to friend declarations, so friend declarations can be placed anywhere in a class definition. We prefer to place friend declarations first inside the class definition’s body and not precede them with any access specifier.

### Modifying a Class’s private Data with a friend Function

Figure 9.28 defines the free function modifyX as a friend of class Count (line 8), so modifyX can set Count’s private data member m_x.

```cpp
// fig09_28.cpp
// Friends can access private members of a class.
#include <format>
#include <iostream>
```

**Fig. 9.28** | Friends can access private members of a class. (Part 1 of 2.)
