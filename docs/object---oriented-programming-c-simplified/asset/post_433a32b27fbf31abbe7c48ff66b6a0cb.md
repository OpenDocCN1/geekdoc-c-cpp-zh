
The student class has two private data members `sname` and **rollno**, and two **public** member functions: **input_st** and **show_st**. This **student** class is inherited by class `subject`, which has just one data member `subject` and two functions **input_sub** and **show_sub**. The functions for input and display of the student name and roll number are called in the functions of this class. The class `subject` is inherited by classes **Internal** and **External**, which we have seen earlier. Note both the classes inherit the class `Subject` in **virtual** public mode so only one copy of data members of class `Subject` will be available in class `Total` and no ambiguity will arise. Trace the program step wise. It is very simple to understand.

## 9.7 CONSTRUCTOR AND DESTRUCTOR IN INHERITANCE

When constructors are present both in base and derived classes then how they are called, how values are passed from derived class to base class? That we will see in this section. Assume a small example of single level inheritance in which `class A` is inherited by `class B`. Both the classes have their default constructors. When an object of `class B` is created, it calls the constructor of `class B`, but as this `class B` has got A as its parent class, constructor of `class A` will be called first, then constructor of class B. Then obviously it will be using the data members from base class. Now, without calling the constructor of the base class, the data members of the base class are not initialized, and unexpected results may follow. Calling a constructor of the base class first allows the base class to properly set up its data members so that they can be used by derived classes.

In case of destructor in inheritance, destructor of derived class is called first and then destructor of base class is called. This is so because if we call destructor of base class first, the destructor might be working with data members of base class. So, destroying them in the base class has the effect of working with the data members that no longer exist. Compiler won’t allow this. That’s why destructor of derived class is called first so that it can do its work finishing with any of the data members of base class and do its own cleaning.

```cpp
/*PROG 9.30 CONSTRUCTOR IN SINGLE LEVEL INHERITANCE VER 1 */

#include <iostream.h>
#include <conio.h>

class first
{
public :
        first( )
        {
                cout << "Hello from con of first" << endl;
        }
};

class second : first
{
public :
        second( )
        {
                cout << "Hello from con of second" << endl;
        }
};

void main()
{
    clrscr();
    second s;
    getch();
}
```

**OUTPUT:**

```text
Hello from con of first
Hello from con of second
```

**EXPLANATION:** When statement `second s;` executes it calls the default constructor of second class. But as class `first` is the base class for `second`, constructor of the base class is called first, then constructor of the derived class is called. So the output is as shown. Note constructors are called implicitly for both the classes by the compiler.

```cpp
/*PROG 9.31 CONSTRUCTOR IN SINGLE LEVEL INHERITANCE VER 2 */

#include <iostream.h>
#include <conio.h>

class first
{
public :
    first()
    {
        cout << "Hello from con of first" << endl;
    }
};

class second : public first
{
public :
    second() : first()
    {
        cout << "Hello from con of second" << endl;
    }
};

void main()
{
    clrscr();
    second s;
    getch();
}
```

**OUTPUT:**

```text
Hello from con of first
Hello from con of second
```

**EXPLANATION:** Here, when the default constructor of class `second` is called, the class `second` default constructor explicitly calls the constructor of class `first`. Though this is not necessary as we have seen in the program, this is another way of calling the constructor of the base class.

```cpp
/* PROG 9.32 CONSTRUCTOR & DESTRUCTOR IN SINGLE LEVEL INHERITANCE VER 1 */

#include <iostream.h>
#include <conio.h>

class first
{
public :
    first()
    {
        cout << "Hello from con" << endl;
    }
    ~first()
    {
        cout << "Bye Bye from des of first " << endl;
    }
};

class second : public first
{
public :
    second() : first()
    {
        cout << "Hello from con of second" << endl;
    }
    ~second()
    {
        cout << "Bye Bye from des of second" << endl;
    }
};

void main()
{
    clrscr();
    second s;
    getch();
}
```

**OUTPUT:**

```text
Hello from con
Hello from con of second
Bye Bye from des of second
Bye Bye from des of first
```

![Figure 9.13](img/ad5299318df8d4d7c6df5eaa86590ea3_464_0.png)

