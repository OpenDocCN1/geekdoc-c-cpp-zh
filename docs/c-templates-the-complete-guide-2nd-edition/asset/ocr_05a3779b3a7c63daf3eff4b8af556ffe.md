```
succeed:
(VariantChoice<Types, Types...>::destroy() , ...);

// indicate that the variant does not store a value
this->setDiscriminator(0);
}
```

# 26.4.3 Assignment

Assignment builds on initialization and destruction, as illustrated by the assignment operators: [Click here to view code image](#)

```
variant/variantchoiceassign.hpp

template<typename T, typename... Types>
auto VariantChoice<T, Types...>::operator= (T const& value) -> Derived&
{
  if (getDerived().getDiscriminator() == Discriminator) {
    // assign new value of same type:
    *getDerived().template getBufferAs<T>() = value;
  }
  else {
    // assign new value of different type:
    getDerived().destroy(); // try destroy() for all types
    new(getDerived().getRawBuffer()) T(value); // place new value
    getDerived().setDiscriminator(Discriminator);
  }
  return getDerived();
}

template<typename T, typename... Types>
auto VariantChoice<T, Types...>::operator= (T&& value) -> Derived& {
  if (getDerived().getDiscriminator() == Discriminator) {
    // assign new value of same type:
    *getDerived().template getBufferAs<T>() = std::move(value);
  }
  else {
    // assign new value of different type:
    getDerived().destroy(); // try destroy() for all types
    new(getDerived().getRawBuffer()) T(std::move(value)); // place new value
    getDerived().setDiscriminator(Discriminator);
  }
  return getDerived();
}
```

As with initialization from one of the stored value types, each