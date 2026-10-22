```
```cpp
class Base :
public Mixins... { public:
// the virtuality of foo() depends on its declaration
// (if any) in the base classes Mixins...
void foo() {
std::cout << "Base::foo()" << '\n';
}
};

template<typename... Mixins>
class Derived : public Base<Mixins...> {
public:
void foo() {
std::cout << "Derived::foo()" << '\n';
}
};

int main()
{
Base<NotVirtual>* p1 = new Derived<NotVirtual>;
p1->foo(); // calls Base::foo()

Base<Virtual>* p2 = new Derived<Virtual>;
p2->foo(); // calls Derived::foo()
}
```
```

This technique can provide a tool to design a class template that is usable both to instantiate concrete classes and to extend using inheritance. However, it is rarely sufficient just to sprinkle virtuality on some member functions to obtain a class that makes a good base class for more specialized functionality. This sort of development method requires more fundamental design decisions. It is therefore usually more practical to design two different tools (class or class template hierarchies) than to try to integrate them all into one template hierarchy.

# 21.4 Named Template Arguments

Various template techniques sometimes cause a class template to end up with many different template type parameters. However, many of these parameters often have reasonable default values. A natural way to define such a class template may look as follows: [Click here to view code image](#)

```
```cpp
template<typename Policy1 = DefaultPolicy1,
typename Policy2 = DefaultPolicy2,
typename Policy3 = DefaultPolicy3,
typename Policy4 = DefaultPolicy4>
class BreadSlicer {
```
```