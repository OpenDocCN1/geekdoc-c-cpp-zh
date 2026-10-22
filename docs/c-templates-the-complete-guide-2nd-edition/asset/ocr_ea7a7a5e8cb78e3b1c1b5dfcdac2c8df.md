which, however, means that we first have to forward declare `Stack<T>`:

```
template<typename T>
class Stack;

template<typename T>
std::ostream& operator<< (std::ostream&, Stack<T> const&); Then, we
can declare this function as friend: Click here to view code image

template<typename T>
class Stack {
...
friend std::ostream& operator<< <T> (std::ostream&,
Stack<T> const&);
};
```

Note the `<T>` behind the “function name” operator<<. Thus, we declare a specialization of the nonmember function template as friend. Without `<T>` we would declare a new nontemplate function. See Section 12.5.2 on page 211 for details.

In any case, you can still use this class for elements that don’t have operator<< defined. Only calling operator<< for this stack results in an error: Click here to view code image

```
Stack<std::pair< int, int>> ps; // std::pair<> has no operator<<
defined
ps.push({4, 5}); // OK
ps.push({6, 7}); // OK
std::cout <<
ps.top().first << '\n'; // OK
std::cout <<
ps.top().second << '\n'; // OK
std::cout << ps << '\n'; // ERROR: operator<< not supported
// for element type
```

# 2.5 Specializations of Class Templates

You can specialize a class template for certain template arguments. Similar to the overloading of function templates (see Section 1.5 on page 15), specializing class templates allows you to optimize implementations for certain types or to fix a misbehavior of certain types for an instantiation of the class template. However, if you specialize a class template, you must also specialize all member functions. Although it is possible to specialize a single member function of a class template, once you have done so, you can no longer specialize the whole