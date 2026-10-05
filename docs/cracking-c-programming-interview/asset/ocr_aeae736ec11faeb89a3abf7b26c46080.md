```
}
```

(a) 1000 1048

(b) 1000 1096

(c) 1000 1001

(d) 1000 1004

# 8. Which mathematical function is computed by given function foo(x, n)?

```
int foo(int x, int n)
{
int val = 1;
if (n > 0)
{
if (n % 2 == 1)
val *= x;
val *= foo(x * x, n / 2);
}
return val;
}
```

(a) x^n

(b) n^x

(c) n^n

(d) n * x

# 9. What is the output of the following program?

```
#include<stdio.h>
int main()
{
char a[] = "India";
char *b = "is great";
a = "Love";
b = "yes";
printf("%s %s", a, b);
}
```