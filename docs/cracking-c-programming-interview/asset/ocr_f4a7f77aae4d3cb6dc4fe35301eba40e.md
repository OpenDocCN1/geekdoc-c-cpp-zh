```
{
  printf("%d d %d %d",sizeof(s1),sizeof(s2),sizeof(s3));
  return 0;
}
```

+   (a) 14 9 130
(b) 16 10 140
(c) 20 12 160
(d) 18 10 140

44. **What is the output of the following program?**

```
#include<stdio.h>
struct std {
  int sn;
  char name[20];
} s1;
int main() {
  struct std s2 = {1, "john"};
  s1 = s2; //line 2
  printf("%p %p\n",&s1.name, &s2.name); //line 3
  strcpy(s2.name, "will");
  printf("%s %s",s1.name, s2.name); //line 5
  return 0;
}
```

+   (a) line 3:: Print both address, line 5:: john will
(b) line 3:: Print both different address, line 5:: john will
(c) Error at line 2: character array cannot assign using = sign
(d) error- run time

45. **What is the default access specifier of structure in C?**

+   (a) Private
(b) Public
(c) Protected
(d) Extern