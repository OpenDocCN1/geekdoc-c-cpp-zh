# Strings before Copy:

strng1

| S | t | r | a | g | e | T | e | c | h | n | o | l | o | g | T | o | d | a | y | \0 |

strng2

| M | o | s | t | A | v | a | n | c | e | d | \0 |

The string copy function is coded as follows:

```
strncpy(strng1, strng2, 4);
printf("strng1: %s\n", strng1);
printf("strng2: %s\n", strng2);
```

The output after copy is as follows:

strng1: Mostage Today
strng2: Most Advanced

Strings after Copy:

strng1

| M | o | s | t | g | e | T | e | c | h | n | o | l | o | g | T | o | d | a | y | \0 |

strng2

| M | o | s | t | A | v | a | n | c | e | d | \0 |

Notice that only the first four characters "Most" of strng2 are copied into strng1 and the rest of the characters in strng1 are retained including the null terminator. If only part of strng2 is copied, as in this example, then the null terminating character is not copied.

# Strings before Copy:

strng1

| S | t | r | a | g | e | T | e | c | h | n | o | l | o | g | T | o | d | a | y | \0 |

strng2

| M | o | s | t | A | v | a | n | c | e | d | \0 |