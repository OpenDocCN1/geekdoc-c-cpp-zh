
```cpp
void test(complex z1)
{
    complex z2 {z1};    // copy initialization
    complex z3;
    z3 = z2;             // copy assignment
    // ...
}
```

```cpp
void bad_copy(Vector v1)
{
    Vector v2 = v1; // copy v1's representation into v2
    v1[0] = 2;      // v2[0] is now also 2!
    v2[1] = 3;      // v1[1] is now also 3!
}
```

```cpp
class Vector {
public:
    Vector(int s); // constructor: establish invariant, acquire resources
    ~Vector() { delete[] elem; } // destructor: release resources

    Vector(const Vector& a); // copy constructor
    Vector& operator=(const Vector& a); // copy assignment

    double& operator[](int i);
    const double& operator[](int i) const;

    int size() const;
private:
    double* elem; // elem points to an array of sz doubles
    int sz;
};
```

```cpp
Vector::Vector(const Vector & a)    // copy constructor
    :elem{new double[a.sz]},         // allocate space for elements
      sz{a.sz}
{
    for (int i=0; i!=sz; ++i)                // copy elements
        elem[i] = a.elem[i];
}
```

```cpp
Vector& Vector::operator=(const Vector& a) // copy assignment
{
    double* p = new double[a.sz];
    for (int i=0; i<a.sz; ++i)
        p[i] = a.elem[i];
    delete[] elem; // delete old elements
    elem = p;
    sz = a.sz;
    return *this;
}
```

```cpp
Vector operator+(const Vector& a, const Vector& b)
{
    if (a.size()b.size())
        throw Vector_size_mismatch{};

    Vector res(a.size());

    for (int i=0; i!=a.size(); ++i)
        res[i]=a[i]+b[i];
    return res;
}
```

```cpp
void f(const Vector& x, const Vector& y, const Vector& z)
{
    Vector r;
    // ...
    r = x+y+z;
    // ...
}
```

```cpp
class Vector {
    // ...

    Vector(const Vector& a);      // copy constructor
    Vector& operator=(const Vector& a); // copy assignment

    Vector(Vector&& a);           // move constructor
    Vector& operator=(Vector&& a);   // move assignment
};
```

```cpp
Vector::Vector(Vector&& a)
    :elem{a.elem}, // "grab the elements" from a
      sz{a.sz}
{
    a.elem = nullptr; // now a has no elements
    a.sz = 0;
}
```

```cpp
Vector f()
{
    Vector x(1000);
    Vector y(2000);
    Vector z(3000);
    z = x; // we get a copy (x might be used later in f())
    y = std::move(x); // we get a move (move assignment)
    // ... better not use x here ...
    return z; // we get a move
}
```

```cpp
std::vector<thread> my_threads;

Vector init(int n)
{
    thread t(heartbeat); // run heartbeat concurrently (in a separate thread)
    my_threads.push_back(std::move(t)); // move t into my_threads ($16.6)
    // ... initialization ...

    Vector vec(n);
    for (auto& x : vec) {
        x = 777; // move vec out of init()
    }
    return vec;
}

auto v = init(1'000'000); // start heartbeat and initialize v
```

```cpp
class Matrix {
    // ...
    Matrix& operator=(const Matrix& a); // assign m to *this; return a reference to *this
};
```

```cpp
Matrix operator+(const Matrix& m1, const Matrix& m2); // assign m1 to m2 and return the sum
```

```cpp
X a = something;
X b = a;
assert(a==b); // If a!=b here, something is very odd (§4.5)
```

```cpp
namespace NX {
    class X {
        // ...

        bool operator==(const X&, const X&);
        // ...
    };
}
```

```cpp
class R {
    // ...
    auto operator<=>(const R& a) const = default;
};

void user(R r1, R r2)
{
    bool b1 = (r1<=r2) == 0; // r1==r2
    bool b2 = (r1<=r2) < 0; // r1<r2
    bool b3 = (r1<=r2) > 0; // r1>r2

    bool b4 = (r1==r2);
    bool b5 = (r1<r2);
}
```

```cpp
struct R2 {
    int m;
    auto operator<=>(const R2 & a) const { return a.m == m ? 0 : a.m < m ? -1 : 1; }
};
```

```cpp
void user(R2 r1, R2 r2)
{
    bool b4 = (r1==r2); // error: no non-default ==
    bool b5 = (r1<r2); // OK
}
```

```cpp
struct R3 { /* ... */ };

auto operator<=>(const R3& a, const R3& b) { /* ... */ };

bool operator==(const R3& a, const R3& b) { /* ... */ };
```

```cpp
string s1 = "asdf";
string s2 = "asdf";

bool b1 = s1==s2;
bool b2 = s1<s2;
```

```cpp
for (int i=0; i!=a.size(); ++i)
    res[i] = a[i]+b[i];
```

```cpp
Vector r
{
    // ...
}
```

```cpp
struct R3 {
    // ...
};

auto operator<=>(const R3& a, const R3& b) {
    // ...
}
```
