# ISO/IEC 14882:2017(E)

Table 134 — match_results assignment operator effects

| Element | Value |
| --- | --- |
| ready() | m.ready() |
| size() | m.size() |
| str() | m.str(n) for all integers n < m.size() |
| prefix() | m.prefix() |
| suffix() | m.suffix() |
| (*this)[n] | m[n] for all integers n < m.size() |
| length(n) | m.length(n) for all integers n < m.size() |
| position(n) | m.position(n) for all integers n < m.size() |

# 31.10.2 match_results state

[re.results.state]

```
bool ready() const;
```

Returns: true if *this has a fully established result, otherwise false.

# 31.10.3 match_results_size

[re.results.size]

```
size_type size() const;
```

Returns: One the number of marked sub-expressions in the regular expression that *this represents the result of a successful match. Otherwise returns 0. [Note: The state of a match_results object can be modified only by passing that to regex_match or regex_search. Sections 31.11.2 and 31.11.3 specify the effects of these algorithms on their match_results arguments.
-- end];

```
size_type max_size() const;
```

Returns: The maximum number of sub_match elements that can be stored in *this.

```
bool empty() const;
```

Returns: size() == 0.

# 31.10.4 match_results_element access

[re.results.acc]

```
difference_type length(size_type type = 0) const;
```

Requires: ready() == true.

Returns: (*this)[sub].length().

```
difference_type position(size_type sub = 0) const;
```

Requires: ready() == true.

Returns: The distance from the start of the target sequence to (*this)[sub].first.

```
string_type str(size_type sub = 0) const;
```

Requires: ready() == true.

Returns: string_type((*this)[sub].

```
const_reference operator[](size_type n) const;
```

Requires: ready() == true.

©ISO/IEC 2017 – All rights reserved

1321