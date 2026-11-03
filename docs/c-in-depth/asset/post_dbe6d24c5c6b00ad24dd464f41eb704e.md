
```c
char str1[10],str2[10];
printf("Enter the first string : ");
scanf("%s",str1);
printf("Enter the second string : ");
scanf("%s",str2);
if((strcmp(str1,str2))==0)
    printf("Strings are same\n");
else
    printf("Strings are not same\n");
}
```

**Output:**
```text
Enter the first string : Bangalore
Enter the second string : Mangalore
Strings are not same
```

```c
int strcmp(char str1[ ],char str2[ ])
{
    int i=0;
    while(str1[i]!='\0'&&str2[i]!='\0'&&str1[i]==str2[i])
        i++;
    if(str1[i]==str2[i])
        return 0;
    else
        return(str1[i]-str2[i]);
}
```

```c
int pstrcmp(char *str1,char *str2)
{
    while(*str1!='\0'&&*str2!='\0'&&*str1==*str2)
    {
        str1++;
        str2++;
    }
    if(*str1==*str2)
        return 0;
    else
        return(*str1-*str2);
}
```

This function is used for copying one string to another string. strcpy( str1, str2 ) copies str2 to str1. Here str2 is the source string and str1 is destination string. If str2 = "suresh" then this function copies "suresh" into str1. This function takes pointers to two strings as arguments and returns the pointer to first string.

```c
/* P9.8 Program to understand the work of strcpy() function*/
#include<stdio.h>
#include<string.h>
main()
{
    char str1[10],str2[10];
    printf("Enter the first string : ");
    scanf("%s",str1);
    printf("Enter the second string : ");
    scanf("%s",str2);
    strcpy(str1,str2);
    printf("First string :%s \t\t Second string : %s\n",str1,str2);
    strcpy(str1,"Delhi");
    strcpy(str2,"Calcutta");
    printf("First string :%s \t\t Second string : %s\n",str1,str2);
}
```

**Output:**
```text
Enter the first string : Bombay
Enter the second string : Mumbai
First string : Mumbai        Second string : Mumbai
First string : Delhi         Second string : Calcutta
```

The programmer should take care that the first string has enough space to hold the second string. The function calls like strcpy("New", str1) or strcpy("New", "York") are invalid because "New" is a string constant which is stored in read only memory and so we can't overwrite it.

```c
strcpy("New", str1);        /*Invalid*/
strcpy("New", "York");      /*Invalid*/
```

### Creation of this Function

- Array version-

```c
char *astrcpy(char str1[ ],char str2[ ])
{
    int i=0;
    while(str2[i]!='\0')
    {
        str1[i]=str2[i];    /*Copy character by character*/
        i++;
    }
    str1[i]='\0';
    return str1;
}
```

- Pointer version-

```c
char *pstrcpy(char *str1,char *str2)
{
    while(*str2!='\0')
    {
        *str1=*str2;
        str1++;
        str2++;
    }
    *str1='\0';
    return str1;
}
```

We can write the above function concisely as-

```c
char *strcpy(char *str1,char *str2)
{
    while(*str1++ = *str2++);
    return str1;
}
```

## 9.3.4 strcat()

This function is used for concatenation of two strings. If first string is "King" and second string is "size" then after using this function the first string becomes "Kingsize".

```c
strcat(str1, str2); /*concatenates str2 at the end of str1*/
```

The null character from the first string is removed, and the second string is added at the end of first string. The second string remains unaffected.

This function takes pointer to two strings as arguments and returns a pointer to the first(concatenated) string.

### 9.9 Program to understand the work of strcat() function

```c
#include<stdio.h>
#include<string.h>
main()
{
    char str1[20],str2[20];
    printf("Enter the first string : ");
    scanf("%s",str1);
    printf("Enter the second string : ");
    scanf("%s",str2);
    strcat(str1,str2);
    printf("First string : %s \tSecond string : %s\n",str1,str2);
    strcat(str1,"_one");
    printf("Now first string is : %s \n",str1);
}
```

### Output:

```text
Enter the first string : data
Enter the second string : base
First string : database Second string : base
Now first string is : database_one
```

### Creation of this Function

- Array version-

```c
char *astrcat(char str1[],char str2[])
{
    int i=0,j=0;
    while(str1[i]!='\0') /*Check for the end of first string*/
        i++;
    while(str2[j]!='\0') /*Add second string at the end of first*/
    {
        str1[i]=str2[j];
        i++;
        j++;
    }
    str1[i]='\0';
    return str1;
}
```

- Pointer version-

