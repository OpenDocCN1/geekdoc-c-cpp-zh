A default constructor is used if no arguments are specified or if an empty initializer list is provided: Vector v1; // OK
Vector v2 {}; // OK

A default argument (§12.2.5) can make a constructor that takes arguments into a default constructor. For example:

```
class String {
public:
String(const char* p = ""); // default constructor :empty string
// ...
};
String s1; // OK
String s2 {}; // OK
```

The standard-library vector and string have such default constructors (§36.3.2, §31.3.2).

The built-in types are considered to have default and copy constructors. However, for a built-in type the default constructor is not invoked for uninitialized nonstatic variables (§17.3). The default value of a built-in type is 0 for integers, 0.0 for floating-point types, and nullptr for pointers. For example:

```
void f()
{
int a0; int a1();
// uninitialized
// function declaration (intended?)
int a {};
double d {};
// a becomes 0 // d becomes 0.0 char* p {}; // p becomes nullptr
int* p1 = new int; // uninitialized int
int* p2 = new int{}; // the int is initialized to 0
}
```

Constructors for built-in types are most often used for template arguments. For example:

```
template<class T>
struct Handle {
T* p;
Handle(T* pp = new T{}) :p{pp} { }
// ...
};
Handle<int> px; // will generate int{}
```

# Section 17.3.3 Default Constructors 495

The generated int will be initialized to 0.