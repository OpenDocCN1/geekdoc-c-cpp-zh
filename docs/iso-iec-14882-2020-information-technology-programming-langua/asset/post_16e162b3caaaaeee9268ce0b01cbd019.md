
// assignment
unique_ptr& operator=(unique_ptr&& u) noexcept;
template<class U, class E>
    unique_ptr& operator=(unique_ptr<U, E>&& u) noexcept;
unique_ptr& operator=(nullptr_t) noexcept;

// 20.11.1.4.4, observers
T& operator[](size_t i) const;
pointer get() const noexcept;
deleter_type& get_deleter() noexcept;
const deleter_type& get_deleter() const noexcept;
explicit operator bool() const noexcept;

// 20.11.1.4.5, modifiers
pointer release() noexcept;
template<class U> void reset(U p) noexcept;
void reset(nullptr_t = nullptr) noexcept;
void swap(unique_ptr& u) noexcept;

// disable copy from lvalue
unique_ptr(const unique_ptr&) = delete;
unique_ptr& operator=(const unique_ptr&) = delete;
};

1 A specialization for array types is provided with a slightly altered interface.

- (1.1) — Conversions between different types of unique_ptr<T[], D> that would be disallowed for the corresponding pointer-to-array types, and conversions to or from the non-array forms of unique_ptr, produce an ill-formed program.
- (1.2) — Pointers to types derived from T are rejected by the constructors, and by reset.
- (1.3) — The observers operator* and operator-> are not provided.
- (1.4) — The indexing observer operator[] is provided.
- (1.5) — The default deleter will call delete[].

2 Descriptions are provided below only for members that differ from the primary template.

3 The template argument T shall be a complete type.

## 20.11.1.4.2 Constructors [unique.ptr.runtime.ctor]

```
template<class U> explicit unique_ptr(U p) noexcept;
```

1 This constructor behaves the same as the constructor in the primary template that takes a single parameter of type pointer.

2 Constraints:
- (2.1) — U is the same type as pointer, or
- (2.2) — pointer is the same type as element_type*, U is a pointer type V*, and V(*) [] is convertible to element_type(*) [].

```
template<class U> unique_ptr(U p, see below d) noexcept;
template<class U> unique_ptr(U p, see below d) noexcept;
```

3 These constructors behave the same as the constructors in the primary template that take a parameter of type pointer and a second parameter.

4 Constraints:
- (4.1) — U is the same type as pointer,
- (4.2) — U is nullptr_t, or
- (4.3) — pointer is the same type as element_type*, U is a pointer type V*, and V(*) [] is convertible to element_type(*) [].

## 20.11.1.7 I/O [unique.ptr.io]

```
template<class E, class T, class Y, class D>
  basic_ostream<E, T>& operator<<(basic_ostream<E, T>& os, const unique_ptr<Y, D>& p);
```

Constraints: os << p.get() is a valid expression.

Effects: Equivalent to: os << p.get();

Returns: os.

## 20.11.2 Class bad_weak_ptr [util.smartptr.weak.bad]

```
namespace std {
class bad_weak_ptr : public exception {
public:
  // see 17.9.3 for the specification of the special member functions
  const char* what() const noexcept override;
};
}
```

An exception of type bad_weak_ptr is thrown by the shared_ptr constructor taking a weak_ptr.

```
const char* what() const noexcept override;
```

Returns: An implementation-defined NTBS.

Preconditions: The specialization less<unique_ptr<T, D>::pointer> is a function object type (20.14) that induces a strict weak ordering (25.8) on the pointer values.

Returns: The first function template returns
less<unique_ptr<T, D>::pointer>()(x.get(), nullptr)
The second function template returns
less<unique_ptr<T, D>::pointer>()(nullptr, x.get())

```
template<class T, class D>
  bool operator<(const unique_ptr<T, D>& x, nullptr_t);
template<class T, class D>
  bool operator<(nullptr_t, const unique_ptr<T, D>& x);
```

## 20.11.3 Class template shared_ptr [util.smartptr.shared]

## 20.11.3.1 General [util.smartptr.shared.general]

1 The shared_ptr class template stores a pointer, usually obtained via new. shared_ptr implements semantics of shared ownership; the last remaining owner of the pointer is responsible for destroying the object, or otherwise releasing the resources associated with the stored pointer. A shared_ptr is said to be empty if it does not own a pointer.

