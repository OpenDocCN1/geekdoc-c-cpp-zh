In other words, we’d like to specify that all Lists of pointers share an implementation. Although this cannot be expressed in C++, we can achieve something quite close by specifying that all Lists of pointers should be instantiated from a different template definition: Click here to view code image

```
template<typename T>
class List<T*> { // #2
private:
List<void*> impl;
...
public:
...
inline void append(T* p) {
impl.append(p);
}
inline std::size_t length() const {
return impl.length();
}
...;
};
```

In this context, the original template at point #1 is called the primary template, and the latter definition is called a partial specialization (because the template arguments for which this template definition must be used have been only partially specified). The syntax that characterizes a partial specialization is the combination of a template parameter list declaration (template<...>) and a set of explicitly specified template arguments on the name of the class template (<T*> in our example).

Our code contains a problem because List<void*> recursively contains a member of that same List<void*> type. To break the cycle, we can precede the previous partial specialization with a full specialization: Click here to view code image

```
template<>
class List<void*> { // #3
...
void append (void* p);
inline std::size_t length() const;
...;
};
```

This works because matching full specializations are preferred over partial specializations. As a result, all member functions of Lists of pointers are forwarded (through easily inlineable functions) to the implementation of List<void*>. This is an effective way to combat code bloat (of which C++ templates are often accused).