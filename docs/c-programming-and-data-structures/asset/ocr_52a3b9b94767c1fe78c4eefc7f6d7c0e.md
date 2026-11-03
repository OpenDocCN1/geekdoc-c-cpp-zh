# 4.44 Computer Programming

The program also counts the number of lines read and the total number of characters in the text. Remember, the last line containing the null string is not counted. After the first while loop is exited, the program prints the results of counting.

# 2. Processing of a Customer List

| Full name | Telephone number |
|-----------|------------------|
| Joseph Louis Lagrange | 869245 |
| Jean Robert Argand | 900823 |
| Carl Fredrich Gauss | 806788 |
|  |  |

It is desired to prepare a revised alphabetical list with surname (last name) first, followed by a comma and the initials of the first and middle names. For example, Argand,J.R.

We create a table of strings, each row representing the details of one person, such as first_name, middle_name, last_name, and telephone_number. The columns are interchanged and the list sorted on the last_name. Figure 4.24 shows a program to achieve this.

```
#define CUSTOMERS 10
main ( )
{
char first_name[20][10], second_name[20][10], surname[20][10], name[20][20], telephone[10][10], dummy[10];
int i,j;
printf("Input names and telephone numbers \n");
printf("? ");
for(i=0; i < CUSTOMERS; i++)
{
scanf("%s %s %s", first_name[i], second_name[i], surname[i]);
/* converting full name to surname with initials */
strcpy(name[i], surname[i] );
strcat(name[i], "," );
dummy[0] = first_name[i][0];
strcat(name[i], dummy );
dummy[0] = '0';
strcat(name[i], "," );
dummy[0] = second_name[i][0];
strcat(name[i], dummy );
strcat(name[i], "," );
strcat(name[i], telephone[i]);
}
 /* Alphabetical ordering of surnames */
for(i=1; i <= CUSTOMERS-1; i++)
for(j=1; j < CUSTOMERS; j++)
if (strcmp(name[i], name[j]) < 0)
{
strcpy(dummy, name[i]);
strcpy(name[i], name[j]);
strcpy(name[j], dummy);
}
printf("The revised list is \n");
for(i=0; i < CUSTOMERS; i++)
printf("%s \n", name[i]);
}
```