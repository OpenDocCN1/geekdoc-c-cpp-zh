```
Is same class? false
Is convertible from/to? false
End *****************
Is base of? false
Is same class? false
Is convertible from/to? true
End *****************
Is base of? false
Is same class? false
Is convertible from/to? false
End *****************
Is base of? false
Is same class? false
Is convertible from/to? false
End *****************
Is base of? false
Is same class? false
Is convertible from/to? false
End *****************
Is base of? false
Is same class? false
Is convertible from/to? true
End *****************
```

# 6.3.5 'Internal Properties' of Types

We show how to examine several properties of member functions of a type, in particular constructors and destructors:

```
template <typename T>
    void MethodInformation(const T& t)
{ //

    // Numeric type
    std::cout << "Virtual destructor? " << std::boolalpha
              << std::has_virtual_destructor<T>::value << std::endl;
    std::cout << "Default constructible? " << std::boolalpha
              << std::is_default_constructible<T>::value << std::endl;
    std::cout << "Copy constructible? " << std::boolalpha
              << std::is_copy_constructible<T>::value << std::endl;
    std::cout << "Move constructible? " << std::boolalpha
              << std::is_move_constructible<T>::value << std::endl;
    std::cout << "Copy assignable? " << std::boolalpha
              << std::is_copy_assignable<T>::value << std::endl;
    std::cout << "Move assignable? " << std::boolalpha
              << std::is_move_assignable<T>::value << std::endl;
    std::cout << "Destructible? " << std::boolalpha
              << std::is_destructible<T>::value << std::endl;

    std::cout << "End ************************\n";
}
```