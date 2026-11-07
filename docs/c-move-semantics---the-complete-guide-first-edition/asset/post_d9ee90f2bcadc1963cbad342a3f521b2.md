
### 3.3.1 Special Member Functions

Let us first look briefly at the term *special member function*, because it is used in different ways. The C++ standard defines the following six operations as *special member functions*:

- Default constructor
- Copy constructor
- Copy assignment operator
- Move constructor (since C++11)
- Move assignment operator (since C++11)
- Destructor

However, in many cases such as in *the rule of five*, we talk only about five of these operations, because the default constructor is a little different from the other five (or three before C++11) operations. The other five operations are usually not declared and have more complex dependencies. So make sure you always know what is meant by the special member functions (I have tried to avoid this term so far).

Figure 3.1 gives an overview of when special member functions are automatically generated depending on which (other) constructors and special member functions are declared.³

![](img/7ef3d1ca55bdc192f1cc0929179f3d21_66_0.png)

*Figure 3.1. Rules for automatic generation of special member functions*

³ This table is adopted from Howard Hinnant with his kind permission.

There are a few basic rules you can see in this table:

- A default constructor is only declared automatically if no other constructor is user-declared.
- The special copy member functions and the destructor disable move support. The automatic generation of special move member functions is disabled (unless the moving operations are also declared). However, a request to move an object usually still works because the copy member functions are used as a fallback (unless the special move member functions are explicitly deleted).
- The special move member functions disable the normal copying and assignment. The copying and other moving special member functions are deleted so that you can only move (assign) but not copy (assign) an object (unless the other operations are also declared).

Let us look at some details.

### 3.3.2 By Default, We Have Copying and Moving

As written, by default, both copying and moving special member functions are generated for a class. Assume the following declaration of a class Person:

```cpp
class Person {
    ...
public:
    ...
    // NO copy constructor/assignment declared

    // NO move constructor/assignment declared

    // NO destructor declared
};
```

In this case, a Person can be both copied and moved:

```cpp
std::vector<Person> coll;

Person p{"Tina", "Fox"};
coll.push_back(p);              // OK, copies p
coll.push_back(std::move(p));   // OK, moves p
```

### 3.3.3 Declared Copying Disables Moving (Fallback Enabled)

When declaring a copying special member function (or the destructor), the automatic generation of the moving special member functions is disabled: Assume the following declaration of a class Person:

```cpp
class Person {
    ...
public:
    ...

    // copy constructor/assignment declared:
    Person(const Person&) = default;
    Person& operator=(const Person&) = default;

    // NO move constructor/assignment declared
};
```

Because the fallback mechanism works, copying and moving a `Person` compiles but the move is performed as a copy:

```cpp
std::vector<Person> coll;

Person p{"Tina", "Fox"};
coll.push_back(p);                 // OK, copies p
coll.push_back(std::move(p));      // OK, copies p
```

Thus, declaring a special member function with `= default` is not the same as not declaring it at all. The copy constructor and copy assignment are user-declared, which disables move construction and move assignment so that moves fall back to copies. A declared destructor has the same effect.

You might wonder why a declared destructor disables move semantics. The chapter about moved-from states discusses a concrete example of a class with a destructor that causes generated move semantics not to work properly.

### 3.3.4 Declared Moving Disables Copying

If you have user-declared move semantics, you have disabled copy semantics. The copying special member functions are deleted.

In other words, if the move constructor or the move assignment operator is explicitly declared (implemented, generated with `= default`, or disabled with `= delete`), you have disabled calls to the copy constructor and the copy assignment operator by declaring them with `= delete`. Assume the following declaration of a class `Person`:

```cpp
class Person {
    ...
public:
    ...
    // NO copy constructor declared

    // move constructor/assignment declared:
    Person(Person&&) = default;
    Person& operator=(Person&&) = default;
};
```

In this case, we have a move-only type. A `Person` can be moved but not copied:

