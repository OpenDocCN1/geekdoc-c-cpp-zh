```
class Stack { //OK
···
};
```

Since C++11, we can also substitute Cont with the name of an alias template, but it wasn’t until C++17 that a corresponding change was made to permit the use of the keyword typename instead of class to declare a template template parameter: Click here to view code image

```
template<typename T,
template<typename Elem> typename Cont = std::deque>
class Stack { //ERROR before C++17
···
};
```

Those two variants mean exactly the same thing: Using class instead of typename does not prevent us from specifying an alias template as the argument corresponding to the Cont parameter.

Because the template parameter of the template template parameter is not used, it is customary to omit its name (unless it provides useful documentation): Click here to view code image

```
template<typename T,
template<typename> class Cont = std::deque>
class Stack {
···
};
```

Member functions must be modified accordingly. Thus, you have to specify the second template parameter as the template template parameter. The same applies to the implementation of the member function. The push() member function, for example, is implemented as follows: Click here to view code image

```
template<typename T, template<typename> class Cont>
void Stack<T,Cont>::push (T const& elem)
{
elems.push_back(elem); // append copy of passed elem
}
```

Note that while template template parameters are placeholders for class or alias templates, there is no corresponding placeholder for function or variable templates.

# Template Template Argument Matching

If you try to use the new version of Stack, you may get an error message saying that the default value std::deque is not compatible with the template