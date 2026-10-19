

overload FUN(Tj) selected by overload resolution for the expression FUN(std::forward<T>(t)) defines the alternative Tj which is the type of the contained value after assignment.

## Constraints:

+   - is_same_v<remove_cvref_t<T>, variant> is false,
+   - is_assignable_v<Tj&, T> && is_constructible_v<Tj, T> is true, and
+   - the expression FUN(std::forward<T>(t)) (with FUN being the above-mentioned set of imaginary functions) is well-formed.

> [Note 1:
>     variant<string, string> v;
>     v = "abc";
>     is ill-formed, as both alternative types have an equally viable constructor for the argument. — end note]

## Effects:

+   - If *this holds a Tj, assigns std::forward<T>(t) to the value contained in *this.
+   - Otherwise, if is_nothrow_constructible_v<Tj, T> || !is_nothrow_move_constructible_v<Tj> is true, equivalent to emplace<j>(std::forward<T>(t)).
+   - Otherwise, equivalent to operator=(variant(std::forward<T>(t))).

Postconditions: holds_alternative<Tj>(*this) is true, with Tj selected by the imaginary function overload resolution described above.

Returns: *this.

## Remarks: The expression inside noexcept is equivalent to:

```
is_nothrow_assignable_v<Tj&, T> && is_nothrow_constructible_v<Tj, T>
```

+   - If an exception is thrown during the assignment of std::forward<T>(t) to the value contained in *this, the state of the contained value and t are as defined by the exception safety guarantee of the assignment expression; valueless_by_exception() will be false.
+   - If an exception is thrown during the initialization of the contained value, the variant object is permitted to not hold a value.

## 20.7.3.5 Modifiers [variant.mod]

```
template<class T, class... Args> T& emplace(Args&&... args);
```

Constraints: is_constructible_v<T, Args...> is true, and T occurs exactly once in Types.

Effects: Equivalent to:

```
return emplace<I>(std::forward<Args>(args)...);
```

where I is the zero-based index of T in Types.

```
template<class T, class U, class... Args> T& emplace(initializer_list<U> il, Args&&... args);
```

Constraints: is_constructible_v<T, initializer_list<U>&, Args...> is true, and T occurs exactly once in Types.

Effects: Equivalent to:

```
return emplace<I>(il, std::forward<Args>(args)...);
```

where I is the zero-based index of T in Types.

```
template<size_t I, class... Args>
variant_alternative_t<I, variant<Types...>>& emplace(Args&&... args);
```

Mandates: I < sizeof...(Types).

Constraints: is_constructible_v<TI, Args...> is true.

Effects: Destroys the currently contained value if valueless_by_exception() is false. Then initializes the contained value as if direct-non-list-initializing a value of type TI with the arguments std::forward<Args>(args)...

Postconditions: index() is I.

# ISO/IEC 14882:2020(E)

```
if (v.valueless_by_exception()) return strong_ordering::less;
if (w.valueless_by_exception()) return strong_ordering::greater;
if (auto c = v.index() <=> w.index(); c != 0) return c;
return get<i>(v) <=> get<i>(w);
```

with i being v.index().

## 20.7.7 Visitation [variant.visit]

```
template<class Visitor, class... Variants>
constexpr see below visit(Visitor&& vis, Variants&&... vars);
template<class R, class Visitor, class... Variants>
constexpr R visit(Visitor&& vis, Variants&&... vars);
```

Let n be sizeof...(Variants). Let m be a pack of n values of type size_t. Such a pack is called valid if 0 ≤ m_i < variant_size_v<remove_reference_t<Variants_i>> for all 0 ≤ i < n. For each valid pack m, let e(m) denote the expression:

```
INVOKE(std::forward<Visitor>(vis), get<m>(std::forward<Variants>(vars))...) // see 20.14.4
```

for the first form and

```
INVOKE<R>(std::forward<Visitor>(vis), get<m>(std::forward<Variants>(vars))...) // see 20.14.4
```

for the second form.

Mandates: For each valid pack m, e(m) is a valid expression. All such expressions are of the same type and value category.

Returns: e(m), where m is the pack for which m_i is vars_i.index() for all 0 ≤ i < n. The return type is decltype(e(m)) for the first form.

Throws: bad_variant_access if any variant in vars is valueless_by_exception().

Complexity: For n ≤ 1, the invocation of the callable object is implemented in constant time, i.e., for n = 1, it does not depend on the number of alternative types of Variants_0. For n > 1, the invocation of the callable object has no complexity requirements.

## 20.7.8 Class monostate [variant.monostate]

```
struct monostate{};
```

The class monostate can serve as a first alternative type for a variant to make the variant type default constructible.

## 20.7.9 monostate relational operators [variant.monostate.relops]

```
constexpr bool operator==(monostate, monostate) noexcept { return true; }
constexpr strong_ordering operator<=>(monostate, monostate) noexcept
{ return strong_ordering::equal; }
```

[Note 1: monostate objects have only a single state; they thus always compare equal. — end note]

