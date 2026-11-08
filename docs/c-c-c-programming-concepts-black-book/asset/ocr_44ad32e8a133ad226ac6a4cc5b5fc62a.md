# Listing 3.5: Showing the Working of the strcat() Function

```
Example

# include<stdio.h>
# include<string.h>

int main()
{
    char myName[50];
    char yourName[50];

    printf("\n Enter  name 1 -> ");
    gets(myName);
    printf("\n Enter  name 2 -> ");
    gets(yourName);

    strcat(yourName, myName);

    printf("\n Result is ");
    puts(yourName);
    getch();
    return 0;
}
```

Output of the preceding program is as follows:

```
Enter  name 1 -> Tanuman Bhaduri

Enter  name 2 -> John Rider

Result is John RiderTanuman Bhaduri
```

# strcmp()

The signature of the strcmp() function is as follows:

```
int strcmp(const char *str1, const char *str2);
```

The strcmp() function compares the two strings and finds out whether they are similar or different. The two strings are compared lexicographically until there is a mismatch or one of the strings reached its end. If both the strings are identical, then strcmp() returns a zero. If they are not identical, then strcmp() returns the numeric difference between the ASCII values of first non-matching pairs of characters. Listing 3.6 shows the working of strcmp():

# Listing 3.6: Showing the Working of the strcmp() Function

```
# include<stdio.h>
# include<string.h>

int main()
{
    char myName[50];
    char yourName[50];

    printf("\n Enter  name 1 -> ");
    gets(myName);
    printf("\n Enter  name 2 -> ");
    gets(yourName);

    if(!strcmp(myName,yourName))
```