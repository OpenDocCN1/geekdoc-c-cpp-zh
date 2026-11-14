

To relieve us from typing typename and ::type when referring to the resulting type, C++14 introduces a template alias:

```
template <bool b, class T, class F>
using conditional_t = typename conditional<b, T, F>::type;
```

If the standard library of your compiler does not provide this alias, you can quickly add it—maybe with a different name or in another namespace to avoid name conflicts later on.

## 5.2.3.5 The Final View

Now we have all we need to revise the view from Listing 5-1. The problem was that we returned an entry of a constant matrix as a mutable reference. To avoid this, we can try to make the mutable access operator disappear in the view when the referred matrix is const. This is possible but more complicated. We will come back to this approach in Section 5.2.6.

An easier solution is to keep both the mutable and the constant access operator but choose the return type of the former depending on the type of the template argument:

### Listing 5-3: const-safe view implementation

```
template <typename Matrix>
class transposed_view
{
public:
    using value_type = Collection<Matrix>::value_type;
    using size_type = Collection<Matrix>::size_type;
private:
    using vref_type = conditional_t<is_const<Matrix>::type,
                                    const value_type&,
                                    value_type&>;
public:
    transposed_view(Matrix& A) : ref(A) {}
    vref_type operator()(size_type r, size_type c)
    { return ref(c, r); }
    const value_type& operator()(size_type r, size_type c) const
    { return ref(c, r); }
private:
    Matrix& ref;
};
```

This implementation differentiates the return type of mutable views between constant and mutable referred matrices. This establishes the desired behavior as the following case study will show.

When the referred matrix is mutable, the return type of operator() depends on the constancy of the view object:

- If the view object is mutable, then operator() in line 14 returns a mutable reference (line 10); and
- If the view object is constant, then operator() in line 17 returns a constant reference.

This is the same behavior as in Listing 5-1.

If the referred matrix is constant, then a constant reference is always returned:

- If the view object is mutable, then operator() in line 14 returns a constant reference (line 9); and
- If the view object is constant, then operator() in line 17 returns a constant reference.

Altogether, we implemented a view class that supplies write access only when the view object and the referred matrix are both mutable.

## 5.2.4 Standard Type Traits

Note: The type traits in the standard library originate from the Boost library collection. If you are moving from the Boost type traits to those of the standard, be aware that some names are different. There are also slight differences in the behavior: whereas meta-functions in Boost expect a type and implicitly read its boolean value implicitly, the meta-function with the same name in the standard expects a boolean value as an argument. Whenever possible prefer the standard type traits sketched in Section 4.3.

## 5.2.5 Domain-Specific Type Properties

Now that we have seen how the type traits in the standard library are realized, we can use this knowledge for ourselves and realize domain-specific type properties. Not surprisingly, we pick linear algebra as the domain and implement the property is_matrix. To be on the safe side, a type is only considered as a matrix when we explicitly declare it as such. Thus, types are by default declared as not being a matrix:

```
template <typename T>
struct is_matrix
{
    static const bool value = false;
};
```

The standard library supplies a false_type containing just this static constant.4 We can save ourselves some typing by deriving from this meta-function and inheriting (See Chapter 6) value from false_type:

```
template <typename T>
struct is_matrix
    : std::false_type
{};
```

4. In C++03 you can resort to boost::mpl::false_.

Now we specialize the meta-predicate for all known matrix classes:

```
template <typename Value, typename Para>
struct is_matrix<mtl::dense2D<Value, Para> >
    : std::true_type
{};
// more matrix classes ...
```

The predicate can also depend on the template arguments. For instance, we might have a transposed_view class applicable to matrices and vectors (certainly tricky to implement but this is a different question). Certainly, a transposed vector is not a matrix whereas a transposed matrix is:

```
template <typename Matrix>
struct is_matrix<transposed_view<Matrix> >
    : is_matrix<Matrix>
{};
// more views ...
```

More likely, we will realize separate views for transposing matrices and vectors, e.g.:

```
template <typename Matrix>
struct is_matrix<matrix::transposed_view<Matrix> >
    : std::true_type
{};
```

To ascertain that our view is used correctly, we verify with static_assert that the template argument is a (known) matrix:

```
template <typename Matrix>
class transposed_view
{
    static_assert(is_matrix<Matrix>::value,
                  "Argument of this view must be a matrix!");
    // ...
};
```

If the view is instantiated with a type that is not a matrix (or not declared as such), the compilation aborts and the user-defined error message is printed. Since static_assert does not create run-time overhead, it should be used wherever errors can be detected at the type level or regarding compile-time constants. Up to C++14, the error message must be a literal. Later C++ versions will probably allow us to compose messages with type information.

When we try to compile our test with the static assertion, we will see that trans(A) compiles but not trans(B). The reason is that const dense2D<> is considered different from dense2D<> in template specialization so it is still not considered a matrix. The good news is that we do not need to double our specializations for mutable and constant types, but we can write a partial specialization for all constant arguments:

```
template <typename T>
struct is_matrix<const T>
    : is_matrix<T> {};
```

Thus, whenever a type T is a matrix, then const T is as well.

## 5.2.6 enable_if

A very powerful mechanism for meta-programming is `enable_if`, discovered by Jaakko Järvi and Jeremy Walcock. It is based on a convention for compiling function templates called SFINAE: **Substitution Failure Is Not An Error**. It means that function templates whose header cannot be substituted with the argument types are just ignored and do not cause an error.

Such substitution errors can happen when the `return` type of a function is a meta-function on a template argument, e.g.:

```
template <typename T>
typename Magnitude<T>::type
inline min_abs(const T& x, const T& y)
{
    using std::abs;
    auto ax = abs(x), ay = abs(y);
    return ax < ay ? ax : ay;
}
```

Here our `return` type is the `Magnitude` of `T`. When `Magnitude<T>` contains no member type for the type of `x` and `y`, the substitution fails and the function template is ignored. The benefit of this approach is that a function call can be compiled when for multiple overloads exactly one of them can be successfully substituted. Or when multiple function templates can be substituted and one of them is more specific than all others. This mechanism is exploited in `enable_if`.

Here we will use `enable_if` to select function templates based on domain-specific properties. As a showcase, we realize the $L_1$ norm. It is defined for vector spaces and linear operators (matrices). Although these definitions are related, the practical real-world implementation for finite-dimensional vectors and matrices is different enough to justify multiple implementations. Of course, we could implement $L_1$ norm for every matrix and vector type so that the call `one_norm(x)` would select the appropriate implementation for this type.

=> c++03/enable_if.test.cpp

To be more productive, we like to have one single implementation for all matrix types (including views) and one single implementation for all vector types. We use the meta-function `is_matrix` and implement `is_vector` accordingly. Further, we need the meta-function `Magnitude` to handle the magnitude of complex matrices and vectors. For convenience, we further provide a template alias `Magnitude_t` to access contained type information.

Next, we implement the meta-function `enable_if` that allows us to define function overloads that are only viable when a given condition holds:

```
template <bool Cond, typename T = void>
struct enable_if {
    typedef T type;
};
```

```
template <typename T>
struct enable_if<false, T> {};
```

