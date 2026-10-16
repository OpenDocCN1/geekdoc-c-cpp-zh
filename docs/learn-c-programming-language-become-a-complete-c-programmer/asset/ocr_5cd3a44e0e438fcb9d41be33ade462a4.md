```
*p=a; // OK
}
```

The increment and decrement operators are unique among C++ operators in that they can be used as both prefix and postfix operators. Consequently, we must define prefix and postfix increment and decrement for Ptr<T>. For example:

```
template<typename T>
class Ptr {
T* ptr;
T* array;
int sz;
public:
template<int N>
Ptr(T* p, T(&a)[N]); // bind to arraya,sz==N, initial value p
Ptr(T* p, T* a, int s); // bind to arrayaofsizes,initial value p
Ptr(T*p); // bind to single object, sz==0, initial value p

Ptr& operator++(); // prefix Ptr operator++(int); // postfix
Ptr& operator--(); // prefix Ptr operator--(int); // postfix
T& operator*(); // prefix
};
```

The int argument is used to indicate that the function is to be invoked for postfix application of ++. This int is never used; the argument is simply a dummy used to distinguish between prefix and postfix application. The way to remember which version of an operator++ is prefix is to note that the version without the dummy argument is prefix, exactly like all the other unary arithmetic and logical operators. The dummy argument is used only for the “odd” postfix ++ and--.

Consider omitting postfix ++ and-- in a design. They are not only odd syntactically, they tend to be marginally harder to implement than the postfix versions, less efficient, and less frequently used. For example:

```
template<typename T>
Ptr& Ptr<T>::operator++() // returnthe current object after incrementing
{
// ... checkthat ptr+1 can be pointed to ... return *++ptr;
}
template<typename T>
Ptr Ptr<T>::operator++(int) // increment and returnaPtr with the old value {
// ... checkthat ptr+1 can be pointed to ...
Ptr<T> old {ptr,array,sz};
++ptr;
return old;
}
```

The pre-increment operator can return a reference to its object. The post-increment operator must make a new object to return.