```
// Variation 2:
template<typename T>
class DD2 : public Base<T> {
    public:
        void f() { Base<T>::basefield = 0; }
};
```