For many uses, the functionality of enable_if is pretty ideal. However, the notation we have to use is often awkward. Consider:

```
Enable_if<Is_class<T>(),T> * operator->();
```

The implementation shows through rather dramatically. However, what is actually expressed is pretty close to the minimal ideal:

```
declare_if (Is_class<T>()) T * operator->(); // not C++
```

However, C++ does not have a declare_if construct for selecting declarations.
Using Enable_if to decorate the return type places it up front where you can see it and where it logically belongs, because it affects the whole declaration (not just the return type). However, some declarations do not have a return type. Consider two of vector’s constructors:

```
template<typename T>
class vector<T> {
public:
vector(size_t n, const T& val); // nelements of type T with value val
template<typename Iter>
vector(Iter b, Iter e); // initialize from [b:e)
// ...
};
```

This looks innocent enough, but the constructor taking a number of elements wrecks its usual havoc. Consider:

```
vector<int> v(10,20);
```

Is that 10 elements with the value 20 or an attempt to initialize from [10:20]? The standard requires the former, but the code above would naively pick the latter because an int-to size_t conversion is required for the first constructor whereas the pair of ints is a perfect match for the template constructor. The problem is that I “forgot” to tell the compiler that the Iter type should be an iterator. However, that can be done:

```
template<typename T>
class vector<T> {
public:
vector(size_t n, const T& val); // nelements of type T with value val
template<typename Iter, typename =Enable_if<Input_iterator<Iter>(),Iter>>
vector(Iter b, Iter e); // initialize from [b:e)
// ...
};
```

That (unused) default template argument will be instantiated because we certainly can’t deduce that unused template parameter. This implies that the declaration of vector(Iter,Iter) will fail unless Iter is an Input_iterator (§24.4.4).

I introduced the Enable_if as a default template argument because that is the most general solution. It can be used for templates without arguments and/or without return types. However, in this case, we could alternatively apply it to the constructor argument type: