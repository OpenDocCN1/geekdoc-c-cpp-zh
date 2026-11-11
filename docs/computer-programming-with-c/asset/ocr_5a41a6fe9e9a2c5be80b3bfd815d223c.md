Also, the index position i must move in forward direction and hence the for loop must perform `i++` after every iteration. In each iteration, the loop copies the value of `a[k]` to `b[i]` as shown below:

```
for(i=0;k>=0;i++) /*increment i*/
{
    b[i]=a[k]; /*Copy a[k] to b[i]*/
    k--; /*decrement k*/
}
```

Figure 6.27 shows the detailed execution of the for loop that performs the copy operation.

As the index k starts from len-1 and decrements towards zero, the NULL character in array a is not copied in array b because the NULL character is present at position len which is after the last character in array a. Hence, we copy the NULL character explicitly as a last character of array b using the statement

```
b[len] = '\0';
```

after the for loop completes, as seen in the code.

The complete source code to calculate the reverse of the string is as given below:

```
#include<stdio.h>
void main()
{
    int len=0,i,k;
    char a[100],b[100];
    printf("Enter a String:\n");
    scanf("%s",a);
    for(i=0;a[i]!='\0';i++)
    {
        len++;
    }
    k=len-1;
    for(i=0;k>=0;i++)
    {
        b[i]=a[k];
        k--;
    }
    b[len] = '\0';
    printf("Reverse is: %s\n",b);
}
```

# Output

```
Enter a String:
hello
Reverse is: olleh
```