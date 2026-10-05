+   (i) const char *p.
(ii) char const *p.
(iii) char *const p.
  (a) (i) and (ii) are equivalent and (iii) is invalid
  (b) All are valid and equivalent
  (c) Only (i) is valid
  (d) All are valid and (i) and (ii) are equivalent but (iii) is not equivalent to (i) and (ii).

# 47. What is the output of the following program?

```
#include<stdio.h>
int fun()
{
    return 20;
}
int main()
{
    const int i = fun();
    const int *p = &i;
    printf("%d", *p);
    return 0;
}
```

+   (a) 20
(b) error- run time
(c) 10
(d) error- compile time

# 48. What is the output of the following program?

```
#include<stdio.h>
int fun() {return 1;}
int main()
{
    enum block{int = fun() , two };
    printf("%d",two);
```