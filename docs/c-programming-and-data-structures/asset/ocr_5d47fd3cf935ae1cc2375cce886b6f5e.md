```
void main()
{
FILE *fs,*ft;/*Declaring file access pointers*/
char str[100];
int i;
clrscr();

fs = fopen("Source.txt","r");/*Opening the source file in read mode*/
if(fs==NULL)
{
printf("Source file cannot be opened.");
exit(0);
}
ft = fopen("Target.txt","w");/*Opening the target file in write mode*/
if (ft==NULL)
{
printf("Target file cannot be opened.");
fclose(fs);
exit(0);
}

i=0;
while(1)
{
str[i]=fgetc(fs);/*Reading contents of Source.txt character by character*/
if (str[i]==EOF)
break;
else
i=i+1;
}

for(i=strlen(str)-2;i>=0;i--)
fputc(str[i],ft);/*Writing the reverse of file contents*/

/*Closing the files*/
fclose(fs);
fclose(ft);

printf("\nContents of Source.txt successfully printed in reverse order in Target.txt");
printf("\nYou can confirm the same by checking the Target.txt file");
getch();
}
```

# Output

Contents of Source.txt successfully printed in reverse order in Target.txt
You can confirm the same by checking the Target.txt file