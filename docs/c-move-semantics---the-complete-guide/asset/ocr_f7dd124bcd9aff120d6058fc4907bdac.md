parameter b became a reference to an array of const chars (const char(&)[6]). Therefore, type char[6] was deduced as type T2 and used as type of the second member. However, initializing an array member with an array is not possible because you cannot copy arrays.

In this case the decayed type should be used as member type, which is the type you get when you would pass the argument by value (const char* for string literals).

+   - As a consequence, with C++03, the function definition was changed to use call-by-value:

```
template<typename T1, typename T2>
pair<T1,T2> make_pair (T1 a, T2 b)
{
    return pair<T1,T2>(a,b);
}
```

As you can read in the rationale for the issue resolution, “it appeared that this was a much smaller change to the standard than the other two suggestions, and any efficiency concerns were more than offset by the advantages of the solution.”

+   - With C++11, make_pair() had to support move semantics, which meant that the arguments had to become universal/forwarding references. Again, we have the problem that for references the type of the arguments does not decay. Therefore, the definition changed as follows:

```
template<typename T1, typename T2>
constexpr pair<typename decay<T1>::type, typename decay<T2>::type>
make_pair (T1&& a, T2&& b)
{
    return pair<typename decay<T1>::type,
                typename decay<T2>::type>(forward<T1>(a),
                                        forward<T2>(b));
}
```

which, since C++14, can be written as follows:

```
template<typename T1, typename T2>
constexpr pair<decay_t<T1>, decay_t<T2>>
make_pair (T1&& a, T2&& b)
{
    return pair<decay_t<T1>, decay_t<T2>>(forward<T1>(a), forward<T2>(b));
}
```

The real implementation is even more complex since C++11: to support std::ref() and std::cref(), the function also unwraps instances of std::reference_wrapper<>.

The C++ standard library perfectly forwards passed arguments in many places in a similar way, often combined with using std::decay<>.