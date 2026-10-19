
## 20.14.17.2 Class bad_function_call [func.wrap.badcall]

1 An exception of type bad_function_call is thrown by function::operator() (20.14.17.3.5) when the function wrapper object has no target.

``` 
namespace std {
  class bad_function_call : public exception {
  public:
    // see 17.9.3 for the specification of the special member functions
    const char* what() const noexcept override;
  };
}
```

``` 
const char* what() const noexcept override;
```

2 Returns: An implementation-defined NTBS.

## 20.14.17.3 Class template function [func.wrap.func]

### 20.14.17.3.1 General [func.wrap.func.general]

``` 
namespace std {
  template<class> class function;      // not defined

  template<class R, class... ArgTypes>
  class function<R(ArgTypes...)> {
  public:
    using result_type = R;

    // 20.14.17.3.2, construct/copy/destroy
    function() noexcept;
    function(nullptr_t) noexcept;
    function(const function&);
    function(function&&) noexcept;
    template<class F> function(F);

    function& operator=(const function&);
    function& operator=(function&&);
    function& operator=(nullptr_t) noexcept;
    template<class F> function& operator=(F&&);
    template<class F> function& operator=(reference_wrapper<F>) noexcept;

    ~function();

    // 20.14.17.3.3, function modifiers
    void swap(function&) noexcept;

    // 20.14.17.3.4, function capacity
    explicit operator bool() const noexcept;

    // 20.14.17.3.5, function invocation
    R operator()(ArgTypes...) const;

    // 20.14.17.3.6, function target access
    const type_info& target_type() const noexcept;
    template<class T> T* target() noexcept;
    template<class T> const T* target() const noexcept;
  };

  template<class R, class... ArgTypes>
    function(R(*)(ArgTypes...)) -> function<R(ArgTypes...)>;

  template<class F> function(F) -> function<see below>;

  // 20.14.17.3.7, null pointer comparison operator functions
  template<class R, class... ArgTypes>
    bool operator==(const function<R(ArgTypes...)>&, nullptr_t) noexcept;

  // 20.14.17.3.8, specialized algorithms
  template<class R, class... ArgTypes>
    void swap(function<R(ArgTypes...)>&, function<R(ArgTypes...)>&) noexcept;
}
```

1 The function class template provides polymorphic wrappers that generalize the notion of a function pointer. Wrappers can store, copy, and call arbitrary callable objects (20.14.3), given a call signature (20.14.3), allowing functions to be first-class objects.

2 A callable type (20.14.3) F is Lvalue-Callable for argument types ArgTypes and return type R if the expression `INVOKE<R>(declval<F&>(), declval<ArgTypes>()...)`, considered as an unevaluated operand (7.2), is well-formed (20.14.4).

3 The function class template is a call wrapper (20.14.3) whose call signature (20.14.3) is R(ArgTypes...).

4 [Note 1: The types deduced by the deduction guides for function have been identified as candidates for being changed in a future revision of C++. — end note]

### 20.14.17.3.2 Constructors and destructor [func.wrap.func.con]

``` 
function() noexcept;
```

1 Postconditions: !*this.

``` 
function(nullptr_t) noexcept;
```

2 Postconditions: !*this.

``` 
function(const function& f);
```

3 Postconditions: !*this if !f; otherwise, *this targets a copy of f.target().

4 Throws: Nothing if f's target is a specialization of reference_wrapper or a function pointer. Otherwise, may throw bad_alloc or any exception thrown by the copy constructor of the stored callable object.

5 Recommended practice: Implementations should avoid the use of dynamically allocated memory for small callable objects, for example, where f's target is an object holding only a pointer or reference to an object and a member function pointer.

``` 
function(function&& f) noexcept;
```

## 20.14.18.3 Class template boyer_moore_searcher [func.search.bm]

``` 
constexpr default_searcher(ForwardIterator1 pat_first, ForwardIterator1 pat_last, BinaryPredicate pred = BinaryPredicate());
```

Effects: Constructs a default_searcher object, initializing pat_first_ with pat_first, pat_last_ with pat_last, and pred_ with pred.

Throws: Any exception thrown by the copy constructor of BinaryPredicate or ForwardIterator1.

``` 
template<class ForwardIterator2>
constexpr pair<ForwardIterator2, ForwardIterator2>
operator()(ForwardIterator2 first, ForwardIterator2 last) const;
```

Effects: Returns a pair of iterators i and j such that

- i == search(first, last, pat_first_, pat_last_, pred_), and
- if i == last, then j == last, otherwise j == next(i, distance(pat_first_, pat_last_)).

