class for qualification works) or multiple base classes may declare the same name (in which case we may have to use a specific base class name for disambiguation).

Note that the name one in the call one(e) is dependent on the template parameter simply because the type of one of the call’s explicit arguments is dependent. Implicitly used default arguments with a type that depends on a template parameter do not count because the compiler cannot verify this until it already has decided the lookup—a chicken-and-egg problem. To avoid subtlety, we prefer to use the this-> prefix in all situations that allow it—even for nontemplate code.

If you find that the repeated qualifications are cluttering up your code, you can bring a name from a dependent base class in the derived class once and for all:

Click here to view code image

```
// Variation 3:
template<typename T>
class DD3 : public Base<T> {
public:
using Base<T>::basefield; // #1 dependent name now in scope
void f() { basefield = 0; } // #2 fine
};
```

The lookup at point #2 succeeds and finds the using declaration of point #1. However, the using declaration is not verified until instantiation time and our goal is achieved. There are some subtle limitations to this scheme. For example, if multiple bases are derived from, the programmer must select exactly which one contains the desired member.

When searching for a qualified name within the current instantiation, the C++ standard specifies that name lookup first search in the current instantiation and in all nondependent bases, similar to the way it performs unqualified lookup for that name. If any name is found, then the qualified name refers to a member of a current instantiation and will not be a dependent name.¹⁵ If no such name is found, and the class has any dependent bases, then the qualified name refers to a member of an unknown specialization. For example:

Click here to view code image

```
class NonDep {
public:
using Type = int;
};

template<typename T>
class Dep {
public:
```