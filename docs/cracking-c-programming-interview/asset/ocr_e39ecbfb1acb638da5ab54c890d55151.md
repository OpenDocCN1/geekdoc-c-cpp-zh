(iv) The function prints the "hi" infinite when p = 50 till the stack gets full.
Which of the above are true?

+   (a) (i), (ii)
(b) (iii), (iv)
(c) (i), (iv)
(d) (iv)

# 10. What is the output of the following program?

```
#include<stdio.h>
int main()
{
  int n=0, m=0;
  if(n>0) //line 2
    if(m>0) //line 3
      printf("true");
  else
    printf("false");
  return 0;
}
```

+   (a) false
(b) true
(c) nothing will get printed
(d) error- compile time

# 11. What is the output of the following program?

```
#include<stdio.h>
int main()
{
  if(sizeof(int) > -5) //line 1
    printf("True\n");
  else
    printf("False");
  return 0;
}
```