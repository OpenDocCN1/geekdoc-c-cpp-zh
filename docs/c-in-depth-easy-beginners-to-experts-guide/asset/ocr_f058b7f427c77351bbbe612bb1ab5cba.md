```
}
fclose(fp);
printf("number of lines = %d\ntabs = %d\ncharacters = %d\nspaces = %d",lines,characters,spaces);
getch();
}
```

# 2. Write a program to receive some strings from keyboard and print it to a file

```
#include<stdio.h>
main()
{
    FILE *fp;
    char s[50];
    fp=fopen("text.c","w");        /*opening file*/
    if(fp==NULL)                   /*to check opening errors*/
    {
        puts("file opening error");
        exit();
    }
    printf("Enter some text");
    while(strlen(gets(s))>0)
    {
        fputs(s,fp);
        fputs("\n",fp);
    }
    fclose(fp);
}
```

# 3. Write a program to read all the strings from file and print it on screen

```
#include<stdio.h>
main()
{
    FILE *fp;
```