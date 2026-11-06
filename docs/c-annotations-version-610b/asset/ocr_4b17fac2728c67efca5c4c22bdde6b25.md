```
```cpp
ci.push_back("3");
ci.pop_front();
ci.push_back("4");
ci.pop_front();
ci.push_back("5");
cout << ci.size() << ' ' << ci.front() << ' ' << ci.back() << '\n';

CirQue<string> copy(ci);
copy.pop_front();
cout << copy.size() << ' ' << copy.front() << ' ' << copy.back() << '\n';

int arr[] = {1, 3, 5, 7, 9};
CirQue<int> ca(arr);
cout << ca.size() << ' ' << ca.front() << ' ' << ca.back() << '\n';

//    int *ap = arr;
//    CirQue<int> cap(ap);
}
```
```

This program produces the following output:

```
```text
2 1 2
3 3 5
2 4 5
5 1 9
```
```

# 21.1.6 Default class template parameters

Different from function templates, template parameters of template classes may be given default argument values. This holds true for both template type- and template non-type parameters. If default template arguments were defined and if a class template object is instantiated without specifying arguments for its template parameters then the template parameter's defaults are used.

When defining defaults keep in mind that they should be suitable for the majority of instantiations of the class. E.g., for the class template `CirQue` the template's type parameter list could have been altered by specifying `int` as its default type:

```
```cpp
template <typename Data = int>
```
```

Even though default arguments can be specified, the compiler must still be informed that object definitions refer to templates. When instantiating class template objects using default template arguments the type specifications may be omitted but the angle brackets must be retained. Assuming a default type for the `CirQue` class, an object of that class may be defined as:

```
```cpp
CirQue<> intCirQue(10);
```
```

Default template arguments cannot be specified when defining template members. So, the definition of, e.g., the `push_back` member must always begin with the same `template` specification:

```
```cpp
template <typename Data>
```
```

When a class template uses multiple template parameters, all may be given default values. Like default function arguments, once a default value is used all remaining template parameters must also use their default values. A template type specification list may not start with a comma, nor may it contain multiple consecutive commas.