## 20.7.10 Specialized algorithms [variant.specialg]

```
template<class... Types>
void swap(variant<Types...>& v, variant<Types...>& w) noexcept(see below);
```

Constraints: is_move_constructible_v<T_i> && is_swappable_v<T_i> is true for all i.

Effects: Equivalent to v.swap(w).

Remarks: The expression inside noexcept is equivalent to noexcept(v.swap(w)).

## 20.7.11 Class bad_variant_access [variant.bad.access]

```
class bad_variant_access : public exception {
public:
// see 17.9.3 for the specification of the special member functions
const char* what() const noexcept override;
};
```

1 Objects of type bad_variant_access are thrown to report invalid accesses to the value of a variant object.

```
const char* what() const noexcept override;
```

2 Returns: An implementation-defined NTBS.

## 20.7.12 Hash support [variant.hash]

```
template<class... Types> struct hash<variant<Types...>>;
```

1 The specialization hash<variant<Types...>> is enabled (20.14.19) if and only if every specialization in hash<remove_const_t<Types>>... is enabled. The member functions are not guaranteed to be noexcept.

```
template<> struct hash<monostate>;
```

2 The specialization is enabled (20.14.19).

## 20.8 Storage for any type [any]

## 20.8.1 General [any.general]

1 Subclause 20.8 describes components that C++ programs may use to perform operations on objects of a discriminated type.

2 [Note 1: The discriminated type can contain values of different types but does not attempt conversion between them, i.e., 5 is held strictly as an int and is not implicitly convertible either to "5" or to 5.0. This indifference to interpretation but awareness of type effectively allows safe, generic containers of single values, with no scope for surprises from ambiguous conversions. — end note]

## 20.8.2 Header <any> synopsis [any.synop]

```
namespace std {
  // 20.8.3, class bad_any_cast
  class bad_any_cast;

  // 20.8.4, class any
  class any;

  // 20.8.5, non-member functions
  void swap(any& x, any& y) noexcept;

  template<class T, class... Args>
    any make_any(Args&&... args);
  template<class T, class U, class... Args>
    any make_any(initializer_list<U> il, Args&&... args);

  template<class T>
    T any_cast(any& operand);
  template<class T>
    T any_cast(const any& operand);
  template<class T>
    T any_cast(any&& operand);

  template<class T>
    const T* any_cast(const any* operand) noexcept;
  template<class T>
    T* any_cast(any* operand) noexcept;
}
```

## 20.8.3 Class bad_any_cast [any.bad.any.cast]

```
class bad_any_cast : public bad_cast {
public:
  // see 17.9.3 for the specification of the special member functions
  const char* what() const noexcept override;
};
```

# ISO/IEC 14882:2020(E)

```
any(const any& other);
```

Effects: If other.has_value() is false, constructs an object that has no value. Otherwise, equivalent to any(in_place_type<T>, any_cast<const T&>(other)) where T is the type of the contained value.

Throws: Any exceptions arising from calling the selected constructor for the contained value.

```
any(any&& other) noexcept;
```

Effects: If other.has_value() is false, constructs an object that has no value. Otherwise, constructs an object of type any that contains either the contained value of other, or contains an object of the same type constructed from the contained value of other considering that contained value as an rvalue.

```
template<class T>
    any(T&& value);
```

Let VT be decay_t<T>.

Constraints: VT is not the same type as any, VT is not a specialization of in_place_type_t, and is_copy_constructible_v<VT> is true.

Preconditions: VT meets the Cpp17CopyConstructible requirements.

Effects: Constructs an object of type any that contains an object of type VT direct-initialized with std::forward<T>(value).

Throws: Any exception thrown by the selected constructor of VT.

```
template<class T, class... Args>
    explicit any(in_place_type_t<T>, Args&&... args);
```

Let VT be decay_t<T>.

Constraints: is_copy_constructible_v<VT> is true and is_constructible_v<VT, Args...> is true.

Preconditions: VT meets the Cpp17CopyConstructible requirements.

Effects: Initializes the contained value as if direct-non-list-initializing an object of type VT with the arguments std::forward<Args>(args)...

Postconditions: *this contains a value of type VT.

Throws: Any exception thrown by the selected constructor of VT.

```
template<class T, class U, class... Args>
    explicit any(in_place_type_t<T>, initializer_list<U> il, Args&&... args);
```

Let VT be decay_t<T>.

Constraints: is_copy_constructible_v<VT> is true and is_constructible_v<VT, initializer_list<U>&, Args...> is true.

Preconditions: VT meets the Cpp17CopyConstructible requirements.

Effects: Initializes the contained value as if direct-non-list-initializing an object of type VT with the arguments il, std::forward<Args>(args)...

Postconditions: *this contains a value.

Throws: Any exception thrown by the selected constructor of VT.

```
~any();
```

Effects: As if by reset().

## 20.8.4.3 Assignment [any.assign]

```
any& operator=(const any& rhs);
```

