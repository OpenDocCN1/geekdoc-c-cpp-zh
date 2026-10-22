
```
}

template<typename> void f() {}

template<typename T> void h(T P) {
    f<int>(p); // #1
    g<int>(p); // #2 ERROR
}

int main() {
    h(N::e); // calls template h with T = N::E
}
```

In line #1, when seeing the name f followed by a <, the compiler has to decide whether that < is an angle bracket or a *less-than* sign. That depends on whether f is known to be the name of a template or not; in this case, ordinary lookup finds the declaration of f, which is indeed a template, and so parsing succeeds with angle brackets.

Line #2, however, produces an error because no template g is found using ordinary lookup; the < is thus treated as a less-than sign, which is a syntax error in this example. If we could get past this issue, we’d eventually find the template N::g using ADL when instantiating h for T = N::E (since N is a namespace associated with E), but we cannot get that far until we successfully parse the generic definition of h.

## 14.3.2 Points of Instantiation

We have already illustrated that there are points in the source of template clients where a C++ compiler must have access to the declaration or the definition of a template entity. A *point of instantiation* (POI) is created when a code construct refers to a template specialization in such a way that the definition of the corresponding template needs to be instantiated to create that specialization. The POI is a point in the source where the substituted template could be inserted. For example:

![](img/0d5072d8203dcaf6ef50e76a3d9a3203_311_0.png)

```
class MyInt {
public:
    MyInt(int i);
};

MyInt operator - (MyInt const&);

bool operator > (MyInt const&, MyInt const&);
```

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

different instantiation.

In practice, most compilers delay the actual instantiation of most function templates to the end of the translation unit. Some instantiations cannot be delayed, including cases where instantiation is needed to determine a deduced return type (see Section 15.10.1 on page 296 and Section 15.10.4 on page 303) and cases where the function is `constexpr` and must be evaluated to produce a constant result. Some compilers instantiate inline functions when they’re first used to potentially inline the call right away.⁹ This effectively moves the POIs of the corresponding template specializations to the end of the translation unit, which is permitted by the C++ standard as an alternative POI.

## 14.3.3 The Inclusion Model

Whenever a POI is encountered, the definition of the corresponding template must somehow be accessible. For class specializations this means that the class template definition must have been seen earlier in the translation unit. For the POIs of function and variable templates (and member functions and static data members of class templates) this is also needed, and typically template definitions are simply added to header files that are `#included` into the translation unit, even when they’re nontype templates. This source model for template definitions is called the *inclusion model*, and it is the only automatic source model for templates supported by the current C++ standard.¹⁰

Although the inclusion model encourages programmers to place all their template definitions in header files so that they are available to satisfy any POIs that may arise, it is also possible to explicitly manage instantiations using *explicit instantiation declarations* and *explicit instantiation definitions* (see Section 14.5 on page 260). Doing so is logistically not trivial and most of the time programmers will prefer to rely on the automatic instantiation mechanism instead. One challenge for an implementation with the automatic scheme is to deal with the possibility of having POIs for the same specialization of a function or variable templates (or the same member function or static data member of a class template instance) across different translation units. We discuss approaches to this problem next.

## 14.4 Implementation Schemes

linkable template instantiations in particular—may in fact appear in duplicate across the various object files and libraries. The compiler will typically mark these entities in a special way. When the linker finds multiple instances, it keeps one and discards all the others. There is not much more to it than that.

In theory, greedy instantiation has some serious drawbacks: 
- The compiler may be wasting time on generating and optimizing N instantiations, of which only one will be kept.
- Linkers typically do not check that two instantiations are identical because some insignificant differences in generated code can validly occur for multiple instances of one template specialization. These small differences should not cause the linker to fail. (These differences could result from tiny differences in the state of the compiler at the instantiation times.) However, this often also results in the linker not noticing more substantial differences, such as when one instantiation was compiled with strict floating-point math rules whereas the other was compiled with relaxed, higher-performance floating-point math rules.¹¹
- The sum of all the object files could potentially be much larger than with alternatives because the same code may be duplicated many times.
In practice, these shortcomings do not seem to have caused major problems. Perhaps this is because greedy instantiation contrasts very favorably with the alternatives in one important aspect: The traditional source-object dependency is preserved. In particular, one translation unit generates but one object file, and each object file contains compiled code for all the linkable definitions in the corresponding source file (which includes the instantiated definitions). Another important benefit is that all function template instances are candidates for inlining without resorting to expensive “link-time” optimization mechanisms (and, in practice, function template instances are often small functions that benefit from inlining). The other instantiation mechanisms treat inline function template instances specially to ensure they can be expanded inline. However, greedy instantiation allows even noninline function template instances to be expanded inline.

Finally, it may be worth noting that the linker mechanism that allows duplicate definitions of linkable entities is also typically used to handle duplicate spilled inlined functions¹² and virtual function dispatch tables.¹³ If this mechanism is not available, the alternative is usually to emit these items with internal linkage, at the expense of generating larger code. The requirement that an inline function have a single address makes it difficult to implement that alternative in a standard-conforming way.
