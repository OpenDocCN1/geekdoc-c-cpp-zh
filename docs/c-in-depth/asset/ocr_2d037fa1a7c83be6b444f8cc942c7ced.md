# *9.18 Program to sort strings represented by array of pointers*/

```
```c
#include<stdio.h>
#define N 5
main()
{
    char *arrp[N]={ "white","red","green","yellow","blue" };
    int i,j;
    char *temp;
    printf("Before sorting : \n");
    for(i=0;i<N;i++)
        printf("%s\t",arrp[i]);
    printf("\n");
    for(i=0;i<N;i++)
        for(j=i+1;j<N;j++)
            if(strcmp(arrp[i],arrp[j])>0)
            {
                temp=arrp[i];
                arrp[i]=arrp[j];
                arrp[j]=temp;
            }
    printf("After sorting :\n");
    for(i=0;i<N;i++)
        printf("%s\t",arrp[i]);
    printf("\n");
}
```
```

Output:

Before sorting -
    white  red  green  yellow  blue
After sorting -
    blue  green  red  white  yellow

![](bbox=[0.22, 0.78, 0.82, 0.97])