separately here. The syntax for a method of a class template with formal data types is as follows:

```
template <typename T>
void ClassName<T>::method( parameter ) { ...
```

With reference to our MyContainer class template, this definition of the method outside the class template would then be as shown in the following listing.

```
// https://godbolt.org/z/4fk5WdoG8
template <std::copyable T>
class MyContainer {
  T data_;
  public:
    void setData(const T& d);
    T getData() const;
};
template <std::copyable T>
void MyContainer<T>::setData(const T& d) {
  data_ = d;
}
template <std::copyable T>
T MyContainer<T>::getData() const {
  return data_;
}
```

**Listing 23.30** Method definitions outside the body of a class template are syntactically somewhat more complex.

It is important that for methods of class templates, you also specify the formal data type in angle brackets (here <T>) after the class name, as seen in MyContainer<T> :.... A specification like MyContainer<T> corresponds to specifying a complete type. An “empty” MyContainer would merely be a template name.