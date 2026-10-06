# ISO/IEC 14882:2017(E)

```
string_type truename() const;
string_type falsename() const;
static locale::id id;
```

```
protected:
    numpunct(); // virtual
    virtual char_type do_decimal_point() const;
    virtual char_type do_thousands_sep() const;
    virtual string do_grouping() const;
    virtual string_type do_truename() const; // for bool
    virtual string_type do_falsename() const; // for bool
};
```

+   1 numpunct<char> provides numeric notation. The specializations in Table 69 (25.3.1.1.1), numpunct<char> and numpunct<char> provide classic "C" numeric formats, i.e., they contain information equivalent to that contained in the "C" locale or their digit counterparts as identified by a call to widen().

The syntax for number formats is as follows, where digit represents the radix set by the fmtflags argument, and thousands-sep and decimal-point are the results of corresponding numpunct<char> members. Integer values have the:

```
integer ::= [sign] units
sign ::= [plusminus]
plusminus ::= '+\' | '-\''
units ::= digits [thousands-sep units]
digits ::= [digit]
```

and floating-point values:

```
float ::= [sign] units [decimal-point digits]] [e [sign] digits] |
           :: [sign]
           :: decimal-point digits [e [sign] digits]
           :: 'e' | 'E'
```

where the number of digits between thousands-seps is specified by do_grouping(). For parsing, if the digits contain no thousands-separators, no grouping constraint is applied.

# 25.4.3.1.1 numpunct members [facet.numpunct.members]

```
char_type do_decimal_point() const;
   Returns: do_decimal_point().
char_type do_thousands_sep() const;
   Returns: do_thousands_sep().
```

```
string grouping() const;
   Returns: do_grouping().
```

```
string_type truename() const;
   Returns: do_truename().
```

```
string_type falsename() const;
   Returns: do_falsename().
```

or do_truename() or do_falsename(), respectively.

§ 25.4.3.1.1

©ISO/IEC 2017 - All rights reserved

806