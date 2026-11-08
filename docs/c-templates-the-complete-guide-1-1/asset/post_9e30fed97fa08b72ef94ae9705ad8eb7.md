

Inspecting all of the possible types within a variant quickly devolves into a redundant chain of if statements. For example, the following prints the value of a `Variant<int, double, string>` named `v`:

**Click here to view code image**

```cpp
if (v.index()!=1) {
    std::cout << v.get<int>();
}
else if (v.is<double>()) {
    std::cout << v.get<double>();
}
else {
    std::cout << v.get<string>();
}
```

To generalize this to print the value stored in an arbitrary variant requires a recursively instantiated function template along with a helper. For example:

**Click here to view code image**

```cpp
// variant/printrec.cpp
#include <variant.hpp>
#include <iostream>

template<typename V, typename Head, typename... Tail>
void printImpl(V const& v)
{
    if (v.template is<Head>()) {
        std::cout << v.template get<Head>();
    }
    else if constexpr (sizeof...(Tail) > 0) {
        printImpl<V, Tail...>(v);
    }
}

template<typename... Types>
void print(variant<Types...> const& t)
{
    printImpl<variant<Types...>, Types...>(t);
}

int main()
{
    variant<int, short, float, double> v(1.5);
    print(v);
}
```

This is a significant amount of code for a relatively simple operation. To simplify this, we turn the problem around by extending `Variant` with a `visit()` operation. The client then passes in a visitor function object whose `operator()` will be invoked with the active value. Because the value could be any one of the variant's potential types, this operator is likely either to be overloaded or itself a function template. For example, a generic lambda provides a templated `operator()`, allowing us to easily represent the print operation for a variant:

**Click here to view code image**

```cpp
v.visit([](auto const& value) {
    std::cout << value;
});
```

This generic lambda is roughly equivalent to the following function object, which can also be useful for compilers that do not yet support generic lambdas:

**Click here to view code image**

```cpp
class VariantPrinter {
public:
    template<typename T>
    void operator()(T const& value) const
    {
        std::cout << value;
    }
};
```

The core of the `visit()` operation is similar to the process in our `get` operation. It steps through the types of the variant, checking whether the active...

Click here to view code image

variant/variantvisitimpl.h

```cpp
template<typename T, typename V, typename Visitor,
         typename Head, typename... Tail>

if (variantVisitImpl<Head>(variant, Visitor, Typelist<Tail...>{})) {
    return static_cast<T>(
        std::forward<Visitor>(visitor)(
            std::forward<V>(variant).template get<Head>()
        )
    );
} else if constexpr (sizeof...(Tail) > 0) {
    return variantVisitImpl<T, V, Visitor, Tail...>(
        std::forward<V>(variant),
        std::forward<Visitor>(visitor),
        Typelist<Tail...>{}
    );
} else {
    throw EmptyVariant();
}
```

variantVisitImpl() is a recursive function template with a number of template parameters. The template parameter T abstracts the result type of the visitation operation, which we will return later. V is the type of the variant and Visitor is the type of the visitor. Head and Tail are used to encapsulate the type list of the variant. To better understand the recursion, refer to the implementation of variantVisitImpl().

The first if performs a run-time check to determine whether the active value of the given variant is of type Head. If so, the visitor is invoked from the variant via get<Head>() and passed along to the visitor, terminating the recursion. The second if performs recursion when there are more elements to consider. If none of the types have matched, the variant does not contain a value, in which case the implementation throws the EmptyVariant exception.

Aside from the result type computation provided by visitResult (which will be discussed in the next section), the visit() implementation is straightforward:

Click here to view code image

Click here to view code image

variant/variantvisit.cpp

```cpp
template<typename... Types>
template<typename V, typename Visitor>
VisitResult<V, Visitor, Types...>
Variant<Types...>::visit(V&& vis) {
    using Result = VisitResult<V, Visitor, Types...>;
    return variantVisitImpl<Result>(this, std::forward<V>(vis),
                                    std::forward<Visitor>(visitor),
                                    Typelist<Types...>{});
}

template<typename... Types>
template<typename V, typename Visitor>
VisitResult<V, Visitor, Types const&>
Variant<Types...>::visit(V&& vis) const {
    using Result = VisitResult<V, Visitor, Types const&>;
    return variantVisitImpl<Result>(this, std::forward<V>(vis),
                                    std::forward<Visitor>(visitor),
                                    Typelist<Types...>{});
}

template<typename... Types>
template<typename V, typename Visitor>
Variant<Types...>::visit(Visitor&& visitor) const {
    using Result = VisitResult<R, Visitor, Types...>;

    return variant.VisitImpl<Result>(std::move(*this),
        std::forward<Visitor>(visitor),
        Types...{});
}
```

