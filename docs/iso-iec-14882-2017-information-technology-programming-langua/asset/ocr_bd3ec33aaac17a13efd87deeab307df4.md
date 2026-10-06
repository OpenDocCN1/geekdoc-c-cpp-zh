# ISO/IEC 14882:2017(E)

```
charT w[1] = { ct.wididen('w') };nchar_class_type x = lookup_classname(w, w+1);
return (fzx) == x;
} else {
return false;
}
```

Example:

```
regez_traits<char> t;
string("upper");
regez_traits<char>:::char_class_type f;
f = t.lookup_classname(d.begin(), d.end());
f = t.lookup_classname(u.begin(), u.end());
tyype_base::mask m = convert<char>(f); // m ctype_base::ctype_base::upper
```

- end example

```
regez_traits<char> t;
string("w");
regez_traits<char>:::char_class_type f;
f = t.lookup_classname(w.begin(), w.end());
t.tctype('a', f); // returns true
t.tctype('_', f); // returns false
```

- end example

```
int value(charT ch, int radix);
```

+   13 Requires: The value of radix shall be 8, 10, or 16.

+   14 Returns: the value represented by the digit ch in base radix if the character ch is a valid digit in base radix; otherwise returns -1.

```
local_type imbue(local_type loc);
```

+   15 Effects: Imbues with a copy of the loc. [Note: Calling imbue with a different locale than the one currently in use invalidates all cached data held by *this.] — end note

+   16 Returns: if no locale has been previously imbued then a copy of the global locale at the time of construction of *this; otherwise a copy of the last argument passed to imbue.

+   17 Postconditions: getloc() == loc.

```
local_type getloc() const;
```

+   18 Returns: if no locale has been imbued then a copy of the global locale at the time of construction of *this, otherwise a copy of the last argument passed to imbue.

# 31.8 Class template basic_regex

+   1 For a char-like type charT, specializations of class basic_regex represent regular expressions constructed from character sequences of charT. In the rest of 31.8, charT defines a char-like type. Storage for a regular expression is allocated and freed as necessary by the member functions of class basic_regex.

+   2 Objects of type specialization of basic_regex are responsible for converting the sequence of charT objects to an internal representation. It is not specified what this representation takes, how it is accessed by algorithms that operate on regular expressions. [Note: Implementations will typically declare some function templates as friends of basic_regex to achieve this — end note]