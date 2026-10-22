full instantiation by default.

# 14.2.2 Instantiated Components

When a class template is implicitly (fully) instantiated, each declaration of its members is instantiated as well, but the corresponding definitions are not (i.e., the member are partially instantiated). There are a few exceptions to this. First, if the class template contains an anonymous union, the members of that union’s definition are also instantiated.³ The other exception occurs with virtual member functions. Their definitions may or may not be instantiated as a result of instantiating a class template. Many implementations will, in fact, instantiate the definition because the internal structure that enables the virtual call mechanism requires the virtual functions actually to exist as linkable entities.

Default function call arguments are considered separately when instantiating templates. Specifically, they are not instantiated unless there is a call to that function (or member function) that actually makes use of the default argument. If, on the other hand, the function is called with explicit arguments that override the default, then the default arguments are not instantiated.

Similarly, exception specifications and default member initializers are not instantiated unless they are needed.

Let’s put together some examples that illustrate some of these principles:

Click here to view code image

details/lazy1.hpp

```
template<typename T>
class Safe {
};
```

```
template<int N>
class Danger {
int arr[N]; // OK here, although would fail for N<=0
};
```

```
template<typename T, int N>
class Tricky {
public:
void noBodyHere(Safe<T> = 3); // OK until usage of default value
results in an error
void inclas() {
Danger<N> noBoomYet; // OK until inclas() is used with N<=0
}
```