# 28.4.3 Enable_if and Concepts

We can use Enable_if for a wide variety of predicates, including many tests of type properties (§28.3.1.1). Concepts are among the most general and useful predicates we have. Ideally, we would like to overload based on concepts, but lacking language support for concepts, the best we can do is to use Enable_if to select based on constraints. For example:

```
template<typename T>
Enable_if<Ordered<T>()> fct(T*,T*); // optimized implementation
template<typename T>
Enable_if<!Ordered<T>()> fct(T*,T*); // nonoptimized implementation
```

Note that Enable_if defaults to void, so fct() is a void function. I’m not sure that using that default increases readability, but we can use fct() like this:

```
void f(vector<int>& vi, vector<complex<int>>& vc)
{
if (vi.size()==0 || vc.size()==0) throw runtime_error("bad fct arg");
fct(&vi.front(),&vi.back()); // call optimized
fct(&vc.front(),&vc.back()); // call nonoptimized
}
```

These calls are resolved as described because we can use < for an int but not for a complex<int>. Enable_if resolves to void if we don’t provide a type argument.

# 28.4.4 More Enable_if Examples

When using Enable_if, sooner or later we want to ask if a class has a member with a specific name and an appropriate type. For many of the standard operations, such as constructors and assignments, the standard library provides a type property predicate, such as is_copy_assignable and is_default_constructible (§35.4.1). However, we can build our own predicates. Consider the question “Can we call f(x) if x is of type X?” Defining has_f to answer that question gives an opportunity to demonstrate some of the techniques used and some of the scaffolding/boilerplate code provided internally in many template metaprogramming libraries (including parts of the standard library). First, define the usual class plus specialization to represent an alternative:

```
struct substitution_failure { }; // represent a failure to declare something
template<typename T>
struct substitution_succeeded : std::true_type {};
template<>
struct substitution_succeeded<substitution_failure> : std::false_type
{};
```

Here, substitution_failure is used to represent a substitution failure (§23.5.3.2). We derive from std::true_type unless the argument type is substitution_failure. Obviously, std::true_type and std::false_type are types that represent the values true and false, respectively: