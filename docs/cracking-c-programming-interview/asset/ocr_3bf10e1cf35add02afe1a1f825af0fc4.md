```
printf("%d",one);
printf("%c",two); //line 2
printf("%s",three); //line 3
return 0;
)
```

+   (a) 1 b c
(b) error: different types of elements are not allowed in enum
(c) error: enum cannot be char at line 2
(d) error: enum cannot be string at line 3

# 44. What is the output of the following program?

```
#include<stdio.h>
#define i 10
int main()
{
enum block(int i = i , two );
printf("%d",two);
return 0;
}

```

+   (a) 0
(b) 1
(c) 11
(d) error- compile time

# 45. What is the difference between the given definitions?

+   (i) const i = 10;
(ii) int const i = 10;
(a) Both are legal but not equivalent.
(b) (i) is illegal but not (ii).
(c) (i) is legal but not (ii).
(d) Both are legal and equivalent.

# 46. Which of the following option is true about the given declarations?