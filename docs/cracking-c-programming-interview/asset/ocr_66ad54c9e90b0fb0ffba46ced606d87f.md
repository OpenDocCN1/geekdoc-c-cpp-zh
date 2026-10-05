```
fun(&a);
printf("%u, %u", *a);
printf("%u, %u", *(a+1), **(a+1));
return 0;
)
```

+   (a) 5, 9, addr(5), addr(6), 6
(b) 5, 9, addr(5), addr(9), 9
(c) addr(5), addr(9), addr(5), addr(9), 9
(d) 5, 9, 5, 6, 9

+   23. Write a code in C to allocate a 2D array in memory dynamically using malloc()

+   24. Given: const int *ptr;
Which of the following statement is/are true about the given declaration?

+   (a) We cannot change the pointer itself that is ptr++ not allowed;
(b) We cannot change the value pointed by ptr that is (*ptr)++ not allowed.
(c) Both a and b;
(d) We can change pointer and value pointed by the pointer

+   23. What is the output of the following program?

```
#include<stdio.h>
#include<string.h>
int main()
{
  printf("%u, %u, %d, %u", sizeof(NULL), sizeof(""),
  strlen(""), sizeof("\0"));
  return 0;
}
```

+   (a) 1, 1, 1, 1
(b) 1, 1, 2, 1
(c) 4, 2, 0, 1