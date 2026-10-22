```
struct S {
    template<typename = void> friend void f();    // ERROR: not a definition
    template<typename = void> friend void g() {    // OK so far
    }
};
template<typename> void g();    // ERROR: g() was given a default template argument
                                 // when defined; no other declaration may exist here
```