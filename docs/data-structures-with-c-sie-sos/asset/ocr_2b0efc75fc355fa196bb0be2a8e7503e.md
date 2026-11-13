Given some printed text, the operations usually associated with word processing are the following:

+   (a) Replacement. Replacing one string in the text by another.
+   (b) Insertion. Inserting a string in the middle of the text.
+   (c) Deletion. Deleting a string from the text.

The above operations can be executed by using the string operations discussed in the preceding section. This we show below when we discuss each operation separately. Many of these operations are built into or can easily be defined in most of the programming languages.

# Insertion

Suppose in a given text T we want to insert a string S so that S begins in position K. We denote this operation by

```
INSERT(text, position, string)
```

For example,

```
INSERT ('ABCDEFG', 3, 'XYZ') = 'ABXYZCDEFG'
INSERT ('ABCDEFG', 6, 'XYZ') = 'ABCDEXYZFG'
```

This INSERT function can be implemented by using the string operation defined in the previous section as follows:

```
INSERT(T, K, S) = SUBSTRING(T, 1, K – 1) /// SUBSTRING(T, K, LENGTH(T) – K + 1)
```

That is, the initial substring of T before the position K, which has length K – 1, is concatenated with the string S, and the result is concatenated with the remaining part of T, which begins in position K and has length LENGTH(T) – (K – 1) = Length (T) – K + 1. (We are assuming implicitly that T is a dyamic variable and that the size of T will not become too large.)

# Deletion

Suppose in a given text T we want to delete the substring which begins at position K and has length L. We denote this operation by

```
DELETE(text, position, length)
```

For example,

```
DELETE( ' ABCDEFG ', 4, 2) = ' ABCFG '
DELETE( ' ABCDEFG ', 2, 4) = ' AFG '
```

We assume that nothing is deleted if position K = 0. Thus

```
DELETE( ' ABCDEFG ', 0, 2) = ' ABCDEFG '
```

The importance of this “zero case” is seen later.

The DELETE function can be implemented using the string operations given in the preceding section as follows:

```
DELETE(T, K, L) =
SUBSTRING(T, 1, K – 1)//SUBSTRING(T, K + L, LENGTH(T) – K – L + 1)
```

That is, the initial substring of T before position K is concatenated with the terminal substring of T beginning at position K + L. The length of the initial substring is K – 1, and the length of the terminal substring is: