
We can achieve this by making doubleDist() a friend of the Distance class:

```cpp
#include <iostream>

using namespace std;
class Distance {
private:
    int feet;
    float inches;
public:
    void setDist(int ft, float in);
    void getDist();
    void showDist();
    void addDist(Distance d2, Distance d3);
    Distance addDist(Distance d);
    friend Distance doubleDist(Distance d);
};

Distance::Distance(int ft, float in) {
    feet = ft;
    inches = in;
}

void Distance::setDist(int ft, float in) {
    feet = ft;
    inches = in;
}

void Distance::getDist() {
    cout << "feet: ";
    cin >> feet;
    cout << "inches: ";
    cin >> inches;
}

void Distance::showDist() {
    cout << feet << " " << inches << endl;
}

void Distance::addDist(Distance d2, Distance d3) {
    inches = d2.inches + d3.inches;
    feet = d2.feet + d3.feet;
    if (inches >= 12.0) {
        inches -= 12.0;
        feet++;
    }
}
```

```cpp
Distance Distance::addDist(Distance d) {
    Distance temp;
    temp.inches = inches + d.inches;
    temp.feet = feet + d.feet;
    if (temp.inches >= 12.0) {
        temp.inches -= 12.0;
        temp.feet += 1;
    }
    return temp;
}
```

```cpp
Distance doubleDist(Distance d) {
    int ft = d.feet * 2;
    float in = d.inches * 2;
    if (in >= 12.0) {
        ++ft;
        in = 12.0;
    }
    return Distance(ft, in);
}
```

In main(), we now say:

d2 = doubleDist(d1);

Note: where doubleDist(), as a member function, takes no arguments, it takes one as a friend.

In general, the friend version of a function requires one more argument than the function is a member.

# Chapter 10. References

Reference Variables
Reference Arguments
Returning References
References Homework

# Reference Variables

We know how to create pointers aliases that address other variables:

```cpp
int num = 5;
int *p = &num;
```

declares an int variable num initialized to 5 and an int pointer p to the address of num.

```cpp
cout << num << *p << endl; // 5 5
```

To use a pointer's address value requires dereferencing the pointer leading to many asterisks that could confuse code. C++ offers an alternative to pointer aliases called references. There are three main uses for references:

- * as variables
- as function parameters
- as function results

# Reference Variables

A reference variable in C++ is simply an alias for another variable. An alias is just another name for another variable. This means that whenever an alias is used, the action is really taking place on the variable to which the alias refers.

For example:

```cpp
int num = 5;
int& val = num;
```

This sets up a reference variable val and assigns it to the existing variable num. We say that val is a reference to an int. A reference variable contains the address of another variable, like a pointer. So val has the address of num.

At this point, the referenced location has two names associated with it: num and val.

```cpp
cout << num << val << endl; // 5 5
```

Because both variables point to the same location in memory, they are in fact the same variable and therefore output the same value. Note that unlike pointers, reference variables are automatically dereferenced when they are used. There is therefore no need for the asterisk *.

```cpp
++num;
cout << num << val << endl;    // 6 6
++val;
cout << num << val << endl;    // 7 7
```

Any assignment made to num is reflected through val and any assignment to val is reflected through num. Any operation on val has precisely the effect as an operation on num.

```cpp
int z = 100;
val = z;
cout << num << val << endl;    // 100 100
```

This does not cause val to refer to z since the compiler always dereferences the address for you. The above code will copy the value of z into num.

Note: Once a reference variable is initialized to some existing value, it cannot be changed or reassigned to some other variables as long as the reference variable remains in scope. However, the value the reference variable points to can always change.

# Rule of References

When a reference variable is created, it must always be initialized with the name of some other existing variable. That means references must be initialized in their declarations:

```cpp
int& iref; // error
```

Unlike a pointer that can be declared in an uninitialized state, or set to NULL if the pointer does not address valid data, a reference must always refer to an object. There is no equivalent of a NULL pointer for a reference.

References do not have to be pre-initialized in four special cases:

- * when declared
- when used as function arguments
- when used as function results
- in class declarations

Some examples:

- int& - reference to an int
- int*& - reference to a pointer

```cpp
int a1;
int& a2 = a1; // a2 is an alias for a1
int* a3 = &a2; // a3 is a pointer to a2, which is an alias for a1
```

Wait, let's continue.

# Reference Arguments

The declaration of reference variables up to now has not really served a very useful purpose. After all, if a variable and an alias for that variable are both defined within the same scope, then why bother to use the alias? Why not just use the name of the variable itself?

The real usefulness of a reference variable occurs when it is created in a scope that is different from the scope of the variable for which it has an alias. For example, a function sets up a new scope whenever it is created. If a reference variable is used as a formal parameter, then it merely becomes an alias for the corresponding actual parameter or argument to the function call. This means that whenever the formal parameter is used within the body of the function, the actual parameter in the calling function is the one that is really manipulated

# Simulate Call By Reference

```cpp
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x = 4, y = 6;
    swap(&x, &y);
    return 0;
}
```

The swap() function:

- declares the function parameter to be a pointer
- uses the dereferenced pointer in the function body
- passes an address as an argument when the function is called

# Address of a Reference

We can show that reference variables are not separate entities with their own addresses. If you take the address of a reference variable, all you will get the address of the variable for which it is alias. For example:

```cpp
#include <cstdio>

int main() {
    int num1;
    int& num2 = num1;
    printf("%p  %p", &num1, &num2); // FFFFFFFF FFFFFFFF
    return 0;
}
```

Therefore a reference variable does not have its unique address.

# Reference Variables are Useless!

Finally, reference variables are generally useless!!!

If you already have a variable, all reference to the variable will provide complexity. Now you'll have two ways of changing the same variable. You'll gain nothing from reference variables. It's messy as it sounds and you should think hard before you decide you must use a reference variable.

References were really designed for argument passing and return values and reference variables were only included for syntactic completeness, not necessarily because they were a good idea. References are usually necessary only in the context of a user-defined class type.
