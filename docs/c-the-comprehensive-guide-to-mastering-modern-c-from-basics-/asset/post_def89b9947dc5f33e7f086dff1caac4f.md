
guidelines is as a specification for tools that happens to be readable by humans.

The general goal of the guidelines is to create a codebase over time that is shared by multiple developers worldwide. A style should emerge similar here there and pursues similar goals. This way, everyone can more easily familiarize themselves with new projects over time, and their code is also quicker to read for others, and thus self-documenting. Adhering to the guidelines partially fulfils itself, as one guideline is that code should document itself as much as possible.

However, the guidelines should not force anyone to use only a part of the language, nor is code that does not follow the guidelines necessarily bad. The primary guideline is still that C++ is expressive and performant, and an author must be able to exploit this when it is right and important.

But if you follow the guidelines, you can expect your code to become more correct, safer, and more maintainable without becoming slower.

Many of the guidelines aim to make your life easier overall by relying more on the static type system of C++.

## 30.2.2 Type Safety

### Do Not Weaken the Type Safety of C++

Type safety is weakened by the use of void* or reinterpret_cast, with limitations by other forms of explicit type conversions, and by (unmarked) union.

If you need to use one of these-mentioned operations because a third party requires it, then hide it behind a layer maintained by you. Do not let void* spread in your code.

### Avoid "Type Dumpsters"

Do not use string and int for everything. Be more specific by introducing, for example, Month.

Trick question: What does the following function do?

```
Color createColor(int a, int b, int c);
Color createColor(int a, int b, int c, int d);
```

There is no correct answer here. You should make the interface cleaner, for which there are many possibilities:

```
Color createColor(Red r, Green g, Blue b);
Color createColor(Cyan c, Magenta m, Yellow y, Black k);
```

This is even better than just naming the parameters, r, g, and b. This way, you can hide it in the data type whether the red component is specified from 0 to 100, from 0 to 255, or even as a double between 0.0 and 1.0.

You avoid accidentally swapping the components this way. And what if you actually wanted to call

createColor(a,b,d) but forgot a component and instead called createColor(a,c,d)? Then you have called the completely wrong function.

### Relevant Guidelines

The relevant guidelines here include the following:

- P.1: Express ideas directly in code.
- P.4: Ideally, a program should be statically type safe.
- I.1: Make interfaces explicit.
- I.24: Avoid adjacent arguments of the same type (...).
- Type.1: Avoid costs. (Especially do not use reinterpret_cast).
- Type.2: Do not use static_cast to downcast. Use dynamic_cast Instead.
- Type.3: Do not use const_cast to cast away const (i.e., at all).
- Type.4: Do not use C-style (T)expression or functional T(expression) casts: prefer construction or named casts or T(expression).

Use std::chrono and std::time_point for time units. You can also use the type-safe boost::units for calculations with numerical units.

Write constructors in such a way that

## 30.2.3 Use RAII

- when you create an object, you can always clean it up in the destructor; and
- if you throw an exception, no resources remain de-allocated.

So it must always be possible to create either a complete object or none at all. A complete object can be one that holds an error state. The main thing is that it is correctly cleaned up in the destructor.

I have advocated for this multiple times in this book. Construction and destruction of objects are explained in detail Chapter 16. The problems with raw pointers and their alternatives are discussed Chapter 20.

### All or None: The Default Operations

As a reminder, C++ defines the following default operations:

- A default constructor: X()
- copy constructor: X(const X&)
- copy assignment: operator=(const X&)
- move constructor: X(X&&)
- move assignment: operator=(X&&)
- destructor: ~X()

You make it easiest for yourself if you follow the rule of zero, meaning neither defining nor deleting the default operations with =delete. Let the compiler do its job and generate the default operations itself.

Of course, this only works if the compiler-generated default operations do what they are supposed to do.

That means you should correctly initialize, copy, and move, and not leave any resources behind.

This, in turn, is easiest if you only use data fields that follow those rules themselves. Built-in types, aggregates, standard containers, smart pointers, and most other data structures of the standard library adhere to that. Raw pointers T* and references T&, which own their objects, do not.

Of course, some classes—those that connect to an external resource—require special attention, starting with the destructor. If that is the case, then the rule is this: define or delete all default operations (if possible or reasonable, also the default constructor). In practice, you need a custom-written destructor exactly when you have to manage a resource yourself. And if that is the case, resource must be accounted for when copying, moving, assigning.

### Do You Know the Guidelines for Construction, Assignment, and Moving?

However, if you need to define the default operations, keep in mind that implementing them is possible but not trivial. You should rely on the compiler whenever possible.

### Pitfall: Noncreated Object

If the constructor exits with an exception, the object is considered not created. The destructor is not called.

### Pitfall: Created Object Despite Exception

You avoid code duplication by delegating constructors. But remember that in the presence of delegating constructors, not every exception means that the destructor will not be called.

```cpp
// https://godbolt.org/z/ve4dc
struct Day {
    Day(int a, int b) : Day() { // delegates
        if(a==0 || b == 0) // throws exception
            throw 666;
    }
    Day() {}
};
int main() {
    try {
        Day(1,2);
    } catch(int) {}
}
```

Here, the first constructor has already been run and the object is thus constructed. This means the destructor will be called. This is not a problem in this simple example, but it can become one in more complicated cases.

### Relevant Guidelines

These run through all guidelines and sections. Here are some of the most obvious and relevant ones (with annotations in square brackets):

- P.8: Don’t leak any resources.
- F.22: Use T* or owner<T*> to designate a single object. [That means T* should not be used for pointer arithmetic. This is good for automated tools.]
- Sections C.defop, C.dtor, C.ctor, C.copy. [Here you will find plenty of tips on (whether and how) to implement the default operations.]
- R.1: Manage resources automatically using resource handles and RAII.
- R.3: A raw pointer T* is nonowning. [T* p does not own the object, so delete p should be avoided; instead, owner<T*> p with delete p is fine, etc.]
- R.4: A raw reference T is nonowning. [No int& r = *new int{7} followed by delete &r.]
- R.5: Prefer scoped objects; don’t heap-allocate unnecessarily. [Not with new or malloc or otherwise.]
