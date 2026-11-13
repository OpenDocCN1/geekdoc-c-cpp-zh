```
printf("\n 3. Count lines, words, characters");
printf("*\n 4. Copy file");
printf("*\n 5. Exit");
printf("*\nEnter your choice");
scanf("%d", &choice);
switch(choice)
{
case 1: fobj.create();
break;
case 2: fobj.display();
break;
case 3: fobj.count();
break;
case 4:
char dfname[30];
cout << "\nEnter the destination filename : ";
cin >> dfname;
fobj.copy(dfname);
fobj.display(dfname);
break;
case 5: exit(0);
}
}while(choice < 5);
getch();
}
```

# 14.5 SEQUENTIAL FILE ORGANIZATION

A sequential file stores records in the order they are entered. The order of the records is fixed. The records are stored and sorted in physical, contiguous blocks. Within each block, the records are in sequence. New records always appear at the end of the file. Therefore, the record found in the first position is the oldest record and the last record in the file is the one most recently added. Records in these files can only be read or written sequentially. Records may be either fixed or variable in length for this file type. This is a significant advantage of sequential files. However the search time associated with sequential files is more because records are accessed sequentially from the beginning of the file. Sequential files are compatible to the magnetic tape storage as shown in the following figure.

| Record 1 | Record 2 | Record 3 | Record 4 | Record 5 | ... | ... | End |
|---|---|---|---|---|---|---|---|