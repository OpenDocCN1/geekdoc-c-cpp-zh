method can take D, but also B. If the original method does not allow B as a parameter value, the overriding method can allow it. Conversely, the LSP is violated if the base method allows B but the overriding method forbids D.

And what about containers? Can a base method that returns vector<B> be overridden by a method that returns vector<D>?

```
// https://github.org/z/Gxh4edc8n
using std::vector;

struct B {};
struct D : public B {};

struct Basel {
    virtual B& func();
};

struct Derived1 : public Basel {
    virtual D& func() override; // D is covariant
};

struct Base2 {
    virtual B& func();
};

struct Derived2 : public Base2 {
    virtual D func() override; // D is not covariant
};

struct Base3 {
    virtual vector<B>& func();
};

struct Derived3 : public Base3 {
    virtual vector<D>& func() override; // vector<D>& is not covariant
};

struct Base4 {
    virtual vector<B*>& func();
};

struct Derived4 : public Base4 {
    virtual vector<D*>& func() override; // different type, not covariant
};
```

# Listing 19.6 Covariance for return types.