``` 
template<class RandomAccessIterator1,
class Hash = hash<typename iterator_traits<RandomAccessIterator1>::value_type>,
class BinaryPredicate = equal_to<>>
class boyer_moore_searcher {
public:
boyer_moore_searcher(RandomAccessIterator1 pat_first,
RandomAccessIterator1 pat_last,
Hash hf = Hash(),
BinaryPredicate pred = BinaryPredicate());
template<class RandomAccessIterator2>
pair<RandomAccessIterator2, RandomAccessIterator2>
operator()(RandomAccessIterator2 first, RandomAccessIterator2 last) const;
private:
RandomAccessIterator1 pat_first_; // exposition only
RandomAccessIterator1 pat_last_; // exposition only
Hash hash_; // exposition only
BinaryPredicate pred_; // exposition only
};
```

``` 
boyer_moore_searcher(RandomAccessIterator1 pat_first,
RandomAccessIterator1 pat_last,
Hash hf = Hash(),
BinaryPredicate pred = BinaryPredicate());
```

Preconditions: The value type of RandomAccessIterator1 meets the Cpp17DefaultConstructible requirements, the Cpp17CopyConstructible requirements, and the Cpp17CopyAssignable requirements.

Preconditions: Let V be `iterator_traits<RandomAccessIterator1>::value_type`. For any two values A and B of type V, if pred(A, B) == true, then hf(A) == hf(B) is true.

Effects: Initializes pat_first_ with pat_first, pat_last_ with pat_last, hash_ with hf, and pred_ with pred.

Throws: Any exception thrown by the copy constructor of RandomAccessIterator1, or by the default constructor, copy constructor, or the copy assignment operator of the value type of RandomAccessIterator1, or the copy constructor or operator() of BinaryPredicate or Hash. May throw bad_alloc if additional memory needed for internal data structures cannot be allocated.

``` 
template<class RandomAccessIterator2>
pair<RandomAccessIterator2, RandomAccessIterator2>
operator()(RandomAccessIterator2 first, RandomAccessIterator2 last) const;
```

Mandates: RandomAccessIterator1 and RandomAccessIterator2 have the same value type.

Effects: Finds a subsequence of equal values in a sequence.

Returns: A pair of iterators i and j such that

``` 
// 20.15.8.7, other transformations
template<class T> struct type_identity;
template<size_t Len, size_t Align = default-alignment> // see 20.15.8.7
    struct aligned_storage;
template<size_t Len, class... Types> struct aligned_union;
template<class T> struct remove_cvref;
template<class T> struct decay;
template<bool, class T = void> struct enable_if;
template<bool, class T, class F> struct conditional;
template<class... T> struct common_type;
template<class T, class U, template<class> class TQual, template<class> class UQual>
    struct basic_common_reference { };
template<class... T> struct common_reference;
template<class T> struct underlying_type;
template<class Fn, class... ArgTypes> struct invoke_result;
template<class T> struct unwrap_reference;
template<class T> struct unwrap_ref_decay;

template<class T>
    using type_identity_t      = typename type_identity<T>::type;
template<size_t Len, size_t Align = default-alignment> // see 20.15.8.7
    using aligned_storage_t    = typename aligned_storage<Len, Align>::type;
template<size_t Len, class... Types>
    using aligned_union_t      = typename aligned_union<Len, Types...>::type;
template<class T>
    using remove_cvref_t       = typename remove_cvref<T>::type;
template<class T>
    using decay_t              = typename decay<T>::type;
template<bool b, class T = void>
    using enable_if_t          = typename enable_if<b, T>::type;
template<bool b, class T, class F>
    using conditional_t        = typename conditional<b, T, F>::type;
template<class... T>
    using common_type_t        = typename common_type<T...>::type;
template<class... T>
    using common_reference_t = typename common_reference<T...>::type;
template<class T>
    using underlying_type_t    = typename underlying_type<T>::type;
template<class Fn, class... ArgTypes>
    using invoke_result_t      = typename invoke_result<Fn, ArgTypes...>::type;
template<class T>
    using unwrap_reference_t = typename unwrap_reference<T>::type;
template<class T>
    using unwrap_ref_decay_t = typename unwrap_ref_decay<T>::type;
template<class...>
    using void_t               = void;

// 20.15.9, logical operator traits
template<class... B> struct conjunction;
template<class... B> struct disjunction;
template<class B> struct negation;

// 20.15.5.2, primary type categories
template<class T>
    inline constexpr bool is_void_v = is_void<T>::value;
template<class T>
    inline constexpr bool is_null_pointer_v = is_null_pointer<T>::value;
template<class T>
    inline constexpr bool is_integral_v = is_integral<T>::value;
template<class T>
    inline constexpr bool is_floating_point_v = is_floating_point<T>::value;
template<class T>
    inline constexpr bool is_array_v = is_array<T>::value;
```
