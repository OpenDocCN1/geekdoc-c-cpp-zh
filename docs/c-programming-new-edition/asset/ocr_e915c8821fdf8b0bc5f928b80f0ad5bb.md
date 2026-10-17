```
fun_ptr=disp;
printf("address is %d",fun_ptr);
(*fun_ptr());
}
disp()
{
printf("aliens are tasty");
}
```

The output of the program would be:
address is 5211
ali ens are tasty.

You must be bewildered after encountering the declaration int(*fun-ptr)(); Well take it as a rule that this is how a pointer into which the address of a function is to be passed should be written. The rest of the program must be easy to comprehend.

# 6.8. FUNCTIONS RETURNING POINTERS

You must be wondering why the functions have been reincarnated. The reason is that these concepts cannot be explained unless the knowledge of pointers is adequate. Now that pointers to some extent have entered your veins be advised that functions can not only return values back to the caller function but also pointers can be returned from within the called function. However, certain rules have to be incorporated to achieve such a feat. To make a function return a pointer it has to be explicitly mentioned in the calling function as well as the function declaration. The following program illustrates this.

```
#include<stdio.h>
void main()
{
int *a; int *func();
a=func();
printf("value of A is",a);
}
int *func()
```