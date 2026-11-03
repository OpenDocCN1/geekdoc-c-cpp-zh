```
```c
get(quantity);
if(atoi(quantity) < book[index].quantity)
    printf("Cost of %d copies is %.2f\n",atoi(quantity),
        book[index].price * atoi(quantity));
else
    printf("\nRequired copies not in stock\n\n");
}
printf("\nBook not in list\n\n");
printf("\nDo you want any other book? (YES / NO):");
get(response);
}
while(response[0] == 'Y' || response[0] == 'y');
printf("\n\nThank you. Good bye!\n");
}
void get(char string [] )
{
    char c;
    int i = 0;
    do
    {
        c = getchar();
        string[i++] = c;
    }
    while(c != '\n');
    string[i-1] = '\0';
}

int look_up(struct record table[],char s1[],char s2[],int m)
{
    int i;
    for(i = 0; i < m; i++)
        if(strcmp(s1, table[i].title) == 0 &&
            strcmp(s2, table[i].author) == 0)
            return(i);          /* book found */
    return(-1);                 /* book not found */
}
```
```

# Output

Enter title and author name as per the list
Title: BASIC
Author: Balagurusamy
Balagurusamy BASIC 30.00 January 1984 TMH
Enter number of copies:5
Required copies not in stock
Do you want any other book? (YES / NO):y
Enter title and author name as per the list
Title: COBOL
Author: Balagurusamy
Balagurusamy COBOL 60.00 December 1988 Macmillan
Enter number of copies:7