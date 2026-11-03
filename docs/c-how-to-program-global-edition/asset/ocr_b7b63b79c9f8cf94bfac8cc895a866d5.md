# 17.10 const Objects and const Member Functions

Let's see how the principle of least privilege applies to objects. Some objects need to be modifiable and some do not. You may use keyword const to specify that an object is not modifiable and that any attempt to modify the object should result in a compilation error. The statement

```
const Time noon( 12, 0, 0 );
```

declares a const object noon of class Time and initializes it to 12 noon. It's possible to instantiate const and non-const objects of the same class.

**Software Engineering Observation 17.8**
*Attempts to modify a const object are caught at compile time rather than causing execution-time errors.*

**Performance Tip 17.3**
*Declaring variables and objects const when appropriate can improve performance—compilers can perform optimizations on constants that cannot be performed on non-const variables.*

C++ disallows member function calls for const objects unless the member functions themselves are also declared const. This is true even for get member functions that do not modify the object. This is also a key reason that we've declared as const all member-functions that do not modify the objects on which they're called.

As you saw starting with class GradeBook in Chapter 16, a member function is specified as const both in its prototype by inserting the keyword const after the function's parameter list and, in the case of the function definition, before the left brace that begins the function body.

**Common Programming Error 17.2**
*Defining as const a member function that modifies a data member of the object is a compilation error.*

**Common Programming Error 17.3**
*Defining as const a member function that calls a non-const member function of the class on the same object is a compilation error.*

**Common Programming Error 17.4**
*Invoking a non-const member function on a const object is a compilation error.*

An interesting problem arises for constructors and destructors, each of which typically modifies objects. A constructor must be allowed to modify an object so that the object can be initialized properly. A destructor must be able to perform its termination housekeeping chores before an object's memory is reclaimed by the system. Attempting to declare a constructor or destructor const is a compilation error. The "constness" of a const object is enforced from the time the constructor completes initialization of the object until that object's destructor is called.