# C++ Namespaces

The purpose of namespaces is to localize the names of identifiers in order to avoid name collisions. Prior to the invention of namespaces, top-level names competed for slots in the global namespace and thus conflicts could occur. For example, if our program defined a function called abs(), could (depending upon its parameter list) override the standard library function abs() because both names would be stored in the global namespace.

The creation of the namespace keyword solves this problem. A namespace allows the same name to be used in different contexts without conflicts arising. This is done by localizing the visibility of names to the namespace in which they are declared.

The **namespace** keyword allows us to partition the global namespace by creating a declarative region. A namespace defines a scope for all of the identifiers that are declared in it. The syntax for a namespace is:

```
namespace name {
// declarations
}
```

The visibility of any name defined within a namespace block is confined to the scope of the namespace.

```
namespace counter_namespace {
int upperbound;
int lowerbound;
class Counter {
int count;
public:
counter(int n) {
if(n <= upperbound)
count = n;
}
```