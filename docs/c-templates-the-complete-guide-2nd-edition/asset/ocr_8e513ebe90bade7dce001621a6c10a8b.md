```
template<typename T>
class CopierInterface {
    public:
        virtual void copy_to(Array<T, SArray<T>>& ) const;
};

template<typename T, typename X>
class Copier : public CopierInterface<T> {
    public:
        Copier(X const& x) : expr(x) {
        }
        virtual void copy_to(Array<T, SArray<T>>& ) const {
            // implementation of assignment loop
            ...
        }
    private:
        X const& expr;
};
```