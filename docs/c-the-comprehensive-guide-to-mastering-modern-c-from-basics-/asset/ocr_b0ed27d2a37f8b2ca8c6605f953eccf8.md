```
unsigned operator""_w(const char*);
int main() {
    using namespace lits;
    1.2_w; // operator""_w(long double), with (1.2L)
    u'one'_w; // operator""_w(char16_t, size_t), with (u'one', 3)
    12_w; // operator""_w(const char*), with "12"
    "two"w; // operator""_w(const char*, size_t) not defined
}
```

**Listing 23.37** Which literal leads to which operator call?

For the literal "two"w, the compiler looks for operator""_w(const char*, size_t). Because we have not defined that, the compiler outputs an error message here.

**23.7.5** User-Defined Literal Using Template template

variant is also easy to implement if you only need to handle a well-defined set of literals.

```
// https://godbolt.org/z5rdzn8YP4
namespace lits {
    using general template
    template<char... > int operator""_bin2();
    // specializations
    template<> int operator""_bin2<'0','0'>() { return 0; }
    template<> int operator""_bin2<'0','1'>() { return 1; }
    template<> int operator""_bin2<'1','0'>() { return 2; }
    template<> int operator""_bin2<'1','1'>() { return 3; }
}
int main() {
    using namespace lits;
    int one = 01_bin2;
    int three = 11_bin2;
}
```

**Listing 23.38** A template for literals of exact length two.