**Figure 9.13.** *Output screen of program after pressing (Ctrl + F9) and after pressing (Alt + F9)*

**EXPLANATION:** Destructors are called in the reverse order of constructors. So, destructor of second class will be called first, then destructor of first class will be called.

```cpp
/*PROG 9.33 CONSTRUCTOR IN TWO LEVEL INHERITANCE VER 1*/

#include <iostream.h>
#include <conio.h>

class first
{
public :
    first()
    {
        cout << "Hello from con of first" << endl;
    }
};

class second : public first
{
public :
    second() : first()
    {
        cout << "Hello from con of second" << endl;
    }
};

class third : second
{
public :
    third() : second()
    {
        cout << "Hello from con of third" << endl;
    }
};

void main()
{
    clrscr();
    third t;
    getch();
}
```

**OUTPUT:**

```text
Hello from con of first
Hello from con of second
Hello from con of third
```

**EXPLANATION:** When statement `third t;` executes it calls the default constructor of its own class. But before falling into the code of the default constructor, it must call constructor of class `second`, which is the base class for class `third`. In the class `second` default constructor, default constructor of class `first` is called, as class `first` is the base class for class `second`. So the output is as shown above.

```cpp
/* PROG 9.34 CONSTRUCTOR IN MULTIPLE INHERITANCE VER 1 */

#include <iostream.h>
#include <conio.h>

class first
{
public :
    first()
    {
        cout << "Hello from con first" << endl;
    }
};

class second
{
public :
    second()
    {
        cout << "Hello from con of second" << endl;
    }
};

class third : second, first
{
public :
    third()
    {
        cout << "Hello from con of third" << endl;
    }
};

void main()
{
    clrscr();
    third t;
    getch();
}
```

**OUTPUT:**

```text
Hello from con of second
Hello from con first
Hello from con of third
```

**EXPLANATION:** In multiple inheritance, the constructor of which base class is called is determined by which class was inherited first. Here in the class `third`, classes `first` and `second` are inherited as:

```cpp
class third : second, first
```

So, constructor of class `second` will be called first and constructor of class `first` will be called after that. Note if constructor of `third` class is written as:

```cpp
third() : first(), second()
{
    cout << "Hello from con of third" << endl;
}
```

Then also constructor of **second** class will be called, followed by constructor of **first** class.

```cpp
/* PROG 9.35 DEMO OF PARAMETERIZED CONSTRUCTOR IN INHERITANCE VER 1 */

#include <iostream.h>
#include <conio.h>

class first
{
    int fa;
public :
    first(int x)
    {
        fa = x;
        cout << "Con of first called";
    }
    void fshow()
    {
        cout << "fa = " << fa << endl;
    }
};

class second : public first
{
    int sa;
public :
    second(int a, int b) : first(a)
    {
        sa = b;
        cout << endl << "Con of second called" << endl;
    }
    void sshow()
    {
        fshow();
        cout << "sa=" << sa << endl;
    }
};

void main()
{
    clrscr();
    second s(10, 20);
    s.sshow();
    getch();
}
```

**OUTPUT:**

```text
Con of first called
Con of second called
fa =10
sa =20
```

**EXPLANATION:** When statement `second s(10, 20);` executes, object `s` calls the parameterized constructor of class `second` and passes parameters 10 and 20. Inside the constructor they are assigned to `a` and `b`. Before entering into the body of the constructor, `first(a)` calls the constructor of class `first` and passes `a` as argument. Inside the class `first`, it is assigned to `fa`, and “Con of first called” is displayed. When control enters into the constructor, it assigns `b` to `sa`. When `sshow()` of class `second` is called, it first calls the `fshow()` of class `first`.

```cpp
/*PROG 9.36 DEMO OF PARAMETERIZED CONSTRUCTOR IN INHERITANCE VER 2*/

#include <iostream.h>
#include <conio.h>

class first
{
    int fa;
public :
    first(int x)
    {
        fa = x;
        cout << " Con of first called" << endl;
    }
    void fshow()
    {
        cout << "fa=" << fa << endl;
    }
};

class second : public first
{
    int sa;
```
