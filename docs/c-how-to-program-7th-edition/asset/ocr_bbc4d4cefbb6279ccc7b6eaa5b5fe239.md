```
```text
C:\\cpphtp7_examples\\ch10\\Fig10_07_09\\Increment.cpp(10) : error C2758:
    'Increment::increment' : must be initialized in constructor base/member
    initializer list
        C:\\cpphtp7_examples\\ch10\\Fig10_07_09\\increment.h(20) : see
            declaration of 'Increment::increment'
C:\\cpphtp7_examples\\ch10\\Fig10_07_09\\Increment.cpp(12) : error C2166:
    l-value specifies const object
```
```

```
```text
Increment.cpp:9: error: uninitialized member 'Increment::increment' with
    'const int'
Increment.cpp:12: error: assignment of read-only data-member
    'Increment::increment'
```
```

**Fig. 10.9** | Program to test class Increment generates compilation errors. (Part 2 of 2.)

Function print (Fig. 10.8, lines 16–19) is declared const. It might seem strange to label this function const, because a program probably will never have a const Increment object. However, it’s possible that a program will have a const reference to an Increment object or a pointer to const that points to an Increment object. Typically, this occurs when objects of class Increment are passed to functions or returned from functions. In these cases, only class Increment’s const member functions can be called through the reference or pointer. Thus, it’s reasonable to declare function print as const—doing so prevents errors in these situations where an Increment object is treated as a const object.

![](bbox=[0.158, 0.546, 0.214, 0.585])

**Error-Prevention Tip 10.1**  
*Declare as const all of a class’s member functions that do not modify the object in which they operate. Occasionally this may seem inappropriate, because you’ll have no intention of creating const objects of that class or accessing objects of that class through const references or pointers to const. Declaring such member functions const does offer a benefit, though. If the member function is inadvertently written to modify the object, the compiler will issue an error message.*

# 10.3 Composition: Objects as Members of Classes

An AlarmClock object needs to know when it’s supposed to sound its alarm, so why not include a Time object as a member of the AlarmClock class? Such a capability is called composition and is sometimes referred to as a has-a relationship—a class can have objects of other classes as members.

![](bbox=[0.159, 0.798, 0.214, 0.844])

**Software Engineering Observation 10.5**  
*A common form of software reusability is composition, in which a class has objects of other classes as members.*

When an object is created, its constructor is called automatically. Previously, we saw how to pass arguments to the constructor of an object we created in main. This section shows how an object’s constructor can pass arguments to member-object constructors via member initializers.