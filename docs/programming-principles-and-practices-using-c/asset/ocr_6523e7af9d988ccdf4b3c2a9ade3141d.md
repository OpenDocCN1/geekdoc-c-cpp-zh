If you want at least one occurrence, use **+** rather than **\***. For example,

```
Ax+
```

matches an **A** followed by one or more **xs**, such as

```
Ax  
Axx  
Axxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

but not

```
A
```

The common case of zero or one occurrence (“optional”) is represented by a question mark. For example,

```
\d–?d
```

matches the two digits with an optional dash between them, such as

```
1–2  
12
```

but not

```
1––2
```

To specify a specific number of occurrences or a specific range of occurrences, use curly braces. For example,

```
\w{2}–\d{4,5}
```

matches exactly two letters and a dash (–) followed by four or five digits, such as

```
Ab–1234  
XX–54321  
22–54321
```

but not

```
Ab–123  
?b–1234
```