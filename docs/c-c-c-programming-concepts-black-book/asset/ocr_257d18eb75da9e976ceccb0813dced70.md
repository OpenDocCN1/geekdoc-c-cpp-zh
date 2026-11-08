```
```c
rewind(fp);
fd = fopen("D:\\temp.dat","wb");
printf("\n Enter Student Name for Deletion -> ");
gets(tempName);
while(fread(&stu, sizeof(stu), 1, fp))
{
    if(strcmp(tempName,stu.name))
    {
        fwrite(&stu, sizeof(stu), 1, fd);
    }
}
fclose(fp);
fclose(fd);
remove("D:\\studentRecords.dat");
rename("D:\\temp.dat","D:\\studentRecords.dat");
fp = fopen("D:\\studentRecords.dat","rb+");
break;
default:break;
}while(choice != 5);

fclose(fp);
getch();
return 0;
}
```
```

Output of the preceding program is as follows:

```
```text
1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 1

Enter Name Class Age ->BRIAN 1 5

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 1

Enter Name Class Age ->CRISTINA 2 6

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 2

BRIAN 1 5
CRISTINA 2 6
1. Add records to a file
2. Display Records
```
```