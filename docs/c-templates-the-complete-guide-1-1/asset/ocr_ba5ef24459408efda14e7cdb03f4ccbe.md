```
```cpp
FunctionPtr() : bridge( nullptr ) {
}

FunctionPtr(FunctionPtr const& other) { // copy ctor
  bridge = other.bridge;
}

FunctionPtr(FunctionPtr& other)
  : FunctionPtr(const_cast<FunctionPtr const&>(other))
{ }

FunctionPtr(FunctionPtr&& other) : bridge(other.bridge) {
  other.bridge = nullptr;
}

// construction from arbitrary function objects
template<typename F> FunctionPtr(F&& f) // see [1]
  : bridge( ... )
{ }

// assignment operators
FunctionPtr& operator=(FunctionPtr const& other) {
  FunctionPtr tmp(other);
  swap(*this, tmp);
  return *this;
}

FunctionPtr& operator=(FunctionPtr&& other) {
  delete bridge;
  bridge = other.bridge;
  other.bridge = nullptr;
  return *this;
}

// construction and assignment from arbitrary function objects
template<typename F> FunctionPtr& operator=(F&& f) {
  FunctionPtr tmp(std::forward<F>(f));
  swap(*this, tmp);
  return *this;
}

// destructor
~FunctionPtr() {
  delete bridge;
}

friend void swap(FunctionPtr& fp1, FunctionPtr& fp2) {
  std::swap(fp1.bridge, fp2.bridge);
}

explicit operator bool() const {
  return bridge == nullptr;
}

// invocation
R operator()(Args... args) const // note: FunctionPtr
{
  return bridge->operator()(std::forward<Args>(args)...);
}
```
```

The implementation contains a single nonstatic member variable, bridge, which will be responsible for both storage and manipulation of the stored function object. Ownership of this pointer is tied to the lifetime of the FunctionPtr object. The implemented functions contain the interesting parts of the implementation and is described in the following subsections.

# ## 22.3 BRIDGE INTERFACE

The FunctionPtr class template is responsible for the ownership and manipulation of the function object. The implementation is implemented as an abstract base class, forming the foundation for the dynamic polymorph...