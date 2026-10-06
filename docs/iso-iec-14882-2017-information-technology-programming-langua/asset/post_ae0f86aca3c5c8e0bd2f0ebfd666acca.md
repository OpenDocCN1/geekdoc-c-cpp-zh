
# ISO/IEC 14882:2017(E)

Rationale: Necessary to enable C++ 2014 hexadecimal literals.
Effect on original feature: Valid C++ 2014 code may fail to compile or produce different results in this International Standard. Special characters like0p+0 and 0x1_p+0 are three separate tokens in C++ 2014, but one single token in this International Standard.

```cpp
#define F(a) b ## a
int b = F(0p);    // ill-formed; equivalent to 'int b = bop + 0;' in C++ 2014
```

## C.4.2 Clause 8: expressions

Change: Remove increment operator with bool operand.
Rationale: Obsolete feature: Valid C++ 2014 expression utilizing the increment operator on a bool lvalue is ill-formed in this International Standard. Note that this might occur when the lvalue has been given by a template parameter.

Change: Dynamic allocation mechanism for over-aligned types.
Rationale: Simplify usage. C++ 2014 code uses a new-expression to allocate an object with an over-aligned class type, which has no allocation functions of its own; ::operator new(std::size_t) is used to allocate the memory. In this International Standard, ::operator new(std::size_t, std::align__) is used instead.

## C.4.3 Clause 10: declarations

Change: Remove register storage-class-specifier.
Rationale: Enable repurposing of deprecated keyword in future revisions of this International Standard.
Effect on original feature: Valid C++ 2014 declaration utilizing the storage-class-specifier is ill-formed in this International Standard. The specifier can be simply removed to retain the original meaning.

Change: auto deduction from braced-init-list.
Rationale: More intuitive deduction behavior.
Effect on original feature: Valid C++ 2014 code may fail to compile or change meaning in this International Standard. For example:

```cpp
auto x(1);    // was std::initializer_list<int>; now int
auto x(2);    // was std::initializer_list<int>; now ill-formed
```

## C.4.4 Clause 11: declarators

Change: Make exception specifications specify by the type of system.
Rationale: Improve type-safety.
Effect on original feature: Valid C++ 2014 code may fail to compile or change meaning in this International Standard.

```cpp
void g() noexcept;
void g();
template<class T> int f(T *, T);
int i = f(g1, g2);    // ill-formed; previously well-formed
```

Change: Definition of an aggregate is extended to apply to user-defined types with base classes.
Rationale: Improve convenience of aggregate initialization.
Effect on original feature: Valid C++ 2014 code may fail to compile or produce different results in this International Standard; initialization from an empty initializer list will perform aggregate initialization instead of invoking a default constructor for the affected types:

```cpp
struct derived {
  struct base {
    friend struct derived;
  private:
    base();
  };
  struct derived : base {};
};

derived d1; // error: the code was well-formed in C++ 2014
derived d2; // still OK
```

## C.4.5 Clause 15: special member functions [diff.cpp14.special]

### 15.6.3

Change: Inheriting a constructor no longer injects a constructor into the derived class.
Rationale: Better interaction with other language features.
Effect on original feature: Valid C++ 2014 code that uses inheriting constructors may not be valid or may have different semantics. A using-declaration that names a constructor now makes the corresponding base class visible to initializations of the derived class rather declaring additional derived class constructors.

```cpp
struct A {
  template<typename T> A(T, typename T::type = 0);
  A(int);
};
struct B : A {
  using A::A;
  B(int);
};
B b(42L); // calls B(int), used to call B<long>(long)
 // which calls A(int) due to substitution failure
 // in A<long>(long)
```

## C.4.6 Clause 17: templates [diff.cpp14.temp]

### 17.8.2.5

Change: Allowance to deduce from the type of a non-type template argument allows partial specialization to deduce the type template argument.
Effect on original feature: Valid C++ 2014 code may fail to compile or produce different results in International Standard:

```cpp
template<int N> struct A;
template<typename T, int N> int foo(A<N>) = delete;
void foo(void*);
void bar(A<0>*) {
  foo(0); // ill-formed; previously well-formed
}
```

## C.4.7 Clause 18: exception handling [diff.cpp14.except]

### 18.4

Change: Remove dynamic exception specifications.
Rationale: Dynamic exceptions were a deprecated feature that was complex and brittle in use. They interacted badly with the type system, which became a more significant issue in this International Standard where (non-dynamic) exception specifications are of the.
Effect on original feature: Valid C++ 2014 code using these identifiers may be ill-formed in this International Standard.

## C.4.8 Clause 20: library [diff.cpp14.library]

### 20.5.1

Change: New features.
Rationale: New functionality.
Effect on original feature: Valid C++ 2014 code may fail to compile or produce different results in International Standard. The following are new: <any>, <execution>, <filesystem>, <optional>, <variant>.

### 20.5.4

Change: New namespaces.
Rationale: By standardization.
Effect on original feature: Valid C++ 2014 code may fail to compile or change meaning in this International Standard.

## C.4.9 Clause 23: general utilities [diff.cpp14.utilities]

### 23.1.4

Change: Removing allocators.
Rationale: By standardization.
Effect on original feature: Valid C++ 2014 code may fail to compile or change meaning in this International Standard.

### 23.11.2

Change: Array support.
Rationale: By new features.
Effect on original feature: Valid C++ 2014 code may fail to compile or produce different results in this International Standard.

## C.4.10 Clause 24: string [diff.cpp14.string]

### 24.3.2

Change: Non-const member added.
Rationale: By standardization.
Effect on original feature: Valid C++ 2014 code may fail to compile or produce different results in this International Standard.

## C.4.11 Clause 26: containers [diff.cpp14.containers]

### 26.2.6

Change: Requirements change.
Rationale: Increase portability, classification of associative container.
Effect on original feature: Valid C++ 2014 code that attempts to use associative containers having a comparison object with non-const function operator may fail to compile in this International Standard.

## C.4.12 Annex D: compatibility features [diff.cpp14.dep]

Change: The class templates auto_ptr, unary_function, and binary_function, the function templates random_shuffle, and the templates (and their return types) ptr_fun, mem_fun, mem_fun_ref, bindist, Superseded by bindnd are not defined.
Rationale: By new features.
Effect on original feature: Valid C++ 2014 code that uses these class templates and function templates may fail to compile in this International Standard.

Change: Remove old istreams members [dep.ios.members].
Rationale: Redundant feature for pre-standard code has served its time.
Effect on original feature: A valid C++ 2014 program using these identifiers may be ill-formed in this International Standard.

# C.5 C standard library [diff.library]

This subclass summarizes the explicit changes in headers, definitions, declarations, or behavior between the C standard library and the parts of the C++ standard library that were included from the C standard library.

## C.5.1 Modifications to headers [diff.mods.to.headers]

- For compatibility with the C standard library, the C++ standard library provides the C headers enumerated in D.5, but their use is deprecated in C++.

- There are no C headers for the C headers <atomic.h>, <stdnore.h>, and <threads.h>, nor are the C headers themselves part of C++.
