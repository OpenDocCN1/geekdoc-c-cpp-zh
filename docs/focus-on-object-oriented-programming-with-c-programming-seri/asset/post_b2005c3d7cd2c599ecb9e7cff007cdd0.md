
## Overloading Copy Constructors

The initialization of a derived instance with an existing derived instance automatically invokes the copy constructor function in the derived class. Remember, if you fail to write one, the compiler will automatically supply one for you.

Note that even if you write a copy constructor for the base class, and someone derives a new class from that base class and writes a copy constructor for the derived class, then a potential problem exists because the compiler will not automatically invoke the copy constructor in the base class when the copy constructor in the derived class is invoked. Instead, the default copy constructor in the base class will get called!

The solution to this problem is to make an explicit call from the derived class copy constructor to the base class copy constructor. You do this using the constructor initialization list to write the name of the base class copy constructor and, within parentheses, the same argument that the derived class copy constructor received.

```cpp
// copyctor.cpp

#include <iostream>

using namespace std;

class Base {
    protected:
        int bnum;
    public:
        Base(int x=0) : bnum(x) {
            cout << "base constructor" << endl;
        }
        Base(const Base& b) : bnum(b.bnum) {
            cout << "base copy constructor" << endl;
        }
        ~Base() {
            cout << "base destructor" << endl;
        }
        int getBnum() const {
            return bnum;
        }
};

class Derived : public Base {
private:
    int dnum;
public:
    Derived(int x=0, int y=0) : Base(x), dnum(y) {
        cout << "derived constructor" << endl;
    }
    Derived(const Derived& d) : Base(d), dnum(d.dnum) {
        cout << "derived copy constructor" << endl;
    }
    ~Derived() {
        cout << "derived destructor" << endl;
    }
    int getDnum() const {
        return dnum;
    }
};

int main() {
    Derived d1(1, 2);
    Derived d2 = d1;    // or Derived d2(d1);
    cout << "d2 = " << d2.getBnum() << " , " << d2.getDnum() << endl;
    return 0;
}
```

output:
base constructor
derived constructor
base copy constructor
derived copy constructor
d2 = 1, 2
derived destructor
base destructor
derived destructor
base destructor

While making the call to the base class copy constructor, note that object d is simply an alias for object d1 (the existing instance), and that a cast occurs from a reference-to-derived into a reference-to-base. This is perfectly acceptable and normal code since the formal argument b in the base class copy constructor now is an alias for only the base class portion of the d1 instance.

## Overloading the Assignment Operator

The situation for the overloaded assignment operator in a derived class works in a fashion similar to that of the overloaded copy constructor. When you need to write an overloaded `operator=()` function in a derived class, it is your responsibility to make an explicit call to the overloaded `operator=()` function in the base class.

Unlike overloading a copy constructor function, you have complete control over when this call is made, although it makes sense to do it immediately so that the base portion of the derived object gets its data members assigned first, followed by the derived portion.

Remember, if the base class does not have an overloaded assignment operator, the compiler will supply one (that we may not like).

```cpp
// assign.cpp

#include <iostream>

using namespace std;

class Base {
    protected:
        int bnum;
    public:
        Base(int x=0) : bnum(x) {
            cout << "base constructor" << endl;
        }
        Base(const Base& b) : bnum(b.bnum) {
            cout << "base copy constructor" << endl;
        }

        Base& operator=(const Base& b) {
            cout << "base operator=()" << endl;
            if (&b != this) {
                bnum = b.bnum;
            }
            return *this;
        }

        ~Base() {
            cout << "base destructor" << endl;
        }

        int getBnum() const {
            return bnum;
        }
};

class Derived : public Base {
private:
    int dnum;
public:
    Derived(int x=0, int y=0) : Base(x), dnum(y) {
        cout << "derived constructor" << endl;
    }
    Derived(const Derived& d) : Base(d), dnum(d.dnum) {
        cout << "derived copy constructor" << endl;
    }
    Derived& operator=(const Derived& d) {
        cout << "derived operator=()" << endl;
        if (&d != this) {
            Base::operator=(d);
            dnum = d.dnum;
        }
        return *this;
    }
    ~Derived() {
        cout << "derived destructor" << endl;
    }
    int getDnum() const {
        return dnum;
    }
};

int main() {
    Derived d1(1, 2);
    Derived d2;

    d2 = d1;
    cout << "d2 = " << d2.getBnum() << ", " << d2.getDnum() << endl;
    return 0;
}
```

output:
base constructor
derived constructor
base constructor
derived constructor
derived operator=()
base operator=()
d2 = 1, 2
derived destructor
base destructor
derived destructor
base destructor

Note that the explicit call to the functions `Base::operator=()` was written using functional notation. If you want to use infix notation, you may use either of the following two methods:

- `(base)this = d;`
- `((base&)*this) = d;`

The first statement casts the `Derived` pointer into a `Base` pointer, and then dereferences the result to produce the `Base` class portion of the invoking instance. Therefore, the `Base` class `operator=()` will be called.

The second statement achieved the same result, but in a more direct fashion, with the invoking instance itself now cast into a reference to the `Base` class.

## Casting from Derived into Base

Casting from a derived class instance, pointer, or reference, into a base class object of the same type presents no problem to the compiler. We've seen previously how a reference-to-derived in the derived class copy constructor was passed into the base class copy constructor and received as a reference-to-base.

Since a derived class instance always contains a base class instance, when the cast occurs the compiler simply ignores the derived class portion of the instance that is being used, pointer at, or referred to. For example:

```
Derived d(1, 2);
```

creates an object of the derived class.

```
Base b = d;
```

creates an object of the base class. Here, however, a derived instance is used to initialize a base instance. Object b now only contains the Base class portion of object d.

```
Base *pbase = new Derived;
```

In this example, new Derived returns a pointer to a Derived object and is used to initialize a pointer to a Base object. In other words, a pointer to Derived is used to initialize a pointer to Base. So pBase "sees" only the Base class portion of the Derived object on the heap.

Remember, since a Derived class instance always contains a Base class instance, when the cast occurs, the compiler simply ignores the Derived class portion of the instance that is being pointed at.

## Casting from Base into Derived

On the other hand, if you attempt to cast from a base class instance, pointer, or reference into a derived class object of the same type, the compiler will complain because what you are trying to do now is put a smaller object (the base class) into a larger object (the derived class). The compiler will not let you do this automatically. We'll not worry about this at this time.

## Pointers to Base and Derived Class Instances

As we've already seen, pointers to base and derived class instances can be declared just like any other type of pointer. In terms of assignment, you can always assign a derived class pointer into a base class pointer, because then the base class pointer will be pointing (only) to the base class portion of the derived object.

- A base class pointer can always point to a base class instance,
- A derived class pointer can always point to a derived class instance.

When a pointer of type Base or Derived class is used to call a member function, and the function has been defined in both the base and derived classes, there is no ambiguity as to which version of the function will be called. The governing factor here is the type of the pointer itself.

```cpp
class Base {
public:
    void print() { cout << "Base class print()" << endl; }
};

class Derived : public Base {
public:
    void print() { cout << "Derived class print()" << endl; }
};

int main() {
    Base* pBase = new Base; // base class instance and pointer
    Derived* pDerived = new Derived; // derived class instance & pointer

    pBase->print(); // calls Base::print()
    pDerived->print(); // calls Derived::print()
    pDerived->Base::print(); // calls Base::print()
    delete pBase;
    delete pDerived;
    return 0;
}
```

output:
Base class print
Derived class print
Base class print
