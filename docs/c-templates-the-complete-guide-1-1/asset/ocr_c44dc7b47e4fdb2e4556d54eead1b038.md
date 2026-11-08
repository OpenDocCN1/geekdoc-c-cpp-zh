This term is somewhat misleading, because it is the name of a pre-defined C++ header. But the term "injected" names the official term because the including scope, making these visible to normal name lookup. In our example above, this would mean that both Code would be well-formed. This chapter therefore further details the history of fixed name injection.

# 13.2.2 Injected Class Names

The name of a class is injected inside the scope of that class itself and therefore accessible as an unqualified name in that scope. (However, it is not accessible as a qualified name because this is the rule used to declare the constructor. For example:

Click here to view code image

```
```cpp
template<typename T>
class C {
  private:
    T t[10];
  public:
    static int i[5];
};

template<typename T>
int C<T>::i[5] = {};

int main()
{
    std::cout << "C<T>::i = " << C<int>::i << '\n'
              << "C<T>::i = " << C<long>::i << '\n';
}
```
```

The member function C<T>::i returns the size of type C, whereas the function i returns the number of the variable (in other words, the size of an int object).

Class templates also have injected class names. However, they're stranger than ordinary injected class names: They can also be followed by template arguments (in which case they are injected class template names) but if they are not followed by template arguments they represent the class with its parameters as its arguments (or, for a partial specialization, its specialization arguments) if the context expects a type, or a template if the context expects a template. This explains the following situation:

Click here to view code image

```
```cpp
template<typename T> class X {
};

template<typename T> class X<T*> {
};

X x1;         // OK: see "class X" above
X<double> x2; // OK
X<int*> x3;   // OK: see "class X<T*>" above

template<typename T>
class C {
  ...
  C* c;       // OK: C is injected class name
              //    and therefore always
              //    denotes the template
};
```
```

Note how the injected name refers to the injected name and not a substituted name of the template if it is not followed by a list of template arguments. To compensate, you can force the name of the template to be followed by using the scope qualifier ::.

The injected class name for a variable template has an additional variable: If the injected class name were directly formed by using the variable template's template parameters as the template arguments, the injected class name would contain template parameter packs (but we have seen that pack names would contain template parameter packs) but have no ... (we saw in Section 12.4.1 on page 405 for details of pack expansion) Therefore, when forming the injected class name for a variable template, the template arguments that correspond to a template parameter pack in a pack expansion where the pattern is a template parameter pack.

Click here to view code image