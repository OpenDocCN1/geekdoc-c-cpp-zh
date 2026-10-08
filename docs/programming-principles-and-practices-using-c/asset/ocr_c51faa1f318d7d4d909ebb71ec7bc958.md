Here, the compiler will see three functions that are independent of Shape::draw_lines() (because they have a different name or a different type) and won’t override them. A good compiler will warn about these likely mistakes. There is nothing you can or must say in an overriding function to ensure that it actually overrides a base class function.

The draw_lines() example is real and can therefore be hard to follow in all details, so here is a purely technical example that illustrates overriding:

```
```cpp
struct B {
    virtual void f() const { cout << "B::f"; }
    void g() const { cout << "B::g"; }    // not virtual
};

struct D : B {
    void f() const { cout << "D::f"; }    // overrides B::f
    void g() { cout << "D::g"; }
};

struct DD : D {
    void f() { cout << "DD::f"; }         // doesn’t override D::f (not const)
    void g() const { cout << "DD::g"; }
};
```
```

Here, we have a small class hierarchy with (just) one virtual function f(). We can try using it. In particular, we can try to call f() and the non-virtual g(), which is a function that doesn’t know what type of object it had to deal with except that it is a B (or something derived from B):

```
```cpp
void call(const B& b)
{
    b.f();
    b.g();
}

int main()
{
    B b;
    D d;
    DD dd;
```
// a D is a kind of B, so call() can accept a D
// a DD is a kind of D and a D is a kind of B, so call() can accept a DD
```