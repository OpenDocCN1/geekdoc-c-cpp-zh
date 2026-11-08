```
~~~
template<typename... T>
void advance(T& t, int n);
~~~
```

```
~~~
double d = 1.0; // ERROR: 1.0 is a literal with
two decimal points
int i = 1; // OK
float f = 1.0f; // OK
~~~
```

Template-type expressions can include template parameters in the name. For example, the following function template returns either the type of the elements or the size:

Click here to view code image

```
~~~
template<typename T1, typename T2>
constexpr bool isomorphic()
{
    return sizeof(T1) == sizeof(T2); // ERROR:
}
~~~
```

This is an application of fold expressions (see Section 4.3 on page 5) for

Click here to view code image

```
~~~
isomorphic<int, int>()
~~~
```

The expression for the return value expands to

Click here to view code image

```
~~~
std::is_same<int, int>::value && std::is_same<int, int>::value
~~~
```

and yields false, while

Click here to view code image

```
~~~
isomorphic<int, char>()
// ERROR: "int", "char"
~~~
```

would be true because all passed arguments are deduced to be char* (Note that the argument types decay because the call arguments are passed by value.)

# 4.4.2 Variadic Indices

As another example, the following function uses a variadic list of indices to access the corresponding element of the passed first argument:

Click here to view code image

```
~~~
template<typename C, typename... Idx>
void printElems(C const& coll, Idx... idx)
{
    print(coll[idx]...);
}
~~~
```

That is when calling

Click here to view code image

```
~~~
std::vector<std::string> coll = {"good", "times", "say", "bye"};
printElems(coll,2,0,3);
~~~
```

The effect is to call

Click here to view code image

```
~~~
print(coll[2], coll[0], coll[3]);
~~~
```

You can also declare nontype template parameters to be parameter packs. For example:

Click here to view code image

```
~~~
template<std::size_t... Idx, typename C>
void printIdx(C const& coll)
{
    print(coll[Idx]...);
}
~~~
```

allows you to call

Click here to view code image

```
~~~
std::vector<std::string> coll = {"good", "times", "say", "bye"};
printIdx<2,0,3>(coll);
~~~
```

which has the same effect as the previous example.

# 4.4.3 Variadic Class Templates

Variadic templates can also describe class templates. An important example is a class where an arbitrary number of template parameters specify the types of corresponding members:

Click here to view code image

```
~~~
template<typename... Elements>
class Tuple;
~~~
```

```
~~~
Tuple<int, std::string, char> t; // can hold int, string, and char
~~~
```

This will be discussed in Chapter 25.

Another example is that it is able to specify the possible types objects can have:

Click here to view code image