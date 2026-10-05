```
{
  for(j=0;j<1;j++)
    printf("%d%d%d%d\n",*( (p+i)+j), *( (j+p)+i),*( (i+p)+j),*( (p+j)+i);
  }
  return 0;
}
```

# 11. Determine the output of the following program?

```
#include<stdio.h>
#include<string.h>
int main()
{
  char *p="India";
  char a[]="India";
  printf("%d %d %d \ sizeof(p), sizeof(*), strlen(p));
  printf("%d %d", sizeof(a), strlen(a));
  return 0;
}
```

# 12. Determine the output of the following code?

```
#include<stdio.h>
int main()
{
  int i=4,j=7;
  j = j || i++ printf("YOU CAN");
  printf("%d %d", i, j);
  return 0;
}
```

+   (a) 4 7
(b) 4 1
(c) 4 8
(d) 5 7

# 13. Determine the output of the following code?