This works fine, but of course not in cases where binary, octal, or hexadecimal values must also be interpreted. In that case we must first determine whether the first character(s) indicate a special number system. This can be determined by the class template NM2kmBase, that is now called from the _NM2km literal operator:

```
~~~cpp
template <char ... Chars>
size_t constexpr operator "" _NM2km()
{
    return static_cast<size_t>(          // forward Chars to NM2kmBase
               NM2kmBase<Chars ...>::value * 1.852);
}
~~~
```

The NM2kmBase class template normally assumes the decimal number system, passing base value 10 and initial sum 0 to NM2km. The NM2km class template is provided with an additional (first) non-type parameter representing the base value of the number system to use. Here is NM2kmBase:

```
~~~cpp
template <char ...Chars>
struct NM2kmBase
{
    enum
    {
        value = NM2km<10, 0, Chars ...>::value
    };
};
~~~
```

Partial specializations handle the different number systems, by inspecting the first (one or two) characters:

```
~~~cpp
template <char ...Chars>
struct NM2kmBase<'0', Chars ...>      // "0..."
{
    enum
    {
        value = NM2km<8, 0, Chars ...>::value          // octal value: base 8
    };
};

template <char ...Chars>
struct NM2kmBase<'0', 'b', Chars ...>  // "0b..."
{
    enum
    {
        value = NM2km<2, 0, Chars ...>::value          // binary value: base 2
    };
};

template <char ...Chars>
struct NM2kmBase<'0', 'x', Chars ...>  // "0x..."
{
    enum
    {
        value = NM2km<16, 0, Chars ...>::value          // hex value: base 16
    };
};
~~~
```

NM2km is implemented as before, albeit that it can now handle various number systems. The conversion from character to numeric value is left to a small support function template, cVal: