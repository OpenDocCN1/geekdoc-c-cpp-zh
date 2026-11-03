Suppose the path of first file is entered as-
c:\mydir\myfile.dat

```
(4) main()
{
    FILE *fptr;
    int ch;
    fptr=fopen("names.dat",'w');
    while((ch=fgetc(fptr))!=EOF)
        putchar(ch);
    fclose(fptr);
}
```

```
(5) main()
{
    char name[50];
    int empid;
    fprintf(stdout,"Enter your name : ");
    fgets(name,50,stdin);
    printf(stdout,"Enter your empid : ");
    fscanf( stdin,"%d",&empid );
    printf(stdout,"Your empid is : %d", empid);
    fputc('\n',stdout);
    printf(stdout,"Your name is : ");
    fputs(name,stdout);
}
```

```
(6) main()
{
    FILE *fptr;
    char str[80];
    fptr=fopen("test.txt","r");
    while(fgets(str,80,fptr)!=EOF)
        puts(str);
}
```

```
(7) main(int argc,char *argv[ ])
{
    int i, sum=0;
    for(i=1;i<argc;i++)
        sum=sum+argv[i];
    printf("%d\n",sum);
}
```

Suppose the name of executable file is add and on the command line it is invoked as-
add 2 4 6 8

# Programming Exercise

+   1. Write a program to copy a file to another file such that blank lines are not written to the new file.
+   2. Write a program to convert all the lower case characters of a file to upper case.