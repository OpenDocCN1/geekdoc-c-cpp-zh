
```cpp
int main() {
    Stack s2;

    s2.push(5);
    s2.push(6);
    s2.push(7);
    cout << s2.pop();
    cout << s2.pop();
    cout << s2.pop();
    cout << s2.pop();
    return 0;
}
```

Note that functions push() and pop() in Stack have the same names, arguments, and return types are functions in class Stack. When we call these functions in main(), how does the compiler know which of the two functions to use?

> Rule: When the same function exists in both the base class and the derived class, the function in the derived class will be executed. The derived class functions override the base class functions.

# Hiding Overloaded Functions

You cannot overload (or hide) a base class function by redefining it in a derived class with a different argument list. The rationale behind this design is that if you override a function inherited from the base class, there should be no danger of accidentally calling the base class version through the process of argument matching.

In other words, if a base class function expects an int as an argument, and you hide it by redefining it in a derived class to accept a char*, then calling the function using a derived instance with an int actual argument should cause a compilation error.

```cpp
// hidel.cpp
class Base {
public:
    void foo(int n) { cout << n; }
};
class Derived : public Base {
public:
    void foo(double n) { cout << n * n; }
};
int main() {
    Derived d;

    d.foo(5);
    return 0;
}
```

This shows that a function inherited from the base class is not examined under the rules of argument matching. It appears that the function call using an int as the actual argument would be a better match for the Base class function that expects an int, rather than the Derived class function that expects a double. But the Derived class function is the one that gets called because it is the only one that the compiler knows about.

Even if there is no conceivable match within the scope of the Derived class, the inherited members from the Base class will not be examined.

```cpp
// hide2.cpp
class Base {
public:
    void foo(char *ptr) { cout << ptr; }
};

class Derived : public Base {
public:
    void foo(double n) { cout << n; }
};

int main() {
    Derived d;
    d.foo("A");      // error - cannot convert char * to double
    d.Base::foo("A"); // ok
    return 0;
}
```

# # Compiler Lookup Rules

Using derived instances to access member functions without the base class name and scope resolution operator, the compiler resolves the address by asking:

- Does the member function have scope in the derived class? If so, use it. If not, generate a compilation error.
- Does the member function have scope in the parent class? If so, use it. If not, generate a compilation error.
- Does the member function have scope higher up in the hierarchy? If so, use it. If not, generate a compilation error.

Note that functions with the same name at file scope are not considered.

Similarly, a function in a derived class resolves the address of a data member by asking:

- Does the data member have scope in the function class itself? If so, use it. If not, generate a compilation error.
- Does the data member have derived class scope? If so, use it. If not, generate a compilation error.
- Does the data member scope in the parent class that is accessible? If so, use it. If not, generate a compilation error.
- Does the data member have accessible scope up the hierarchy? If so, use it. If not, generate a compilation error.
- Does the data member exist at file scope? If so, use it. If not, generate a compilation error.

# Constructors and Destructors with Derived Classes

Recall that an instance of a derived class always contains the data members inherited from its base class. Therefore it logically follows that whenever a derived class instance gets created, two constructor functions are needed to ensure the proper initialization of all of the data members of the instance.

So the constructor for the base class must somehow get control to ensure the proper initialization of all of the data members of the instance. The constructor for the base class must somehow get control to ensure the proper initialization of all of the data members of the instance.

The base class is called as soon as the derived class constructor is invoked. The only question now is, which base class is called? The answer is this: If you fail to tell the compiler which one to call, the base class is called first.

One of the easiest ways to improve a C++ program's efficiency is to specify an appropriate base class constructor in the colon list of a derived class function. What happens without a constructor initialization list?

- To initialize an object of a particular class, your program calls the appropriate constructor for that class.
- To initialize a derived class's object, your program implicitly calls the appropriate base class function.

Unfortunately, that implicit call to the base class function makes it easy to initialize the base class's data members twice! See the example below:

```cpp
// constructor.cpp

#include <iostream>

using std;

class Base {
protected:
    int bNum;
public:
    Base(int n = 0) : bNum(n) {
        cout << "Base constructor" << endl;
    }
    void SetBase(int n) {
        cout << "set base to " << n << endl;
    }
    int getBaseNum() {
        return bNum;
    }
};

class Derived : public Base {
private:
    int dNum;
public:
    Derived(int a = 0, int b = 0) : Base(a), dNum(b) {
        cout << "Derived constructor" << endl;
        SetBase(a);
        SetDerived(b);
    }
    void SetDerived(int n) {
        cout << "set derived to " << n << endl;
    }
    int getDerivedNum() {
        return dNum;
    }
};

int main() {
    Derived d(1,2);

    cout << d.getBaseNum() << " " << d.getDerivedNum() << endl;
}
```

Here is the program’s output:

```
base constructor
derived constructor
set base to 1
set derived to 2
1 2
```

Note that the derived instance d is being created with two integers: 

Caution:

When you initialize base class members, do not attempt to list them individually in the member list of the derived class. Their initialization is not the responsibility of the derived class, and will cause a compilation error because the only items that can be written in a class initialization list are the derived class data member names and base class names.

Note that base class constructor and destructor functions are unique in the sense that they are not inherited by the derived class. If you create a derived class instance, then the proper constructor to handle that type of creation must exist within the derived class, not the base class.
