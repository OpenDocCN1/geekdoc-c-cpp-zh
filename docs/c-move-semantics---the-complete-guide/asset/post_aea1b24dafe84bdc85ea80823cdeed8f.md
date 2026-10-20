
## 3.3.1 Special Member Functions

Let us first look briefly at the term *special member function*, because it is used in different ways. The C++ standard defines the following six operations as *special member functions*:

- Default constructor
- Copy constructor
- Copy assignment operator
- Move constructor (since C++11)
- Move assignment operator (since C++11)
- Destructor

However, in many cases such as in *the rule of five*, we talk only about five these operations, because the default constructor is a little different to the other five (or three before C++11) operations. The other five operations are usually not declared and have more complex dependencies. So make sure you always know what is meant by *the* special member functions (I have tried to avoid this term so far).

Figure 3.1 gives an overview of when special member functions are automatically generated depending on which (other) constructors and special member functions are declared:

![](img/c6f2c4fe3e0701d95a17354ad517147a_66_0.png)

There are a few basic rules you can see in this table:

- A default constructor is only declared automatically if no other constructor is user-declared.
- The special copy member functions and the destructor disable move support. The automatic generation of special move member functions is disabled (unless the moving operations are also declared). However,

3 This table is adopted from Howard Hinnant with his kind permission.

still a request to move an object usually works because the copy member functions are used as a fallback (unless the special move member functions are explicitly deleted).

- The special move member functions disable the normal copying and assignment. The copying and other moving special member functions are deleted so that you can only move (assign) but not copy (assign) an object (unless the other operations are also declared).

Let us look at some details.

### 3.3.2 By Default, We Have Copying and Moving

As written, by default, both copying and moving special member functions are generated for a class.

Assume the following declaration of a class Person:

```
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

```
std::vector<Person> coll;
```

```
Person p{"Tina", "Fox"};
coll.push_back(p);                // OK, copies p
coll.push_back(std::move(p));    // OK, moves p
```

### 3.3.3 Declared Copying Disables Moving (Fallback Enabled)

When declaring a copying special member function (or the destructor), we have the automatic generation of the moving special member functions disabled:

Assume the following declaration of a class Person:

```
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

### 3.3 Rules for Special Member Functions

Because the fallback mechanism works, copying and moving a Person compiles but the move is performed as a copy:

```
std::vector<Person> coll;

Person p{"Tina", "Fox"};
coll.push_back(p); // OK, copies p
coll.push_back(std::move(p)); // OK, copies p
```

Thus, declaring a special member function with =default is not the same as not declaring it at all. The copy constructor and copy assignment are user-declared, which disables move construction and move assignment so that moves fall back to copies. A declared destructor has the same effect.

You might wonder why a declared destructor disables move semantics. The chapter about moved-from states discusses a concrete example of a class with a destructor that causes generated move semantics not to work properly.

### 3.3.4 Declared Moving Disables Copying

If you have user-declared move semantics, you have disabled copy semantics. The copying special member functions are deleted.

In other words, if the move constructor or the move assignment operator is explicitly declared (implemented, generated with =default, or disabled with =delete), you have disabled to call the copy constructor and the copy assignment operator by declaring them with =delete.

```
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

In this case, we have a move-only type. A Person can be moved but not copied:

```
std::vector<Person> coll;

Person p{"Tina", "Fox"};
coll.push_back(p); // ERROR: copying disabled
coll.push_back(std::move(p)); // OK, moves p

coll.push_back(Person{"Ben", "Cook"}); // OK, moves temporary person into coll
```

Again, declaring a special member function with =default is not the same as not declaring it at all. However, this time, the consequences for the caller are more severe: the attempt to copy an object will no longer compile.

A class supporting move operations but not copy operations can make sense. You can use such a move-only type to pass around ownership or handles of resources without sharing or copying them. In the C++ standard library there are a couple of move-only types (e.g., I/O stream classes, thread classes, and std::unique_ptr<>). See the chapter about move-only types for details.

### 3.3.5 Deleting Moving Makes No Sense

For the same reason, if you declare the move constructor as deleted, you cannot move (you have disabled this operation; any fallback is not used) and cannot copy (because a declared move constructor disables copy operations):

```
class Person {
  public:
    ...
    // NO copy constructor declared
    
    // move constructor/assignment declared as deleted:
    Person(Person&&) = delete;
    Person& operator=(Person&&) = delete;
    ...
};

Person p{"Tina", "Fox"};
coll.push_back(p);                // ERROR: copying disabled
coll.push_back(std::move(p));     // ERROR: moving disabled
```

You get the same effect by declaring copying special member functions as deleted and that is probably less confusing for other programmers.

Deleting the move operations and enabling the copy operations really makes no sense:

```
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

Person p{"Tina", "Fox"};
coll.push_back(p);                // OK: copying enabled
coll.push_back(std::move(p));     // ERROR: moving disabled
```

### Copy Constructor

The copy constructor is automatically generated when all of the following apply:⁵

- No move constructor is user-declared
- No move assignment operator is user-declared

If generated (implicitly or with =default), the copy constructor has the following behavior:⁶

```
MyClass(const MyClass& obj) noexcept-specifier
  : Base(obj), value(obj.value) {
}
```

The generated copy constructor first passes the source object, to the best matching copy constructor of the base class(es). (remember that copy constructors are always called on a top-down basis). It prefers the copy constructor with the same declaration (usually declared const&), but if that is not available it might call the next best matching constructor (e.g., a copy constructor template). Afterwards, it copies all members of its class (again using the best match).

The generated copy constructor is declared as noexcept if all copy operations (the copy constructors of all base classes and the copy constructors of all members) give this guarantee.

### Move Constructor

The move constructor is automatically generated when all of the following apply:

- No copy constructor is user-declared
- No copy assignment operator is user-declared
- No move assignment operator is user-declared
- No destructor is user-declared

If generated (implicitly or with =default), the move constructor has the following behavior:

```
MyClass(MyClass&& obj) noexcept-specifier
  : Base(std::move(obj)), value(std::move(obj.value)) {
}
```

The generated move constructor first passes the source object, marked with std::move() to pass through its move semantics, to the best matching move constructor of the base class(es). The best matching move constructor usually is the one with the same declaration (declared with &&). However, if that is not available it might call the next best matching constructor (e.g., a move constructor template or even a copy constructor). Afterwards, it moves all members of its class (again using the best match).

You might wonder, why after performing a move in the base class obj.value is still used here. The reason is that a base class can only see its members. Therefore, class MyClass knows that its member value still has its value and can perform the move.

The generated move constructor is declared as noexcept if all called move/copy operations (the copy or move constructors of all base classes and the copy or move constructors of all members) give this guarantee.
