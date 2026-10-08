# 10.3 Pointers and Arrays

```
#include <stdio.h>
int main() {
    int numbers[10] = {12,25,67,85,90,72,94,86,9,18};
    int *ptr;
    ptr = numbers;
    printf("The address printed is: %d\n", ptr);
    printf("The number printed is: %d\n", *ptr);
    printf("The number printed is: %d\n", ++ptr);
    printf("The number printed is: %d\n", ++ptr);
    printf("The number printed is: %d\n", *ptr++);
    printf("The number printed is: %d\n", ++ptr);
    return 0;
}
```

*++ptr is the same as **(++ptr)
++*ptr is the same as ++(*ptr)
*ptr++ is the same as *(ptr++)

The output is as follows:

+   - The address printed is: 10000 /* pointer is used */
- The number printed is: 12 /* pointer is incremented then used */
- The number printed is: 25 /* array element is incremented */
- The number printed is: 26 /* pointer is used then incremented */
- The number printed is: 26 /* pointer is used */
- The number printed is: 67 /* pointer is incremented then used */
- The number printed is: 85

Notice that the address of the numeric array is printed as 10000 in the first statement. In the second print statement the number 12 is printed by *ptr, which is simply dereferencing the first memory location. In the third print statement the pointer is incremented and then dereferenced, which prints number 25. In the next print statement the pointer is dereferenced, which points to the location containing the number 25 and the value 25 is incremented by 1 so that 26 is printed. The number 26 replaces the number 25 in memory. In the next statement, the number 26 is printed, having been changed from 25, and the post-increment is not effective in