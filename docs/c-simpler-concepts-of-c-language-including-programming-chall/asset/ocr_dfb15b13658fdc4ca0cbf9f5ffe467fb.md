# FILE HANDLING IN C

```
case 3:
    printf("Want to write(0) or append(1) or wanna use fprintf(2) or/
    fputs(0) or putw(4)??\n");
    scanf("%d", &option);
    printf("Enter the file name with extension..\n");
    scanf("%s", &file_name);
    if (option==0)
    {
        out=fopen(file_name,"w");
        if (out==NULL)
            printf("Cannot open such file..\n");
        else
        {
            printf("Enter the contents of the file (Press * to stop ending).\n");
            while ((c=getchar()) != '*')
                putc (c, out);
        }
    }
    else if (option==1)
    {
        out=fopen(file_name,"a");
        if (out==NULL)
            printf("Cannot open such file..\n");
        else
        {
            printf("Enter the contents of the file (Press * to stop ending).\n");
            while ((c=getchar()) != '*')
                putc (c, out);
        }
    }
    else if (option==3)
    {
        out=fopen(file_name,"w");
        if (out==NULL)
            printf("Cannot open such file..\n");
        else
        {
            printf("Enter the word..\n");
            scanf("%s", &word);
            fputs (word, out);
        }
    }
    else if (option==4)
    {
        in=fopen(file_name,"w");
        for(i=100;i<=110;i++)
            putw(i,in);
        fclose (in);
        printf("Written successfully!\n");
    }
```

Program 10.1 File operations-part III