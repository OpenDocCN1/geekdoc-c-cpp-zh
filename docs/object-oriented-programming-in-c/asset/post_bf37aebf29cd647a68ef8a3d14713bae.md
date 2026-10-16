
by D. The class D, in effect, will have more members than what it contains at the time of declaration as shown in Fig. 8.2.

![](img/58ab8f034e2127e80560390a921c2523_203_0.png)

Fig. 8.2: Adding more members to a class (by public derivation)

The program illustrates that the objects of class D have access to all the public members of B. Let us have a look at the functions show_a() and mul():

```
void show_a()
{
    cout << "a = " << a << "\n";
}
```

```
void mul()
{
    c = b * get_a();        // c = b * a
}
```

Although the data member a is private in B and cannot be inherited, objects of D are able to access it through an inherited member function of B.

Let us now consider the case of private derivation.

```
public:
    void mul(void);
    void display(void);
};

//-----------------------------------------------

void B :: get_ab(void)
{
    cout << "Enter values for a and b:";
    cin >> a >> b;
}

int B :: get_a()
{
    return a;
}

void B :: show_a()
{
    cout << "a = " << a << "\n";
}

void D :: mul()
{
    get_ab();
    c = b * get_a();      // 'a' cannot be used directly
}

void D :: display()
{
    show_a();             // outputs value of 'a'
    cout << "b = " << b << "\n"
         << "c = " << c << "\n\n";
}

//-----------------------------------------------

int main()
{
    D d;

    // d.get_ab();  WON'T WORK
    d.mul();
    // d.show_a();  WON'T WORK
    d.display();
```

```
.....        // within its class
protected:
.....        // visible to member functions
.....        // of its own and derived class
public:
.....        // visible to all functions
.....        // in the program
};
```

When a **protected** member is inherited in **public** mode, it becomes **protected** in the derived class too and therefore is accessible by the member functions of the derived class. It is also ready for further inheritance. A **protected** member, inherited in the **private** mode derivation, becomes **private** in the derived class. Although it is available to the member functions of the derived class, it is not available for further inheritance (since **private** members cannot be inherited). Figure 8.4 is the pictorial representation for the two levels of derivation.

![](img/58ab8f034e2127e80560390a921c2523_205_0.png)

Fig. 8.4: Effect of inheritance on the visibility of members

## MULTIPLE INHERITANCE

```
#include <iostream>

using namespace std;

class M
{
    protected:
        int m;
    public:
        void get_m(int);
};

class N
{
    protected:
        int n;
    public:
        void get_n(int);
};

class P : public M, public N
{
    public:
        void display(void);
};

void M :: get_m(int x)
{
    m = x;
}

void N :: get_n(int y)
{
    n = y;
}

void P :: display(void)
{
    cout << "m = " << m << "\n";
    cout << "n = " << n << "\n";
    cout << "m*n = " << m*n << "\n";
}

int main()
{
    P p;

    p.get_m(10);
    p.get_n(20);
    p.display();

    return 0;
}
```

PROGRAM 8.4

The output of Program 8.4 would be:

```
m = 10
n = 20
m*n = 200
```

### Ambiguity Resolution in Inheritance

Occasionally, we may face a problem in using the multiple inheritance, when a function with the same name appears in more than one base class. Consider the following two classes.

```
class M
{
public:
    void display(void)
    {
        cout << "Class M\n";
    }
};

class N
{
public:
    void display(void)
    {
        cout << "Class N\n";
    }
};
```

Which display() function is used by the derived class when we inherit these two classes? We can solve this problem by defining a named instance within the derived class, using the class resolution operator with the function as shown below:

```
class P : public M, public N
{
    public:
        void display(void)        // overrides display() of M and N
        {
            M :: display();
        }
};
```

We can now use the derived class as follows:

```
int main()
{
    P p;
    p.display();
}
```

Ambiguity may also arise in single inheritance applications. For instance, consider the following situation:

```
class A
{
    public:
        void display()
        {
            cout << "A\n";
        }
};
class B : public A
{
    public:
        void display()
        {
            cout << "B\n";
        }
};
```

In this case, the function in the derived class overrides the inherited function and, therefore, a simple call to display() by B type object will invoke function defined in B only. However, we may invoke the function defined in A by using the scope resolution operator to specify the class.

Example:

```
int main()
{
```

### 8.12 Member Classes: Nesting of Classes

Inheritance is the mechanism of deriving certain properties of one class into another. We have seen in detail how this is implemented using the concept of derived classes. C++ supports yet another way of inheriting properties of one class into another. This approach takes a view that an object can be a collection of many other objects. That is, a class can contain objects of other classes as its members as shown below:

```
class alpha {...};
class beta {...};
class gamma
{
    alpha a;        // a is an object of alpha class
    beta b;         // b is an object of beta class
    ....
};
```

All objects of gamma class will contain the objects a and b. This kind of relationship is called containership or nesting. Creation of an object that contains another object is very different than the creation of an independent object. An independent object is created by its constructor when it is declared with arguments. On the other hand, a nested object is created in two stages. First, the member objects are created using their respective constructors and then the other 'ordinary' members are created. This means, constructors of all the member objects should be called before its own constructor body is executed. This is accomplished using an initialization list in the constructor of the nested class.

Example:

```
class gamma
{
    ....
    alpha a;        // a is object of alpha
    beta b;         // b is object of beta
public:
    gamma(arglist): a(arglist1), b(arglist2)
    {
        // constructor body
    }
};
```

arglist is the list of arguments that is to be supplied when a gamma object is defined. These parameters are used for initializing the members of gamma. arglist1 is the argument list

### Review Questions

- 8.1 What does inheritance mean in C++?
- 8.2 What are the different forms of inheritance? Give an example for each.
- 8.3 Describe the syntax of the single inheritance in C++.
- 8.4 We know that a private member of a base class is not inheritable. Is it anyway possible for the objects of a derived class to access the private members of the base class? If yes, how? Remember, the base class cannot be modified.
- 8.5 How do the properties of the following two derived classes differ?
  - (a) class D1: private B{ / ... };
  - (b) class D2: public B{ / ... };
- 8.6 When do we use the protected visibility specifier to a class member?
- 8.7 Describe the syntax of multiple inheritance. When do we use such an inheritance?
- 8.8 What are the implications of the following two definitions?
  - (a) class A: public B, public C{ / ... };
  - (b) class A: public C, public B{ / ... };
- 8.9 What is a virtual base class?
- 8.10 When do we make a class virtual?
- 8.11 What is an abstract class?
- 8.12 In what order are the class constructors called when a derived class object is created?
- 8.13 Class D is derived from class B. The class D does not contain any data members of its own. Does the class D require constructors? If yes, why?
- 8.14 What is containership? How does it differ from inheritance?
- 8.15 Describe how an object of a class that contains objects of other classes created?
- 8.16 State whether the following statements are TRUE or FALSE:
  - (a) Inheritance helps in making a general class into a more specific class.
  - (b) Inheritance aids data hiding.
  - (c) One of the advantages of inheritance is that it provides a conceptual framework.
  - (d) Inheritance facilitates the creation of class libraries.
  - (e) Defining a derived class requires some changes in the base class.
  - (f) A base class is never used to create objects.
  - (g) It is legal to have an object of one class as a member of another class.
  - (h) We can prevent the inheritance of all members of the base class by making base class virtual in the definition of the derived class.

### Debugging Exercises

- 8.1 Identify the error in the following program.

```
#include <iostream.h>
```
