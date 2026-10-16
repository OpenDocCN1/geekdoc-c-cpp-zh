The **numpunct** facet defines the I/O format of built-in types, such as **bool**, **int**, and **double**:

**numpunct<C> facet** (siso.22.4.6.3.1)

**C decimal_point() const**; E.g., `,`

**C thousands_sep() const**; E.g., `,`

**string grouping() const**; E.g., `""` meaning “no grouping” **string_type truename() const**; E.g., **“true”**

**string_type falsename() const**; E.g., **“false”**

The characters of the string returned by **grouping()** are read as a sequence of small integer values. Each number specifies a number of digits for a group. Character **0** specifies the rightmost group (the least significant digits), character **1** the group to the left of that, etc. Thus, **“004\002\003”** describes a number such as **123–45–6789** (provided you use **‘_’** as the separation character). If necessary, the last number in a grouping pattern is used repeatedly, so **“\003”** is equivalent to **“\003\003\003”**. The most common use of grouping is to make large numbers more readable. The **grouping()** and **thousands_sep()** functions define a format for both input and output of integers and the integer part of floating-point values.

We can define a new punctuation style by deriving from **numpunct**. For example, I could define facet **My_punct** to write integer values using spaces to group the digits in sets of three and floating-point values, using a European-style comma as the “decimal point”:

```
class My_punct : public numpunct<char> {
public:
  explicit My_punct(size_t r = 0) : numpunct<char>(r) { }

protected:
  char do_decimal_point() const override { return ','; } // comma
  char do_thousands_sep() const override { return '_'; } // underscore string
  do_grouping() const override { return "\003"; } // 3-digit groups
};

void f()
{
  cout << "style A: " << 12345678
       << " *** " << 1234567.8
       << " ***" << fixed << 1234567.8 << '\n';

  cout << defaultfloat; // reset floating for mat
  locale loc(locale(), new My_punct);
  cout.imbue(loc);
  cout << "style B: " << 12345678
       << " *** " << 1234567.8
       << " ***" << fixed << 1234567.8 << '\n';
}
```

This produces:

**style A:** 12345678 *** 1.23457e+06 *** 1234567.800000