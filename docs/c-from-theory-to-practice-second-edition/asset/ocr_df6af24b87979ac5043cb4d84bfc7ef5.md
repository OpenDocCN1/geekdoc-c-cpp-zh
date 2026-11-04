```
if(fp == NULL)
{
    printf("Error: fopen() failed\n");
    exit(EXIT_FAILURE);
}
while(1)
{
    printf("\nMenu selections\n");
    printf("------------------\n");

    printf("1. Add Book\n");
    printf("2. Find Book\n");
    printf("3. Modify Book \n");
    printf("4. Erase Book\n");
    printf("5. Exit\n");

    printf("\nEnter choice: ");
    scanf("%d", &sel);
    getchar();

    switch(sel)
    {
    case 1:
        read_data(&b);
        fseek(fp, 0, SEEK_END); /* Add the book at the
        end of the file. */
        fwrite(&b, sizeof(book), 1, fp);
        break;

    case 2:
        printf("\nTitle to search: ");
        read_text(title, sizeof(title), 1);
        if(strcmp(title, "**") != 0)
            find_book(fp, title);
        else
            show_books(fp);
        break;

    case 3:
        read_data(&b);
        modify_book(fp, &b, 0);
        break;

    case 4:
        printf("\nTitle to search: ");
        read_text(b.title, sizeof(b.title), 1);
        modify_book(fp, &b, 1);
        break;

    case 5:
        fclose(fp);
        return 0;
    }
```