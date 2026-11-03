first allocate memory through malloc( ). Here is a program in which we first enter the string and then allocate memory required for that string. This allocated memory is pointed by an element of array of pointers.

```
/*P9.16*/
#include<stdio.h>
#include<string.h>
main()
{
        char *arrp[10],str[20];
        int i;
        for(i=0;i<10;i++)
        {
                printf("\nEnter string %d :  ",i+1);
                gets(str);
                /* Now allocate memory sufficient to hold the string*/
                arrp[i]=(char *)malloc(strlen(str)+1);
                strcpy(arrp[i],str);
        }
        for(i=0;i<10;i++)
                printf("%s\t",*(arrp+i));
        printf("\n");
        for(i=0;i<10;i++)
                free(arrp[i]);
}
```

If we want to enter the number of strings at run time, then we can allocate the array of pointers dynamically as we had done in previous chapter program P8.33.

Array of pointers is also useful in grouping together logically related data items. For example we can take the names of months in an array and then access them by appropriate subscript.

```
/*P9.17  Program to input a date and print the month*/
#include<stdio.h>
main()
{
        int d,m,y;
        char *months[]={"January", "February", "March", "April", "May",
                        "June", "July", "August", "September", "October",
                        "November", "December"};
        printf("Enter date (dd/mm/yy) : ");
        scanf("%d/%d/%d",&d,&m,&y);
        printf("Month : %s\n",months[m-1]);
}
```

# Output:

Enter date : 2/5/2002

Month : May

We could do this by switch statement also but using array of pointers makes the stuff concise.

The next program sorts the strings represented by array of pointers using selection sort technique