# ISO/IEC 14882:2017(E)

```
function& operator=(const function& f);
14   Effects: As if function(f).swap(*this);
15   Returns: *this.
    function& operator=(function&& f);
16   Effects: Replaces the target of *this with the target of f.
17   Returns: *this.
```

```
function& operator=(nullptr_t) noexcept
18   Effects: If *this != nullptr, destroys the target of this.
19   Postconditions: *(*this).
```

```
20   Returns: *this.
    template<class F> function& operator=(F&& f);
21   Effects: As if function(forward<F>(f)).swap(*this);
22   Returns: *this.
23   Remarks: This assignment operator shall not participate in order resolution unless decay_t<F> is Lvalue(23.14.13.2) for argument ArgTypes... and return R.
```

```
template<class F> function& operator=(reference_wrapper<F> f) noexcept
24   Effects: As if function(f).swap(*this);
25   Returns: *this.
```

```
-function();
26   Effects: If *this != nullptr, destroys the target of this.
```

# 23.14.13.2 function modifiers

```
void swap(function&& f) noexcept
1   Effects: interchanges the targets of *this and this other.
```

# 23.14.13.3 function capacity

```
explicit operator bool() const noexcept
1   Returns: true if *this has a target, otherwise false.
```

# 23.14.13.4 function invocation

```
R operator()(ArgTypes... args) const;
1   Returns: INVOKE<R>(f, std::forward<ArgTypes>(args)...) (23.14.3), where f is the target object (23.14.2).
```

```
2   Throws: bad_call if *this; otherwise, any exception thrown by the wrapped callable object.
```

# 23.14.13.5 function target access

```
const type_info& target_type() const noexcept;
1   Returns: If *this has a target of T, typeid(T); otherwise, typeid(void).
```

> [func.wrap.func.mod]

> [func.wrap.func.cap]

> [func.wrap.func.inv]

> [func.wrap.func.targ]