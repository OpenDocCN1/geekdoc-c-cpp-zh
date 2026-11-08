```
```cpp
void h1(pair<T, Rest...> const&);

template<typename T, typename... Rest>
void h2(pair<T, Rest...> const&);

void foo(pair<T1, T2> const& p, int& pi, double* pd,
         pair<double*, double> pdd)
{
    h1(pi, pdd); // OK: deduces T to int, Rest to (float,
                 // double)
    h2(pi, pdd); // ERROR: T deduced to int from the first
                 // argument but to double from the second
    h1(pi, pdd); // OK: one deduces T to int, double, Rest
    h2(pi, pdd); // ERROR: T deduced to (int, double), Rest
                 // to (float, double)
}
```
```

For both h1() and h2(), P is a reference type that is adjusted to the unqualified version of the reference (pair<T, Rest...> or pair<T, T2>, respectively) for deduction against each argument type. Since all arguments are specializations of class template pair, the template arguments are compared. For h1(), the first template argument (T) is not a parameter pack, so it is deduced independently for each argument. If the deductions differ, as in the second call to h1(), deduction fails. For the second pair template argument both h1() and h2() (first) are different, and the function template argument deduction determines the corresponding types. For h2(), the second call to h2() has the same problem.

For both h1() and h2(), the function template parameter packs are deduced by comparing the pattern of the pack expansion embedded within the tuple type. The types must be compatible for the function call to succeed.

```
```cpp
template<typename... Types> class tuple { };

template<typename... Types>
tuple(Types&&...);

template<typename T1, typename... Types>
tuple(T1&&, Types&&...);

void bar(tuple<short, int, long> sv,
         tuple<unsigned short, unsigned long> uv)
{
    f1(sv, sv); // OK: Types is deduced to (short, int,
                // long)
    f2(sv, sv); // OK: Types is deduced to (short, int,
                // long)
    f1(sv, uv); // ERROR: Types is deduced to (short, int,
                // long) from the first argument but to
                // (unsigned short, unsigned long) from the
                // second
}
```
```

In both f1() and f2(), the template parameter packs are deduced by comparing the pattern of the pack expansion embedded within the Tuple type. The types for f1() are against each of the template arguments of the tuple type provided by the call argument, deducing successive values for the corresponding template parameter pack. The function f1() uses the same template parameter pack Types in both function parameters, meaning that deduction only succeeds when the two function call arguments have the same set of types. The function f2(), on the other hand, uses different parameter packs for the Tuple type in each of its function parameters, so the types of the function call arguments can be different as long as each specialization is compatible with its corresponding parameter pack.

# 15.5.1 LITERAL OPERATOR TEMPLATE

Literal operator templates have their argument determined in a unique way. The following example illustrates this:

```
```cpp
template<char...> operator "" _B7() { }        // #1

int n = 121_B7;                                // #2
```
```

Here, the initial 121_B7 contains a user-defined literal, which is turned into a call to the literal operator template with the template argument list of '1', '2', and '1'. Thus, an implementation of the literal operator such as

```
```cpp
template<char... Chars>
operator "" _B7()
{
    std::array<char, sizeof...(Chars)>
        arr = {Chars...};
    for (char c : arr)                     // and use it (print
        std::cout << c << " ";
}
```
```