```c
char *pstrcat(char *str1,char *str2)
{
    while(*str1!='\0')
        str1++;
    while(*str2!='\0')
    {
        *str1=*str2;
        str1++;
        str2++;
    }
    *str1='\0';
    return str1;
}
```

The function strcat() returns a pointer to the first string, hence it can be nested. The following program illustrates this.

```c
#include<stdio.h>
#include<string.h>
main()
{
    char str1[20]="Subhash ";
    char str2[10]="Chandra ";
    strcat(str1,str2);
    printf("str1 - %s\n",str1);
}
```

**Output:**
```text
str1 - Subhash Chandra Bose
```

Other string related functions are explained in the chapter on library functions.

## 9.4 String Pointers

We can take a char pointer and initialize it with a string constant. For example-

```c
char *ptr = "Chennai";
```

Here ptr is a char pointer which points to the first character of the string constant "Chennai" i.e. contains the base address of this string constant.

Now we'll compare the strings defined as arrays and strings defined as pointers.

```c
char str[] = "Mumbai";
char *ptr = "Chennai";
```

These two forms may look similar but there are some differences in them. The initialization itself has different meaning in both forms. In the array form, initialization is a short form for-

```c
char str[] = {'M', 'u', 'm', 'b', 'a', 'i', '\0'};
```

while in pointer form, address of string constant is assigned to the pointer variable.

Now let us see how they are represented in memory.

| 1000 | 1001 | 1002 | 1003 | 1004 | 1005 | 1006 |
|---|---|---|---|---|---|---|
| M | u | m | b | a | i | \0 |
| str[0] | str[1] | str[2] | str[3] | str[4] | str[5] | str[6] |

| 5220 | 5221 |
|---|---|
| 200 |  |

| 200 | 201 | 202 | 203 | 204 | 205 | 206 | 207 |
|---|---|---|---|---|---|---|---|
| C | h | e | n | n | a | i | \0 |

Here str is an array of characters and 7 bytes are reserved for it. Since str is the name of an array hence it is a constant pointer which will always point to the first element of array. The elements of array are initialized with the characters of the string. Note that we had mentioned before that when a string constant appears as array initializer, then it does not return an address.

In the second case, the string constant "Chennai" is stored somewhere in memory with 8 consecutive bytes reserved for it. The string constant returns the address of the first character of the string that is assigned to the pointer variable ptr. So in this case total 10 bytes are reserved, 2 bytes for the pointer variable and 8 bytes for the string.

The main difference is that str is a constant pointer and will always contain address 1000 while ptr is a pointer variable and may contain any other address. So string assignments are valid for pointers while they are invalid for strings defined as arrays.

```c
str = "Bombay";    /*Invalid*/
ptr = "Delhi";     /*Valid*/
```

We can assign string of any length to ptr. That string constant will be stored somewhere and its address will be assigned to ptr.

| 5220 | 5221 |
|---|---|
| 310 |  |

| 310 | 311 | 312 | 313 | 314 | 315 |
|---|---|---|---|---|---|
| D | e | l | h | i | \0 |

We can assign a different string to str by scanf(), strcpy or by assigning characters.

```c
strcpy(str, "Bombay");
scanf("%s", str);
```

or

```c
str[0] = 'B'; str[1] = 'o'; str[2] = 'm'; str[3] = 'b'; str[4] = 'a'; str[5] = 'y'; str[6] = '\0';
```

This will write the new string at the address 1000, but take care that string size does not exceed the size of array.

We have studied earlier that string constants are stored in read only area by some compilers and so they can't be changed. So these operations are invalid-

```c
char *ptr = "Bareilly";
ptr[0] = 'D'; /*Invalid*/
scanf("%s",ptr);
strcpy(ptr, "Bareilly"); /*Invalid*/
```

We can't use scanf() with uninitialized pointer since it contain garbage value-

```c
char *ptr;
scanf("%s",ptr); /*Invalid*/
```

For this first we should allocate memory through malloc(), and let this pointer point to that region of memory.

```c
ptr = (char *)malloc(20);
scanf("%s",ptr); /*Valid*/
```

```c
/*P9.11*/
#include<stdio.h>
main()
{
    char *str;
    str=(char *)malloc(10);
    printf("Enter a string : ");
    scanf("%s",str);
    printf("String is : %s\n",str);
}
```

**Output:**
```text
Enter a string : Oxford
String is : Oxford
```

## 9.5 Array Of Strings Or Two Dimensional Array Of Characters

Strings are character arrays so array of strings means array of character type arrays i.e. a two dimensional array of characters.

Suppose we declare and initialize a two-dimensional array of characters as-

```c
char arr[5][10] = {
"white",
"red",
"green",
"
```
