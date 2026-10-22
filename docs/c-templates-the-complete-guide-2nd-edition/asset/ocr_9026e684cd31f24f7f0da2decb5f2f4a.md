```
```cpp
using Int = MyInt;

template<typename T>
void f(T i)
{
    if (i>0) {
        g(-i);
    }
}
// #1
void g(Int)
{
    // #2
    f<Int>(42); // point of call
    // #3
}
// #4
```
```

When a C++ compiler sees the call `f<Int>(42)`, it knows the template `f` will need to be instantiated for T substituted with `MyInt`. A POI is created. Points #2 and #3 are very close to the point of call, but they cannot be POIs because C++ does not allow us to insert the definition of `::f<Int>(Int)` there. The essential difference between point #1 and point #4 is that at point #4 the function `g(Int)` is visible, and hence the template-dependent call `g(-i)` can be resolved. However, if point #1 were the POI, then that call could not be resolved because `g(Int)` is not yet visible. Fortunately, C++ defines the POI for a reference to a function template specialization to be immediately after the nearest namespace scope declaration or definition that contains that reference. In our example, this is point #4.

You may wonder why this example involved the type `MyInt` rather than simple `int`. The answer lies in the fact that the second lookup performed at the POI is only an ADL. Because `int` has no associated namespace, the POI lookup would therefore not take place and would not find function `g`. Hence, if we were to replace the type alias declaration for `Int` with `using Int = int;` the previous example would no longer compile. The following example suffers from a similar problem: [Click here to view code image](#)

```
```cpp
template<typename T>
void f1(T x)
{
    g1(x); // #1
}

void g1(int)
{
```
```