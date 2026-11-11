It is desired to prepare a revised alphabetical list with surname (last name) first, followed by a comma and the initials of the first and middle names. For example,

Argand, J.R

We create a table of strings, each row representing the details of one person, such as first_name, middle_name, last_name, and telephone number. The columns are interchanged as required and the list is sorted on the last_name. Figure 10.14 shows a program to achieve this.

```
```c
#define CUSTOMERS    10

main( )
{
        char    first_name[20][10], second_name[20][10],
                surname[20][10], name[20][20],
                telephone[20][10], dummy[20];

        int     i,j;

        printf("Input names and telephone numbers \n");
        printf("?");
        for(i=0; i < CUSTOMERS ; i++)
        {
                scanf("%s %s %s", first_name[i],
                      second_name[i], surname[i], telephone[i]);

                /* converting full name to surname with initials */

                strcpy(name[i], surname[i]);
                strcat(name[i], ",");
                dummy[0] = first_name[i][0];
                dummy[1] = '\0';
                strcat(name[i], dummy);
                strcat(name[i], ".");
                dummy[0] = second_name[i][0];
                dummy[1] = '\0';
                strcat(name[i], dummy);
        }
                /* Alphabetical ordering of surnames */

                for(i=1; i <= CUSTOMERS-1; i++)
                        for(j=1; j <= CUSTOMERS-i; j++)
```
```