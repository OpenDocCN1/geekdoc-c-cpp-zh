# 30.10.3 State [re.results.state]

```
bool ready() const;
```

Returns: true if *this has a fully established result state, otherwise false.

# 30.10.4 Size [re.results.size]

```
size_type size() const;
```

Returns: One plus the number of marked sub-expressions in the regular expression that was matched if *this represents the result of a successful match. Otherwise returns 0.

> [Note 1: The state of a match_results object can be modified only by passing that object to regex_match or regex_search. Subclauses 30.11.2 and 30.11.3 specify the effects of those algorithms on their match_results arguments. — end note]

```
size_type max_size() const;
```

Returns: The maximum number of sub_match elements that can be stored in *this.

```
[[nodiscard]] bool empty() const;
```

Returns: size() == 0.

# 30.10.5 Element access [re.results.acc]

```
difference_type length(size_type sub = 0) const;
```

Preconditions: ready() == true.

Returns: (*this)[sub].length().

```
difference_type position(size_type sub = 0) const;
```

Preconditions: ready() == true.

Returns: The distance from the start of the target sequence to (*this)[sub].first.

```
string_type str(size_type sub = 0) const;
```

Preconditions: ready() == true.

Returns: string_type((*this)[sub]).

```
const_reference operator[](size_type n) const;
```

Preconditions: ready() == true.

Returns: A reference to the sub_match object representing the character sequence that matched marked sub-expression n. If n == 0 then returns a reference to a sub_match object representing the character sequence that matched the whole regular expression. If n >= size() then returns a sub_match object representing an unmatched sub-expression.

```
const_reference prefix() const;
```

Preconditions: ready() == true.

Returns: A reference to the sub_match object representing the character sequence from the start of the string being matched/searched to the start of the match found.

```
const_reference suffix() const;
```

Preconditions: ready() == true.

Returns: A reference to the sub_match object representing the character sequence from the end of the match found to the end of the string being matched/searched.

```
const_iterator begin() const;
const_iterator cbegin() const;
```

Returns: A starting iterator that enumerates over all the sub-expressions stored in *this.