The % operator replaces the expressions to its right in the character string to its left, in place of the placeholders like %2d or %.4f. In the above example the %4d specifier adds some left padding spaces to the string representing k, to get at least four characters. Likewise, the %.4f placeholder in 'pi = %.4f' % n(pi) outputs pi = 3.1416 with four digits after the decimal point.

In the terminal, the raw_input('message') command prints the text message, waits a keyboard input validated by the <Enter> key, and returns the user-given character string.

# ## 3.3 Lists and Other Data Structures

This section discusses some data structures available in Sage: character strings, lists — either mutable or immutable —, sets and dictionaries.

# ### 3.3.1 List Creation and Access

The list in computer science and the n-tuple in mathematics allow the enumeration of mathematical objects. In a pair — with (a, b) ≠ (b, a) — and an n-tuple, each object has its own position, contrary to a set.

A list is defined by surrounding its elements with square brackets [...], separated by commas. Assigning the triple (10, 20, 30) to the variable L is done as follows, and the empty list is defined as:

```
```
sage: L = [10, 20, 30]
sage: L
[10, 20, 30]
sage: []
                          # [] is the empty list
[]
```
```

The list indices are increasing from 0, 1, 2, etc. The element of index k of a list L is accessed simply by L[k], in mathematical terms this corresponds to the canonical projection on the k-th coordinate. The number of elements of a list is given by the len function⁵:

```
```
sage: L[1], len(L), len([])
(20, 3, 0)
```
```

Modifying an element is done the same way, by simply assigning the corresponding index. Hence the following command modifies the third term of the list, whose index is 2:

```
```
sage: L[2] = 33
sage: L
[10, 20, 33]
```
```

Negative indices access end-of-list elements, L[-1] referring to the last one:

⁵The output of len is a Python integer of type int, to get a Sage integer we write Integer(len(...)).