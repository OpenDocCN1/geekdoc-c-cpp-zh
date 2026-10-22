```
```cpp
virtual bool equals(FunctorBridge<R, Args...> const* fb) const override {
  if (auto specFb = dynamic_cast<SpecificFunctorBridge const*>(fb)) {
    return TryEquals<Functor>::equals(functor, specFb->functor);
  }
  // functors with different types are never equal:
  return false;
}
```
```