# 9.5.4 Coroutine definitions [dcl.fct.def.coroutine]

3 [Example 1: One can prevent default initialization and initialization by non-doubles with

```
struct onlydouble {
    onlydouble() = delete;            // OK, but redundant
    template<class T>
        onlydouble(T) = delete;
    onlydouble(double);
};
```

— end example]

[Example 2: One can prevent use of a class in certain new-expressions by using deleted definitions of a user-declared operator new for that class.

```
struct sometype {
    void* operator new(std::size_t) = delete;
    void* operator new[](std::size_t) = delete;
};
sometype* p = new sometype;      // error: deleted class operator new
sometype* q = new sometype[3];   // error: deleted class operator new[]
```

— end example]

[Example 3: One can make a class uncopyable, i.e., move-only, by using deleted definitions of the copy constructor and copy assignment operator, and then providing defaulted definitions of the move constructor and move assignment operator.

```
struct moveonly {
    moveonly() = default;
    moveonly(const moveonly&) = delete;
    moveonly(moveonly&&) = default;
    moveonly& operator=(const moveonly&) = delete;
    moveonly& operator=(moveonly&&) = default;
    ~moveonly() = default;
};
moveonly* p;
moveonly q(*p);                  // error: deleted copy constructor
```

— end example]

4 A deleted function is implicitly an inline function (9.2.8).

[Note 2: The one-definition rule (6.3) applies to deleted definitions. — end note]

A deleted definition of a function shall be the first declaration of the function or, for an explicit specialization of a function template, the first declaration of that specialization. An implicitly declared allocation or deallocation function (6.7.5.5) shall not be defined as deleted.

[Example 4:

```
struct sometype {
    sometype();
};
sometype::sometype() = delete;  // error: not first declaration
```

— end example]

1 A function is a coroutine if its function-body encloses a coroutine-return-statement (8.7.5), an await-expression (7.6.2.4), or a yield-expression (7.6.17). The parameter-declaration-clause of the coroutine shall not terminate with an ellipsis that is not part of a parameter-declaration.

2 [Example 1:

```
task<int> f();

task<void> g1() {
    int i = co_await f();
    std::cout << "f() => " << i << std::endl;
}
```