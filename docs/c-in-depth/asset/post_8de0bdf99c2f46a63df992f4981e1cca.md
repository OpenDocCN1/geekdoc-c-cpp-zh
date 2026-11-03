
```
"yellow",
"blue"
};
```

This initialization is equivalent to

```
char arr[5][10] = {
{'w','h','i','t','e','\0'},
{'r','e','d','\0'},
{'g','r','e','e','n','\0'},
{'y','e','l','l','o','w','\0'},
{'b','l','u','e','\0'}
};
```

Here first subscript of array denotes number of strings in the array and second subscript denotes the maximum length that each string can have. The space reserved for this two-dimensional array is 50 bytes.

Here the name of 2-D array is arr and it gives the base address of the array i.e. it gives the address of first string.

- arr[0] represents 0th string, points to 0th character of 0th string
- arr[1] represents 1st string, points to 0th character of 1st string
- arr[i] represents ith string, points to 0th character of ith string
- arr[i][j] represents jth character in ith string

So we see that if we want to access individual characters in the string then we use two subscripts and if we want to access the strings we use a single subscript.

| 起始地址 | 字符串内容 | 结束地址 |
|---|---|---|
| 2000 | w h i t e \0 | 2009 |
| 2010 | r e d \0 | 2019 |
| 2020 | g r e e n \0 | 2029 |
| 2030 | y e l l o w \0 | 2039 |
| 2040 | b l u e \0 | 2049 |

This is the internal storage representation of array of strings. 2000 is the base address of the first string. Similarly, 2010 is the base address of the second string. Here 10 bytes are reserved in memory for each string. We can see that first string takes only 6 bytes, so 4 bytes are wasted. Similarly 2nd string takes only 4 bytes and 6 bytes are wasted. The total number of bytes occupied by the array is 50 while the strings use only 28 bytes so 22 bytes of memory is wasted. Now we'll see through a program how to print these strings.

```
/*P9.12 Program to print the strings of the two-dimensional character array*/
#include<stdio.h>
#define N 5
#define LEN 10
main()
{
    char arr[N][LEN]={
        "white",
        "red",
        "green",
        "yellow",
        "blue"
    };
    int i;
    for(i=0;i<N;i++)
    {
        printf ("String = %s\t",arr[i] );
        printf ("Address of string = %u\n", arr[i]);
    }
}
```

Output:

```
String = white      Address of string = 2000
String = red        Address of string = 2010
String = green      Address of string = 2020
String = yellow     Address of string = 2030
String = blue       Address of string = 2040
```

In the above program we have initialized the 2-D array with strings. Suppose we don’t initialize it at the time of declaration and try to assign strings to it afterwards like this-

```
arr[0] = "white";      /*Invalid*/
arr[1] = "red";        /*Invalid*/
```

This will give an error 'lvalue required'. Similarly we cannot write

```
arr[0] = arr[1];       /*Invalid*/
```

If we want to assign values to strings we’ll have to use strcpy() or scanf() function.

```
strcpy(arr[0], "white");      /*Valid*/
scanf("%s", arr[0]);          /*Valid*/
strcpy(arr[0], arr[1]);       /*Valid*/
```

Now we’ll take a program to sort the strings alphabetically using the selection sort technique.

```
/*P9.13 Program to sort the array of strings*/
#include<stdio.h>
#define N 5
#define LEN 10
main()
{
    char arr[N][LEN]={
        "white",
        "red",
        "green",
        "yellow",
        "blue"
    };
    char temp[10];
    int i,j;
    printf("Before sorting :\n");
    for(i=0;i<N;i++)
        printf (" %s   ", arr[i]);
    printf("\n");
    for(i=0;i<N;i++)
        for(j=i+1;j<N;j++)
            if(strcmp(arr[i],arr[j])>0)
            {
                strcpy(temp,arr[i]);
                strcpy(arr[i],arr[j]);
                strcpy(arr[j],temp);
            }
    printf("After sorting :\n");
    for(i=0;i<N;i++)
        printf (" %s   ",arr[i]);
}
```

Output:

```
Before sorting :
white red green yellow blue
After sorting :
blue green red white yellow
```

The internal representation of strings after sorting is-

