```
```c
{
    puts("File cannot be opened.");
    exit(0);
}
k=*argv[2]-48;
n = fread(a,1,k,fp);
a[n]='\0';
len=strlen(a);
for(i=len-1;i>=0;i--)
{
    s[j]=a[i];
    printf("%c",s[j]);
    j=j+1;
}
s[j+1]='\0';
getch();
}
```
```

+   b) Refer Section 8.2 and 8.5.3