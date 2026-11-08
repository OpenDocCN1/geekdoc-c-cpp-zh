Suppose this version of `Array` is instantiated for type `float`. The friend operator function is then declared as a result of that instantiation, but note that this function itself is not an instantiation of a function template. It is a normal non-template function that gets injected in the global scope as a side effect of the instantiation process. Because it is a non-template function, it will be treated with other overloaded functions. The function templates were added to the language. Barton and Nackman called this restricted template approach because it avoided the use of a template parameter — `T` — that applied to all types? (in other words, unrestricted expansion).

# Because

Click here to view code image

```
operator<< (const Array<T> const&)
```

is defined inside a class definition, it is implicitly considered to be an inline function, and when therefore is added to delegate the implementation to a static member function, which doesn't need to be inline.

Name lookup for friend function definitions has changed since 1994, so the Barton-Nackman trick is not as useful in standard C++. At the time of its invention, friend declarations would be visible in the enclosing scope of a class template when that template was instantiated via a process called friend injection. Historically, when a friend function was declared in a class template, its declaration was found by argument-dependent lookup (see Section 13.2.2 on page 220 for the specific details). This means that at least one of the arguments of the function call must already have the class containing the friend function as an associated class. The friend function would not be found if the arguments were of an unrelated class type that could be converted to the class containing the friend.

Click here to view code image

```
class S {

};

template<typename T>
class Wrapper {
private:
    T object;
public:
    Wrapper(T obj) : object(obj) { // implied comment
    }

    friend void foo(Wrapper<T> const&);
};

int main()
{
    S s;

    Wrapper<S> w(s);

    foo(w); // ERROR: Wrapper<S> is not associated with the argument
    foo(s); // ERROR: Wrapper<S> is not associated with the argument
}
```

Here, the call `foo(s)` is valid because the function `foo()` is a friend declared in `Wrapper<S>` which is a class associated with the argument `s`. However, in the call `foo(s)`, the friend declaration of function `foo(Wrapper<S> const&)` is not visible because the class `Wrapper<S>` is not instantiated in that call. The friend function is defined in the class template, so it is implicitly considered to be an inline function. Even though the class is not instantiated, the constructor of `Wrapper<S>` is the only function that is considered because the candidate function `foo()` is not inlined in the first place. At the time Barton and Nackman invented their trick, friend name injection was made the friend function visible and call `foo()` would succeed.

In modern C++, the only advantages to defining a friend function in a class template over simply defining an ordinary function template are syntactic: friend function definitions have access to the private and protected members of their enclosing class and don't need to restate all of the template parameters of enclosing class templates. However, friend function definitions can be useful when the Curiously Recurring Template Pattern (CRTP), as illustrated in the operator implementations described in the following sections.