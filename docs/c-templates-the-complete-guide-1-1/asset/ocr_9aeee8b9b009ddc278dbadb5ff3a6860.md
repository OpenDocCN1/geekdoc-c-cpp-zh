Because of these considerations, C++ templates provide ways to customize function templates and class templates transparently. For function templates, this is achieved through the overloading mechanism. For example, we can write an overloaded set of quickExchange functions as follows:

```
```cpp
template<typename T>
void quickExchange(T& a, T& b) // #1
{
    T tmp(a);
    a = b;
    b = tmp;
}

template<typename T>
void quickExchange(Array<T>* a, Array<T>* b) // #2
{
    quickExchange(*a, *b); // uses #1
}

void demo(Array<int>* p1, Array<int>* p2)
{
    int a=42, y=7;
    quickExchange(a, y); // uses #1
    quickExchange(p1, p2); // uses #2
}
```
```

The first call to quickExchange() has two arguments of type int, and therefore deduction succeeds with the first template, defined at #1, and the second template is not considered. The second call has two arguments of type Array<int>*, and the deduction succeeds with the second template at #2. Therefore, the second call is an exact match for the second template and the first template is not considered.

Of course, we can also overload to customize class templates. However, class templates do not support overloading. We can specialize class templates, but the specializations don't match the type of the template arguments. They are not overloaded. The following section discusses a more powerful technique for class template customization, called partial specialization. But for now, let's look at a few more function template overloading examples.

# 16.1.2 Semantic Transparency

The use of overloading in the previous section is very useful in achieving transparent customization of the instantiation process, but it is also somewhat misleading. In particular, we can see that the implementations of the templates may differ, and the one selected as a result of overloading may not behave as expected. In fact, the different behaviors are not always the same.

This is dramatically illustrated by considering code that compares the exchange of two values of type Array<int>:

```
```cpp
void distinguish(Array<int> a1, Array<int> a2)
{
    int a = a1[0];
    int b = a1[1];
    a1[0] = a2[0];
    a2[0] = a; // a1[0] after this
    a1[1] = a2[1];
    a2[1] = b; // a1[1] after this
    quickExchange(a1, a2); // uses #2
}
```
```

```
```cpp
void distinguish(Array<int> a1, Array<int> a2)
{
    int* p = &a1[0];
    int* q = &a1[1];
    a1[0] = a2[0];
    a2[0] = *p; // p no longer after this
    a1[1] = a2[1];
    a2[1] = *q; // q no longer after this
    quickExchange(a1, a2); // uses #2
}
```
```

This example shows that a pointer p into the first Array a1 becomes a pointer into the second array after quickExchange() is called. However, the pointer into the array a1 is still pointing into a1, even after the exchange operation. That means the value that was pointed to was swapped.