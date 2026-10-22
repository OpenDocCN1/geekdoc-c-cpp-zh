s1

| V | T | U | 1 | 2 | \0 |  |  |  |  |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

And s2

| V | T | U | 1 | 2 | 3 | \0 |  |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

# strcat(str1,str2)

This function copies all the characters of string str2 to the end of string str1. The delimiter of string str1 is replaced by the first character of str2. The size of str1 should be large enough to store a string whose length is str1+str2.

Str1

| h | i |  |  |  |  |  |  |  |  |

Str2

| h | e | l | l | o |  |

afterstrcat

Str1

| h | i | h | e | l | l | o | \0 |  |  |

Str2

| h | e | l | l | o |  |
|  |  |  |  |  |  |