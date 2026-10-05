# POINTERS

```
#include<stdio.h>
void main() {
    int *p,i,size;
    printf("Enter the array size..\n");
    scanf("%d",&size);
    p=(int *)malloc(size*sizeof(int));
    if(p==NULL)
        printf("OUT OF MEMORY error!\n");
    else {
        printf("\nEnter the array elements by one..\n");
        for(i=0;i<size;i++){
            scanf("%d",&p[i]);
        }
        printf("\nN array elements are..\n");
        for(i=0;i<size;i++){
            printf("%d->",p[i]);
        }
        free(p);
        getch();
    }
```

It is a good practice to always free the used memory to prevent any memory leak. The syntax to free up memory is simple, just use free (pointer variable). After freeing the memory, it is illegal to operate the memory locations. The output for the above program is given below.

# Program 7.10 malloc()

![](bbox=[0.248, 0.686, 0.778, 0.866])

Output 7.10