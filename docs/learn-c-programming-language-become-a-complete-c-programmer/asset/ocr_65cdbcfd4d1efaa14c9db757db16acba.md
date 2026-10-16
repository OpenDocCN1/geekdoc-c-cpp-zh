data members last to emphasize the functions providing the public user interface. For example:

```
class Date3 {
public:
Date3(int dd, int mm, int yy);
void add_year(int n); // add n years
private:
int d, m, y;
};
```

In real code, where both the public interface and the implementation details typically are more extensive than in tutorial examples, I usually prefer the style used for Date3. Access specifiers can be used many times in a single class declaration. For example:

```
class Date4 {
public:
Date4(int dd, int mm, int yy);
private:
int d, m, y;
public:
void add_year(int n); // add n years
};
```

Having more than one public section, as in Date4, tends to be messy, though, and might affect the object layout (§20.5). So does having more than one private section. However, allowing many access specifiers in a class is useful for machine-generated code.

# 16.2.5 Constructors

The use of functions such as init() to provide initialization for class objects is inelegant and errorprone. Because it is nowhere stated that an object must be initialized, a programmer can forget to do so – or do so twice (often with equally disastrous results). A better approach is to allow the programmer to declare a function with the explicit purpose of initializing objects. Because such a function constructs values of a given type, it is called a constructor. A constructor is recognized by having the same name as the class itself. For example:

```
class Date {
int d, m, y;
public:
Date(int dd, int mm, int yy); // constructor
// ...
};
```

When a class has a constructor, all objects of that class will be initialized by a constructor call. If the constructor requires arguments, these arguments must be supplied:

```
Date today = Date(23,6,1983);
```