```cpp
std::vector<Person> coll;

Person p{"Tina", "Fox"};
coll.push_back(p);                 // ERROR: copying disabled
coll.push_back(std::move(p));      // OK, moves p

coll.push_back(Person{"Ben", "Cook"});  // OK, moves temporary person into coll
```

Again, declaring a special member function with `= default` is not the same as not declaring it at all. However, this time, the consequences of the call are more severe: the attempt to copy an object will no longer compile.

A class supporting move operations but not copy operations can make sense. You can use such a *move-only* type to pass around ownership or handles of resources without sharing or copying them. In the C++ standard library there are a couple of move-only types (e.g., I/O stream classes, thread classes, and `std::unique_ptr<>`). See the chapter about move-only types for details.

### 3.3.5 Deleting Moving Makes No Sense

For the same reason, if you declare the move constructor as deleted, you cannot move (you have disabled this operation; any fallback is not used) and cannot copy (because a declared move constructor disables copy operations):

```cpp
class Person {
  public:
    ...
    // NO copy constructor declared

    // move constructor/assignment declared as deleted:
    Person(Person&&) = delete;
    Person& operator=(Person&&) = delete;
    ...
};
```

```cpp
Person p{"Tina", "Fox"};
coll.push_back(p);           // ERROR: copying disabled
coll.push_back(std::move(p)); // ERROR: moving disabled
```

You get the same effect by declaring copying special member functions as deleted and that is probably less confusing for other programmers.

Deleting the move operations and enabling the copy operations really makes no sense:

```cpp
class Person {
  public:
    ...
    // copy constructor explicitly declared:
    Person(const Person& p) = default;
    Person& operator=(const Person&) = default;

    // move constructor/assignment declared as deleted:
    Person(Person&&) = delete;
    Person& operator=(Person&&) = delete;
    ...
};
```

```cpp
Person p{"Tina", "Fox"};
coll.push_back(p);           // OK: copying enabled
coll.push_back(std::move(p)); // ERROR: moving disabled
```

In this case, `= delete` disables the fallback mechanism (and is therefore also not the same as not declaring it at all). The compiler finds the declaration and reports the call as an error.

A type that supports copying but fails when moving is called does not make any sense. For the user of such a class, copying would sometimes work, sometimes not. As a guideline: never `= delete` the special move member functions.⁴ If you want to disable both copying and moving, deleting the copying special member functions is enough.

### 3.3.6 Disabling Move Semantics with Enabled Copy Semantics

Based on what we have just discussed, we now know how to disable move semantics when copying still makes sense. Declaring the special move member functions as deleted is usually not the right way to do it because it disables the fallback mechanism.

The right way to disable move semantics while providing copy semantics is to declare one of the other special member functions (copy constructor, assignment operator, or destructor). I recommend that you default the copy constructor and the assignment operator (declaring one of them would be enough but might cause unnecessary confusion):

```cpp
class Customer {
    ...
public:
    ...
    Customer(const Customer&) = default;            // disable move semantics
    Customer& operator=(const Customer&) = default; // disable move semantics
};
```

Because no generated special move member functions are found, a nameless temporary customer or even a customer marked with `std::move()` is now copied:

```cpp
std::vector<Customer> customers;
...
customers.push_back(createCustomer());           // OK, falls back to copying
customers.push_back(std::move(customers[0]));     // OK, falls back to copying
```

However, it is usually better to implement the special move member functions to fix any problem a default generated move operation has. The chapter about moved-from states will discuss examples from practice.

Note that only declaring the special copy member functions breaks the common “rule of five,” which we will discuss later in detail. You have to declare the special copy member functions but cannot also declare the special move member functions (both deleting and defaulting would not work, implementing them makes the class unnecessarily complicated). Therefore, if you explicitly declare a copying special member function just to disable move semantics, add a big comment to ensure that this declaration is neither removed nor extended by a declaration of the special move member functions.
