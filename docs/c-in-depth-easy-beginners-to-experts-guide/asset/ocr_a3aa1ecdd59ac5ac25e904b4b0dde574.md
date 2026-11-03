```
printf("\n File doesn't exixt");
exit(1);
}
fscanf(fp,"%s",str);
printf("\n file contains...");
puts(str);
fclose(fp);
getch();
}
```

# 111. Wap to read 'n' names from user and store them into a file also create a copy of it into another file.

```
#include<stdio.h>
#include<conio.h>
#include<stdlib>
#include<string.h>
void main()
{
    FILE *fp1,*fp2;
    char str[20];
    int i,n;

    fp1=fopen("file1.txt","w+");
    printf("\n How many names u want to Enter");
    scanf("%d",&n);

    for(i=0;i<n;i++)
    {
        printf("\n Enter the name");
        gets(str);
        fprintf(fp1,"\n %s",str);
    }

    rewind(fp1);
    fp2=fopen("file2.txt","w");
    while(!feof(fp1))
    {
        fscanf(fp1,"\n %s",str); /*read from first file */
```