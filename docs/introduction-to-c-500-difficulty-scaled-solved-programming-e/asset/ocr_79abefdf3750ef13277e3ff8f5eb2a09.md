# 526 Introduction to C++

there is no problem, the defined constructor will be called. In addition to the default constructor that does not accept parameters, a constructor with predefined values in all of its arguments is also considered a default constructor. For example:

```
Student(const string& n = "No name", int c = 0, float g = 0);
```

Now, the Student s declaration is acceptable. Note if you specify a constructor, it is not allowed to define the default (e.g., Student()). Because both can be called without arguments, the Student s; declaration would produce a compilation error for ambiguity, as the compiler couldn't determine which of the two to call. To sum up, create a default constructor, we can use no arguments or default values for all arguments

As another example of the default constructor, consider the following class:

```
class A
private:
    int x, v;
public:
    A(int i, int j = 0);
    ...
};
```

See now which declarations are accepted:

```
A a; // there is no default constructor.
A a(1, 2); // OK.
A a(1); // the default value of j is used.
```

The default constructor can also be useful when a member of the class is object. For example:

```
class C // Example 17.7
public:
    int p;
public:
    C() {};
    C(int m) {p = m};
    ...
};
```

```
class B
public:
    C c;
    ...
};
```

```
int main()
{
    B b;
    ...
};
```

For the construction of the b object the default constructor of class B is called and for the construction of the c object the default constructor of class C is called. If it was missing, the compiler would display an error message, as it could not construct the c object.