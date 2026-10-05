```
}
# return value
no value returned
```

If the evenNumber function does not receive an even number, evenNumber returns nullopt. Otherwise the function returns an unsigned int.

opt.has_value() is a predicate that checks whether the std::optional variable has a value or is nullopt. opt.value() returns the value.

If opt is nullopt, opt.value() will throw an exception of type std::bad_optional_access.

The pointer dereferencing operators * and -> are implemented, but accessing an empty std::optional object has undefined behavior.

reset() destroys std::optional object and makes it empty (nullopt).