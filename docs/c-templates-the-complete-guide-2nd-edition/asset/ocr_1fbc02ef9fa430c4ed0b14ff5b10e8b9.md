```
: functor(std::forward<FunctorFwd>(functor)) {
}
virtual SpecificFunctorBridge* clone() const override {
return new SpecificFunctorBridge(functor);
}
virtual R invoke(Args... args) const override {
return functor(std::forward<Args>(args)...);
}
};
```

Each instance of SpecificFunctorBridge stores a copy of the function object (whose type is Functor), which can be invoked, copied (by cloning the SpecificFunctorBridge), or destroyed (implicitly in the destructor). SpecificFunctorBridge instances are created whenever a FunctionPtr is initialized to a new function object, completing the FunctionPtr example: Click here to view code image

bridge/functionptr-init.hpp

```
template<typename R, typename... Args>
template<typename F>
FunctionPtr<R(Args...)>::FunctionPtr(F&& f)
: bridge(nullptr)
{
using Functor = std::decay_t<F>;
using Bridge = SpecificFunctorBridge<Functor, R, Args...>;
bridge = new Bridge(std::forward<F>(f));
}
```

Note that while the FunctionPtr constructor itself is templated on the function object type F, that type is known only to the particular specialization of SpecificFunctorBridge (described by the Bridge type alias). Once the newly allocated Bridge instance is assigned to the data member bridge, the extra information about the specific type F is lost due to the derived-to-based conversion from Bridge * to FunctorBridge<R, Args...> *.² This loss of type information explains why the term type erasure is often used to describe the technique of bridging between static and dynamic polymorphism.

One peculiarity of the implementation is the use of std::decay (see Section D.4 on page 731) to produce the Functor type, which makes the inferred type F suitable for storage, for example, by turning references to function types into function pointer types and removing top-level const, volatile, and reference types.