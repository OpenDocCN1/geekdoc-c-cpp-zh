```
template<typename T>
class Container {
  public:
    ...

    requires HasLess<T>
    void sort() {
      ...
    }
};
```