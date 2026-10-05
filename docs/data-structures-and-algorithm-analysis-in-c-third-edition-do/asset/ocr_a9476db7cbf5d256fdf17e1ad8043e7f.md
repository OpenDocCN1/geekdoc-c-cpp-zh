Sec. 4.5 Further Reading

```
int size() { // Return list size
{ return list->length(); }
};
```

Figure 4.34 (continued)

for the comparator class to extract the key from the record type, as an alternative to
storing key-value pairsnHere is an example of the required class for comparing integers.

```
class intCompare { // Comparator class for integer keys
public:
    static bool lt(int x, int y) { return x < y; }
    static bool eq(int x, int y) { return x == y; }
    static bool gt(int x, int y) { return x > y; }
};
```

intCompare provides methods for determining if int variables
are equal (eq), or if the first is less than the second (lt), or greater than the second
(gt).
Here is a class for comparing C-style character strings. It makes use of the
standard library function strcmp // Compare two character strings

```
class CCmpare {
public:
    static bool lt(char* x, char* y) {
        return strcmp(x, y) < 0; }
    static bool eq(char* x, char* y) {
        return strcmp(x, y) == 0; }
    static bool gt(char* x, char* y) {
        return strcmp(x, y) > 0; }
};

```

We use a comparator in Section 5.5 to implement comparison in heaps, and
in Chapter 7 to implement comparison in sorting algorithms.

# 4.5 Further Reading

For more discussion on choice functions used to define the List ADT, see the
work of the Reuse Software Research Group from Ohio State. Their definition
for the List ADT can be found in [SWH93]. More information about designing
classes can be found in [SWH94].

# 4.6 Exercises

4.1 Assume a list has the following configuration:

| 2, 23, 15, 5, 9 |