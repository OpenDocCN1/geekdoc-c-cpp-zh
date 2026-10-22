exception.

Aside from the result type computation provided by `VisitResult` (which will be discussed in the next section), the `visit()` implementation is straightforward: [Click here to view code image](#)

**Click here to view code image**

```
variant/variantvisit.hpp

template<typename... Types>
template<typename R, typename Visitor>
VisitResult<R, Visitor, Types&...>
Variant<Types...>::visit(Visitor&& vis) & {
using Result = VisitResult<R, Visitor, Types&...>;
return variantVisitImpl<Result>(*this, std::forward<Visitor>(vis),
TypeList<Types...>());
}

template<typename... Types>
template<typename R, typename Visitor>
VisitResult<R, Visitor, Types const&...>
Variant<Types...>::visit(Visitor&& vis) const& {
using Result = VisitResult<R, Visitor, Types const&...>;
return variantVisitImpl<Result>(*this, std::forward<Visitor>(vis),
TypeList<Types...>());
}

template<typename... Types>
template<typename R, typename Visitor>
VisitResult<R, Visitor, Types&&...>
Variant<Types...>::visit(Visitor&& vis) && {
using Result = VisitResult<R, Visitor, Types&&...>;
return variantVisitImpl<Result>(std::move(*this),
std::forward<Visitor>(vis),
TypeList<Types...>());
}
```

The implementations delegate to `variantVisitImpl` directly, passing along the variant itself, forwarding the visitor, and supplying the complete list of types. The only differences between the three implementations are whether they pass the variant itself as `Variant&`, `Variant const&`, or `Variant&&`.

# 26.5.1 Visit Result Type

The result type of `visit()` remains a mystery. A given visitor might have different `operator()` overloads that produce different result types, a