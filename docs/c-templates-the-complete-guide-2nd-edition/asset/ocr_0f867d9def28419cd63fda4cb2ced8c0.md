# Assignment

The Variant assignment operators are similar to the copy and move constructors above. Here, we illustrate only the copy assignment operator: Click here to view code image

variant/variantcopyassign.hpp

```
template<typename... Types>
Variant<Types...>& Variant<Types...>::operator= (Variant const& source) {
if (!source.empty()) {
source.visit([&](auto const& value) {
*this = value;
});
}
else {
destroy();
}
return *this;
}
```

The only interesting addition is in the else branch: When the source variant contains no value (indicated by a discriminator 0), we destroy the value of the destination, implicitly setting its discriminator to 0.

# 26.7 Afternotes

Andrei Alexandrescu covered discriminated unions in detail in a series of articles [AlexandrescuDiscriminatedUnions]. Our treatment of Variant relies on some of the same techniques such as aligned buffers for in-place storage and visitation to extract values. Some of the differences are due to the base language: Andrei was working with C++98, so, for example, it cannot make use of variadic templates or inheriting constructors. Andrei also devotes considerable time to the computation of alignment, which C++11 made trivial with the introduction of alignas. The most interesting design difference is in the handling of the discriminator: While we opted to use an integral discriminator to indicate which type was currently stored in the variant, Andrei employs a “static vtable” approach using function pointers to construct, copy, query, and destroy the underlying element type. Interestingly, this static vtable approach has been more influential as an optimization technique for open discriminated unions like the FunctionPtr template, developed in Section 22.2 on page 519, and is a