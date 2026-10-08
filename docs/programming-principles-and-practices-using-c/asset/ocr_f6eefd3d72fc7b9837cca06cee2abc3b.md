• Functions within functions: local functions (also called nested functions)

```
```
void f()
{
    void g()    // illegal
    {
        // ...
    }
    // ...
}
```
```

This is not legal in C++; don’t do it. The compiler will reject it.

• Blocks within functions and other blocks: nested blocks

```
```
void f(int x, int y)
{
    if (x>y) {
        // ...
    }
    else {
        // ...
        {
            // ...
        }
        // ...
    }
}
```
```

Nested blocks are unavoidable, but be suspicious of complicated nesting: it can easily hide errors.

C++ also provides a language feature, **namespace**, exclusively for expressing scoping; see §8.7

Note our consistent indentation to indicate nesting. Without consistent indentation, nested constructs become unreadable. For example:

```
```
// dangerously ugly code
struct X {
    void f(int x) {
        struct Y {
            int f() { return 1; } int m;
        };
        int m;
        m=x; Y m2;
```
```