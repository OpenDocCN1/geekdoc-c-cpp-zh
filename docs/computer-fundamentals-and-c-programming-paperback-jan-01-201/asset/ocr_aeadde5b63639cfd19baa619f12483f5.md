```
```c
if ((fp = fopen("student.dat", "rb+")) == NULL) {   /* wb+ would ... */
    perror("student.dat");                             /* ... overwrite file */
    exit(1);
}

size = sizeof(struct student);                         /* Size of each record */
fseek(fp, 0, SEEK_END);
records = ftell(fp) / size;
fprintf(stderr, "Number of records available = %d\n", records);

fputs("Enter roll no and new marks: ", stderr);
scanf("%d%d", &s_roll_no, &s_marks);
rewind(fp);
for (i = 0; i < records; i++) {                        /* Start search */
    fread(&stud, size, 1, fp);
    if (stud.roll_no == s_roll_no) {                   /* If record located ... */
        found = 1;
        stud.marks = s_marks;                           /* ... update the member. */
        fseek(fp, -size, SEEK_CUR);                     /* Go back to that record ... */
        fwrite(&stud, size, 1, fp);                     /* ... and update file. */
        break;                                          /* No need to search further */
    }
}

if (found == 1) {
    rewind(fp);
    fputs("Record updated. Displaying all records ...\n\n", stderr);
    for (i = 0; i < records; i++) {
        fread(&stud, size, 1, fp);
        printf("%s %d %d\n", stud.name, stud.roll_no, stud.marks);
    }
}
else
    fputs("Record not found\n", stderr);
fclose(fp);
exit(0);
}
```
```

# PROGRAM 15.14: **update_structure.c**

```
```text
Number of records available = 5
Enter roll no and new marks: 2345 5432
Record updated. Displaying all records ...

Narciso Yepes 1234 666
Andres Segovia 4567 555
Sergio Abreu 8910 999
Celedonio Romero 2345 5432
Leo Brouwer 6789 888

Record updated on disk
```
```

# PROGRAM OUTPUT: **update_structure.c**