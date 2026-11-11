![](bbox=[0.225, 0.144, 0.797, 0.215])

There are several specific points to observe:

+   1. The first field always starts with the first bit of the word.
+   2. A bit field cannot overlap integer boundaries. That is, the sum of lengths of all the fields in a structure should not be more than the size of a word. In case, it is more, the overlapping field is automatically forced to the beginning of the next word.
+   3. There can be unnamed fields declared with size. Example:
+   
+      ```c
+      Unsigned : bit-length
+      ```
+   
+      Such fields provide padding within the word.
+   4. There can be unused bits in a word.
+   5. We cannot take the address of a bit field variable. This means we cannot use `scanf` to read values into bit fields. We can neither use the pointer to access the bit fields.
+   6. Bit fields cannot be arrayed.
+   7. Bit fields should be assigned values that are within the range of their size. If we try to assign larger values, behaviour would be unpredictable.

Suppose, we want to store and use personal information of employees in compressed form, this can be done as follows:

```
```c
struct personal
{
    unsigned sex              :     1
    unsigned age              :     7
    unsigned m_status         :     1
    unsigned children         :     3
    unsigned                 :     4
} emp;
```
```

This defines a variable name **emp** with four bit fields. The range of values each field could have is as follows:

| Bit field | Bit length | Range of value |
|---|---:|---|
| sex | 1 | 0 or 1 |
| age | 7 | 0 or 127 (2⁷ − 1) |
| m_status | 1 | 0 or 1 |
| children | 3 | 0 to 7 (2³−1) |

Once bit fields are defined, they can be referenced just as any other structure-type data item would be referenced. The following assignment statements are valid.

```
```c
emp.sex = 1;
emp.age = 50;
```
```

Remember, we cannot use `scanf` to read values into a bit field. We may have to read into a temporary variable and then assign its value to the bit field. For example:

```
```c
scanf("%d %d", &AGE, &CHILDREN);
emp.age = AGE;
```
```