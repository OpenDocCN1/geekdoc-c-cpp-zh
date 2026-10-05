return 0;
}

# 58. What is the output of the following program?

```
#include<stdio.h>
#include<stdlib.h>
void fun(int **i)
{
  (*i)[4]=99;
  (*i)++; // line 2
}
int main()
{
  int *p=(int)malloc(sizeof(int)*10);//line 4
  fun(&p);
  printf("%d\n", p[3]);
  free(p); //line 7
  return 0;
}
```

+   (a) 99;
(b) 0
(c) 99, error- run time due to line 7

59. Given a function pointer 'f' pointing to a function that is taking two integers as its input parameter and returning integer pointer.
int *(f)(int, int);
Demonstrate it with some example?

60. Given a function pointer 'funptr' pointing to a function which is taking an integer and function pointer 'f' as its input parameter and returning void type.
'f' is a pointer to a function that is taking two integers as its parameter and returning integer pointers (int *).
void (*funptr)(int, int*(*f)(int, int));