```
namespace std {
  template<class T> class shared_ptr {
  public:
    using element_type = remove_extent_t<T>;
    using weak_type    = weak_ptr<T>;

    // 20.11.3.2, constructors
    constexpr shared_ptr() noexcept;
    constexpr shared_ptr(nullptr_t) noexcept : shared_ptr() { }
    template<class Y>
      explicit shared_ptr(Y* p);
    template<class Y, class D>
      shared_ptr(Y* p, D d);
    template<class Y, class D, class A>
      shared_ptr(Y* p, D d, A a);
    template<class D>
      shared_ptr(nullptr_t p, D d);
    template<class D, class A>
      shared_ptr(nullptr_t p, D d, A a);
    template<class Y>
      shared_ptr(const shared_ptr<Y>& r, element_type* p) noexcept;
    template<class Y>
      shared_ptr(shared_ptr<Y>&& r, element_type* p) noexcept;
    shared_ptr(const shared_ptr& r) noexcept;
    template<class Y>
      shared_ptr(const shared_ptr<Y>& r) noexcept;
    shared_ptr(shared_ptr&& r) noexcept;
    template<class Y>
      shared_ptr(shared_ptr<Y>&& r) noexcept;
    template<class Y>
      explicit shared_ptr(const weak_ptr<Y>& r);
    template<class Y, class D>
      shared_ptr(unique_ptr<Y, D>&& r);

    // 20.11.3.3, destructor
    ~shared_ptr();

    // 20.11.3.4, assignment
    shared_ptr& operator=(const shared_ptr& r) noexcept;
    template<class Y>
      shared_ptr& operator=(const shared_ptr<Y>& r) noexcept;
    shared_ptr& operator=(shared_ptr&& r) noexcept;
    template<class Y>
      shared_ptr& operator=(shared_ptr<Y>&& r) noexcept;
    template<class Y, class D>
      shared_ptr& operator=(unique_ptr<Y, D>&& r);

    // 20.11.3.5, modifiers
    void swap(shared_ptr& r) noexcept;
    void reset() noexcept;
    template<class Y>
      void reset(Y* p);
    template<class Y, class D>
      void reset(Y* p, D d);
    template<class Y, class D, class A>
      void reset(Y* p, D d, A a);
```

## 20.11.3.2 Constructors [util.smartptr.shared.const]

// 20.11.3.6, observers
element_type* get() const noexcept;
T& operator*() const noexcept;
T* operator->() const noexcept;
element_type& operator[](ptrdiff_t i) const;
long use_count() const noexcept;
explicit operator bool() const noexcept;
template<class U>
  bool owner_before(const shared_ptr<U>& b) const noexcept;
template<class U>
  bool owner_before(const weak_ptr<U>& b) const noexcept;
};

```
template<class T>
  shared_ptr(weak_ptr<T>) -> shared_ptr<T>;
template<class T, class D>
  shared_ptr(unique_ptr<T, D>) -> shared_ptr<T>;
}
```

2 Specializations of shared_ptr shall be Cpp17CopyConstructible, Cpp17CopyAssignable, and Cpp17LessThanComparable, allowing their use in standard containers. Specializations of shared_ptr shall be contextually convertible to bool, allowing their use in boolean expressions and declarations in conditions.

3 The template parameter T of shared_ptr may be an incomplete type.
[Note 1: T can be a function type. — end note]

4 [Example 1:
if (shared_ptr<X> px = dynamic_pointer_cast<X>(py)) {
// do something with px
}
— end example]

5 For purposes of determining the presence of a data race, member functions shall access and modify only the shared_ptr and weak_ptr objects themselves and not objects they refer to. Changes in use_count() do not reflect modifications that can introduce data races.

6 For the purposes of subclause 20.11, a pointer type Y* is said to be compatible with a pointer type T* when either Y* is convertible to T* or Y is U[N] and T is cv U[].

1 In the constructor definitions below, enables shared_from_this with p, for a pointer p of type Y*, means that if Y has an unambiguous and accessible base class that is a specialization of enable_shared_from_this (20.11.6), then remove_cv_t<Y>* shall be implicitly convertible to T* and the constructor evaluates the statement:
if (p != nullptr && p->weak_this.expired())
  p->weak_this = shared_ptr<remove_cv_t<Y>>(*this, const_cast<remove_cv_t<Y>*>(p));
The assignment to the weak_this member is not atomic and conflicts with any potentially concurrent access to the same object (6.9.2).

```
constexpr shared_ptr() noexcept;
```

2 Postconditions: use_count() == 0 && get() == nullptr.

```
template<class Y> explicit shared_ptr(Y* p);
```

3 Mandates: Y is a complete type.

4 Constraints: When T is an array type, the expression delete[] p is well-formed and either T is U[N] and Y(*)[N] is convertible to T*, or T is U[] and Y(*)[ ] is convertible to T*. When T is not an array type, the expression delete p is well-formed and Y* is convertible to T*.

5 Preconditions: The expression delete[] p, when T is an array type, or delete p, when T is not an array type, has well-defined behavior, and does not throw exceptions.

6 Effects: When T is not an array type, constructs a shared_ptr object that owns the pointer p. Otherwise, constructs a shared_ptr that owns p and a deleter of an unspecified type that calls delete[] p. When
