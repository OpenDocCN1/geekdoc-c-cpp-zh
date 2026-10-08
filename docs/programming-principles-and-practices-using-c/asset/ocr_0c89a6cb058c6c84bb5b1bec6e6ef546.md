Yes, digits are \u characters.

# # 23.8.4 Grouping

To specify a regular expression as a sub-pattern, you group it using parentheses. For example:

```
(\d*\:)
```

This defines a sub-pattern of zero or more digits followed by a colon. A group can be used as part of a more elaborate pattern. For example:

```
(\d\*\:)\?\(\d\+\)
```

This specifies an optional and possibly empty sequence of digits followed by a colon followed by a sequence of one or more digits. No wonder people invented a terse and precise way of saying such things!

# # 23.8.5 Alternation

The “or” character (|) specifies an alternative. For example:

```
Subject: \(\b\w\|\re\: \)\?\(.\*\)
```

This recognizes an email subject line with an optional \u or \u: followed by zero or more characters. For example:

+   *   Subject: \u: \u, \u!
*   Subject: \u:
*   Subject: \u \u

but not

+   *   \u: \u \u
*   \u \u: \u \u!

An empty alternative is not allowed:

```
|\u \u ) // \u
```

However, we can specify several alternatives at once:

```
(\u\u | \u\u | \u\u\u)
```