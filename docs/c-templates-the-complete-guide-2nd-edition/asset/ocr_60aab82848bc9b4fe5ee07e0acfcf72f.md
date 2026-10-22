However, as discussed in this chapter, using a template parameter T is no guarantee that it is not a reference, because T might sometimes implicitly be deduced as a reference: Click here to view code image

```
template<typename T>
T retR(T&& p) // p is a forwarding reference
{
return T{}; // OOPS: returns by reference when called for lvalues
}
```

Even when T is a template parameter deduced from a call-by-value call, it might become a reference type when explicitly specifying the template parameter to be a reference: Click here to view code image

```
template<typename T>
T retV(T p) //Note: T might become a reference
{
return T{}; // OOPS: returns a reference if T is a reference
}
```

```
int x;
retV<int&>(x); // retT() instantiated for T as int&
```

To be safe, you have two options: • Use the type trait std::remove_reference<> (see Section D.4 on page 729) to convert type T to a nonreference: Click here to view code image

```
template<typename T>
typename std::remove_reference<T>::type retV(T p)
{
return T{}; // always returns by value
}
```

Other traits, such as std::decay<> (see Section D.4 on page 731), may also be useful here because they also implicitly remove references.

+   • Let the compiler deduce the return type by just declaring the return type to be auto (since C++14; see Section 1.3.2 on page 11), because auto always decays: Click here to view code image

```
template<typename T>
auto retV(T p) // by-value return type deduced by compiler
{
return T{}; // always returns by value
}
```

# 7.6 Recommended Template Parameter Declarations