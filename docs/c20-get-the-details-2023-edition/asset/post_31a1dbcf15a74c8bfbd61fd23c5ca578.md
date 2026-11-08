
## 3.2 Core Language

![](img/c60a87adb7f61e2e82071d081bbb389a_30_0.png)

### 3.2.1 Three-Way Comparison Operator

The **three-way comparison operator** (`<=>`), or spaceship operator, determines, for two values A and B, whether A < B, A == B, or A > B.

By declaring the three-way comparison operator `default`, the compiler will attempt to generate a consistent relational operator for the class. In this case, you get all six comparison operators: `==`, `!=`, `<`, `<=`, `>`, and `>=`.

**Auto-generating the three-way comparison operator**

```cpp
struct MyInt {
    int value;
    MyInt(int value) : value(value) { }
    auto operator<=>(const MyInt&) const = default;
};
```

The compiler-generated operator `<=>` performs a lexicographical comparison, starting with the base classes and taking into account all the non-static data members in their declaration order. Here is a quite sophisticated example from the Microsoft blog: [Simplify Your Code with Rocket Science: C++20's Spaceship Operator](https://devblogs.microsoft.com/cppblog/simplify-your-code-with-rocket-science-c20s-spaceship-operator/).

1 https://devblogs.microsoft.com/cppblog/simplify-your-code-with-rocket-science-c20s-spaceship-operator/

**Spaceship operator for derived classes**

```cpp
struct Basics {
    int i;
    char c;
    float f;
    double d;
    auto operator<=>(const Basics&) const = default;
};

struct Arrays {
    int ai[1];
    char ac[2];
    float af[3];
    double ad[2][2];
    auto operator<=>(const Arrays&) const = default;
};

struct Bases : Basics, Arrays {
    auto operator<=>(const Bases&) const = default;
};

int main() {
    constexpr Bases a = { { 0, 'c', 1.f, 1 },
        { { 1 }, { 'a', 'b' }, { 1.f, 2.f, 3.f }, {{ 1., 2. }, { 3., 4. } } } };
    constexpr Bases b = { { 0, 'c', 1.f, 1 },
        { { 1 }, { 'a', 'b' }, { 1.f, 2.f, 3.f }, {{ 1., 2. }, { 3., 4. } } } };
    static_assert(a == b);
    static_assert(!(a != b));
    static_assert(a <= b);
    static_assert(!(a > b));
    static_assert(a >= b);
}
```

I assume the most complicated stuff in this code snippet is not the spaceship operator but the initialization of Bases using aggregate initialization. Aggregate initialization essentially means that you can directly initialize the members of class types (class, struct, or union) if all members are public. In this case, you can use a brace initialization list, as in the example.

Before I discuss designated initialization, let me show more about aggregate initialization. Here is a straightforward example.

**Aggregate initialization**

```cpp
struct Point2D{
  int x;
  int y;
};

class Point3D{
public:
  int x;
  int y;
  int z;
};

int main(){

  std::cout << "\n";

  Point2D point2D {1, 2};
  Point3D point3D {1, 2, 3};

  std::cout << "point2D: " << point2D.x << " " << point2D.y << "\n";
  std::cout << "point3D: " << point3D.x << " "
            << point3D.y << " " << point3D.z << "\n";

  std::cout << '\n';

}
```

This is the output of the program:

![](img/c60a87adb7f61e2e82071d081bbb389a_32_0.png)

The aggregate initialization is quite error-prone, because you can swap the constructor arguments without realizing it. Explicit is better than implicit. Let’s see what that means. Take a look at how designated initializers from C99, now part of the C++ standard, intervene.

### 3.2.2 Designated Initialization

**Designated initialization**

```cpp
struct Point2D{
    int x;
    int y;
};

class Point3D{
public:
    int x;
    int y;
    int z;
};

int main(){

    Point2D point2D {.x = 1, .y = 2};
    // Point2D point2D {.y = 2, .x = 1};          // error
    Point3D point3D {.x = 1, .y = 2, .z = 2};
    // Point3D point3D {.x = 1, .z = 2}           // {1, 0, 2}

    std::cout << "point2D: " << point2D.x << " " << point2D.y << "\n";
    std::cout << "point3D: " << point3D.x << " " << point3D.y << " " << point3D.z
              << "\n";

}
```

The arguments for the instances of Point2D and Point3D are explicitly named. The output of the program is identical to the output of the previous one. The commented-out lines 16 and 18 are quite interesting. Line 16 would give an error because the order of the designators does not match the declaration order of the data members. As for line 18, the designator for y is missing. In this case, y is initialized to 0, such as when using braced initialization list {1, 0, 2}.

### 3.2.3 consteval and constinit

The new `consteval` specifier added in C++20 creates an immediate function. For an immediate function, each invocation of the function must produce a compile-time constant expression. An immediate function is implicitly a constexpr function but not necessarily the other way around.

**An immediate function**

```cpp
consteval int sqr(int n) {
    return n*n;
}
constexpr int r = sqr(100);  // OK

int x = 100;
int r2 = sqr(x);             // Error
```

The final assignment gives an error because x is not a constant expression and, therefore, sqr(x) cannot be performed at compile time.

constinit ensures that the variable with static storage duration or thread storage duration is initialized at compile time. Static storage duration means that the object is allocated when the program begins and is deallocated when the program ends. Thread storage duration means that the object's lifetime is bound to the lifetime of the thread.

constinit ensures for this kind of variable (static storage duration or thread storage duration) that they are initialized at compile time. constinit does not imply constness.

### 3.2.4 Template Improvements

C++20 offers various improvements to programming with templates. A generic constructor is a catch-all constructor because you can invoke it with any type.

**An implicit and explicit generic constructor**

```cpp
struct Implicit {
    template <typename T>
    Implicit(T t) {
        std::cout << t << '\n';
    }
};

struct Explicit {
    template <typename T>
    explicit Explicit(T t) {
        std::cout << t << '\n';
    }
};

Explicit exp1 = "implicit";  // Error
Explicit exp2{"explicit"};
```

## 3.3 The Standard Library

![](img/c60a87adb7f61e2e82071d081bbb389a_36_0.png)

- **The Big Four**
  - Concepts
  - Modules
  - Ranges library
  - Coroutines

- **Core Language**
  - Three-way comparison operator
  - Designated initializers
  - consteval and constinit
  - Template improvements
  - Lambda improvements
  - New attributes

- **Library**
  - std::span
  - Container improvements
  - Atomic utilities
  - Calendar and time zone
  - Formatting library

- **Concurrency**
  - Atomics
  - Semaphores
  - Latches and barriers
  - Cooperative interruption
  - std::jthread

### 3.3.1 std::span

A std::span represents an object that can refer to a contiguous sequence of objects. A std::span, sometimes also called a view, is never an owner. This view can be a C-array, a std::array, a pointer with a size, or a std::vector. A typical implementation of a std::span needs a pointer to its first element and a size. The main reason for having a std::span is that a plain array will decay to a pointer if passed to a function; therefore, its size is lost. std::span automatically deduces the size of an array, a std::array, or a std::vector. If you use a pointer to initialize a std::span, you have to provide the size in the constructor.

**std::span as function argument**

```cpp
void copy_n(const int* src, int* des, int n){}

void copy(std::span<const int> src, std::span<int> des){}

int main(){

    int arr1[] = {1, 2, 3};
    int arr2[] = {3, 4, 5};

    copy_n(arr1, arr2, 3);
    copy(arr1, arr2);

}
```

Compared to the function `copy_n`, `copy` doesn't need the number of elements. Hence, a common cause of errors is gone with `std::span<T>`.
