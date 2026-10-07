# 6.4.9 Comments

Except within a character constant, a string literal, or a comment, the characters /* introduce a comment. The contents of such a comment are examined only to identify multibyte characters and to find the characters */ to terminate it.^{83}

Except within a character constant, a string literal, or a comment, the characters // introduce a comment that includes all multibyte characters up to, but not including, the next new-line character. The contents of such a comment are examined only to identify the multibyte characters and to find the terminating new-line character.

EXAMPLE
```c
"a/b"                   // four-character string literal
#include "//"         // undefined behavior
//*                      // comment, not syntax error
f = g//*/h;               // equivalent to f = g / h;
i();                    // part of a two-line comment
/\                      // part of a two-line comment
5();
#define glue(x,y) ##y
glue(/,) k());     // syntax error, not comment
/**/* 1();               // equivalent to 1();
m = n//*/o               // equivalent to m = n + p;
+ p;
```

> 83) Thus, /* */ comments do not nest.