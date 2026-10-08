```
Ax*
// A, Ax, Axxxx
```

```
Ax+
// Ax, Axxx Not A
```

```
\d-\?d\d{2}
// 1-2, 12 Not 1-2
```

```
\w{2}-\d{4,5}
// Ab-1234, XX-54321, 22-5432 Digits are in \w
```

```
(\d*:)?(\d+)
// 12:3, 1:23, 123, :123 Not 123:
```

```
(bs|BS)
// bs, BS Not bS
```

```
[aeiou]
// a, o, u An English vowel, not x
```

```
[^aeiou]
// x, k Not an English vowel, not e
```

```
[a^eiou]
// a, ^, u An English vowel or ^
```