The implementations delegate to `variant.VisitImpl()` directly, passing along the variant itself, forwarding the visitor, and applying the complete list of types. The only differences between the three implementations are whether they pass the variant itself as `Variant&`, `Variant const&`, or `Variant&&`.

## 26.5.1 Visit Result Type

The result type your `visit()` returns is a mystery. A given visitor might have different `operator()` overloads that produce different result types, a templated `operator()` (where result type is dependent on its parameter type), or some combination thereof. For example, consider the following generic lambda:

```cpp
[](auto const& value) {
    return value + 1;
}
```

The result type of this lambda depends on the input type: given an `int`, it will produce an `int`, but given a `double`, it will produce a `double`. If this generic lambda were passed to the `visit()` operation of a `Variant<int, double>`, what should the result be?

There is no single correct answer, so our `visit()` operation allows the result type to be explicitly provided. For example, one might want to capture the return value in another `Variant<double>`. One can explicitly specify the result type to `visit()` as the first template argument:

**Click here to view code image**

```cpp
v.visit<Variant<int, double>>([](auto const& value) {
    return value + 1;
});
```

The ability to explicitly specify the result type is important when there is no one-size-fits-all solution. However, requiring that the result type be explicitly specified in all cases can be verbose. Therefore, `visit()` provides both options using the combination of a default template argument and a simple programming approach. Recall the declaration of `visit()`:

**Click here to view code image**

```cpp
template<typename R = ComputeResultType, typename... Types>
R visit(Visitor&& visitor) const;
```

The template parameter `R`, which we explicitly specified in the example above, also has a default argument so that it need not always be explicitly specified. That default argument is an incomplete sentinel type `ComputeResultType`:

```cpp
class ComputeResultType {};
```

**Click here to view code image**

variant/variantvisitresult.hpp

```cpp
// an explicitly provided visitor result type:
template<typename R, typename Visitor, typename... Elements>
class VisitResult {
public:
    using Type = R;
};

// ...

template<typename Visitor, typename... Elements>
class VisitResult<ComputeResultType, Visitor, Elements...> {
    // ...
};
```

This partial specialization is responsible for computing an appropriate result type for the common case, and is the subject of the next section.

## 26.5.3 Common Result Type

When calling a visitor that may produce different types for each of the variant's alternative types, how can we combine those types into a single result type for `visit()`? (There are some obvious cases—if the visitor returns the same type for each element type, that should be the result type of `visit()`.)

C++ already had a notion of a reasonable result type, which was introduced in Section 3.3.9 on page 12: The ternary expression `b ? x : y`, where the difference in the types `x` and `y` are ignored by the type of `x` and `y`. For example, if `x` has type `int` and `y` has type `double`, the common type is `double` because it promotes to `double`. We can capture this notion of the common type in a traits class:

**Click here to view code image**

```cpp
// variant/commonType.hpp

using std::declval;

template<typename T, typename U>
class CommonTypeT
{
public:
    using Type = decltype(true ? declval<T>() : declval<U>());
};

template<typename T, typename U>
using CommonType = typename CommonTypeT<T, U>::Type;
```

The notion of a common type extends to a set of types. The common type is a type to which all of the types in the set can promote. For our visitor, we want to compute the common type of the result types that the visitor will produce when called with each of the types in the variant:

**Click here to view code image**

```cpp
// variant/accumulateVisitorResult.hpp

#include "accumulate.hpp"
#include "commonType.hpp"

// the result type produced when calling a visitor with
// a particular element type
template<typename Visitor, typename ElementType>
using VisitElementResult = decltype(declval<Visitor>()(
    declval<ElementType>()));

// the common result type for a visitor called with
// each of the element types
template<typename Visitor, typename... ElementTypes>
class VisitResultType
{
    using ResultType =
        TypeList<VisitElementResult<Visitor, ElementTypes>...>;

public:
    using Type =
        Accumulate<PopFront<ResultType>, CommonTypeT, PopFront<ResultType>>;
};
```

The `VisitResult` computation occurs in two stages. First, `VisitElementResult` computes the result type produced when calling the visitor with a value of type `T`. This information is applied to each of the given element types to determine all of the result types that the visitor could produce, capturing the result in the typelist `ResultTypes`.

Next, the computation uses the `Accumulate` algorithm described in Section 9.3.4 on page 59 to apply the common-type operation to the typelist `ResultTypes`. This initial value is the first result type, which is combined with the other result types. The result is the common type to which all of the visitor's result types can be converted, or an error if the result types are incompatible.