| 起始地址 | 字符串内容 | 结束地址 |
|---|---|---|
| 2000 | b l u e \0 | 2009 |
| 2010 | g r e e n \0 | 2019 |
| 2020 | r e d \0 | 2029 |
| 2030 | w h i t e \0 | 2039 |
| 2040 | y e l l o w \0 | 2049 |

Internal representation after sorting

Here the sorting is not considered very efficient since each time the whole string is being copied.

## 9.6 Array Of Pointers To Strings

We have already studied about array of pointers. Array of pointers to strings is an array of char pointers in which each pointer points to the first character of a string i.e. each element of this array contains the base address of a string. Let us take an example and see how this array can be declared and initialized.

```
char *arrp[] ={
    "white",
    "red",
    "green",
    "yellow",
    "blue"
};
```

Here arrp is an array of pointers to strings. We have not specified the size of array, so the size is determined by the number of initializers. The initializers are string constants. arrp[0] contains the base address of string “white”, similarly arrp[1] contains the base address of string “red”.

Now let us see how these strings are stored in memory-

![](img/a76c706396af8b310f291a5313a27079_282_0.png)

| String | Address of string | Address of string is stored at |
|---|---|---|
| white | 100 | 2000 |
| red | 106 | 2002 |
| green | 110 | 2004 |
| yellow | 116 | 2006 |
| blue | 123 | 2008 |

Here all strings occupy 28 bytes and 10 bytes are occupied by the array of pointers. So the total byte occupied are 38 bytes. In two-dimensional array, total bytes occupied were 50 bytes for these same strings. So we can see here saving of 12 bytes.

In the figure we see that strings are stored in consecutive memory locations. Well it is not necessary, they may not be stored consecutively and pointers may point to strings located anywhere. Now let us see how to print these strings.

```
/*P9.14 Program to print the address and string using array of pointer to strings*/
#include<stdio.h>
main()
{
    int i;
    char *arrp[] = {
        "white",
        "red",
        "green",
        "yellow",
        "blue"
    };
    for(i=0;i<5;i++)
    {
        printf ("String : %s\t",arrp[i] );
        printf ("Address of string : %u\t",arrp[i] );
        printf("Address of string is stored at : %u\n",arrp+i );
    }
}
```

Output:

```
String : white      Address of string : 100      Address of string is stored at : 2000
String : red        Address of string : 106      Address of string is stored at : 2002
String : green      Address of string : 110      Address of string is stored at : 2004
String : yellow     Address of string : 116      Address of string is stored at : 2006
String : blue       Address of string : 123      Address of string is stored at : 2008
```

Instead of initializing we could have assigned strings after declaration as-

```
arrp[0] = "white";      /*Valid*/
arrp[1] = "red";        /*Valid*/
```

Remember this type of assignment was invalid when we used 2-D array. Here it is valid because arrp[0] is a pointer variable and it can be assigned address of any string.

Now let us compare array of strings and array of pointers to strings. Earlier we had studied the differences between strings declared as pointers and strings declared as arrays. Here also we have same differences that are illustrated by this program.

```
/*P9.15 Program to show the differences between array of strings and array of pointers to strings*/
#include<stdio.h>
main()
{
    char  arr[5][10];
    char *arrp[5];

    arr[0]="January";                 /*Invalid*/
    arrp[0]="January";                /*Valid*/

    strcpy(arr[1],"February");        /*Valid*/
    strcpy(arrp[1],"February");       /*Invalid, arrp[1] not initialized*/

    scanf("%s",arr[2]);               /*Valid*/
    scanf("%s",arrp[2] );             /*Invalid, arrp[2] not initialized*/

    arrp[3]=(char *)malloc(10);
    strcpy(arrp[3],"March");          /*Valid*/

    arrp[4]=(char *)malloc(10);
    scanf("%s",arrp[4] );             /*Valid*/
}
```

We have seen that we can't input strings directly in an array of pointers using scanf(). We have to first allocate memory through malloc( ). Here is a program in which we first enter the string and then allocate memory required for that string. This allocated memory is pointed by an element of array of pointers.

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

Output:

```
Enter date : 2/5/2002

Month : May
```

We could do this by switch statement also but using array of pointers makes the stuff concise.

The next program sorts the strings represented by array of pointers using selection sort technique
