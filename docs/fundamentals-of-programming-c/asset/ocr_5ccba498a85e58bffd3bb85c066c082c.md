# F.1. DECLARING AND USING ARRAYS

```
int list[] = { 2, 4, 6, 8 };
```

| 2 | 4 | 6 | 8 |
| 0 | 1 | 2 | 3 |

```
double collection[10] = { 1.0, 3.5, 0.5, 7.2 };
```

| 1.0 | 3.5 | 0.5 | 7.2 | ? | ? | ? | ? | ? | ? |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

```
char letters[] = { 'a', 'b', 'c' };
```

| 'a' | 'b' | 'c' |
| 0 | 1 | 2 |

Figure F.2: Array declarations and memory layout

+   * Elements in an array are located by a numeric index. The first element is at index zero, not one.

```
int nums[10];
ums = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 }; // Illegal, will not compile
```

is illegal, and the compiler will report an error. The second statement is a simple assignment statement, not a declaration and initialization statement. An array may not appear all by itself on the left side of the assignment operator. An array, may be modified after that point of declaration only by reassigning elements using the [] operator.

In such expression as

```
list[3]
```

the expression within square brackets is called an index or subscript. The subscript terminology is borrowed from mathematicians who use subscripts to reference elements in a mathematical vector (for, example, V2 represents the second element in vector V). Unlike the convention used in mathematics, however, the first element in an array is at position zero, not. The expression list[2] can be read as “list two.\ The index indicates the distance from the beginning; the very first element is at a distance of zero from the beginning of the array. The first element of an array is a[0]. As a consequence of a zero beginning index, if an array holds n elements, the last element in it is a[n-1], not a[n].