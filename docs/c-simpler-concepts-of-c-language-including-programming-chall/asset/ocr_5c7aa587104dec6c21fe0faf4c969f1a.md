# FILE HANDLING IN C

```
fclose(fptr);
}
else
printf("FILE OPEN FAILED");
choice=0;
fptr=fopen(file_name,"r");
while((c=fgets(fptr))!=EOF)
{
    if(c=='\n')
    {
        if(sum<2)
            choice=ftell(fptr);
            fseek(out,1L,SEEK_CUR);
            putc('\n',out);
    }
    sum=0;
    }
    i=isowel(c);
    if(i==1)
    {
        sum+=1;
    }
    if(sum>=2)
    {
        option=ftell(fptr);
        fseek(fptr,choice-option,SEEK_CUR);
        while((c=fgets(fptr))!=''.')
        {
            putc(c,out);
        }
        choice=ftell(fptr);
    }
}
fclose(fptr);
fclose(out);
in=fopen("file_test.txt","r");
if(in==NULL)
printf("File open failed..");
```