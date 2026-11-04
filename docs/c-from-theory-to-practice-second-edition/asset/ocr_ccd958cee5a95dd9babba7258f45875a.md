```
printf("Authors: ");
len = read_text(str, sizeof(str), 1);
books_ptr[i].auth = (char*) malloc(len+1);
strcpy(books_ptr[i].auth, str);

printf("Code: ");
len = read_text(str, sizeof(str), 1);
books_ptr[i].code = (char*) malloc(len+1);
strcpy(books_ptr[i].code, str);

printf("Price: ");
scanf("%f", &books_ptr[i].prc);

getchar();
/* Allocate memory to store the data of the publishing firm. */
books_ptr[i].pub_ptr = (pub*) malloc(sizeof(pub));

printf("Name: ");
len = read_text(str, sizeof(str), 1);
(books_ptr[i].pub_ptr)->name = (char*)malloc(len+1);
strcpy((books_ptr[i].pub_ptr)->name, str);

printf("Address: ");
len = read_text(str, sizeof(str), 1);
(books_ptr[i].pub_ptr)->addr = (char*)malloc(len+1);
strcpy((books_ptr[i].pub_ptr)->addr, str);

printf("Phone: ");
len = read_text(str, sizeof(str), 1);
(books_ptr[i].pub_ptr)->phone = (char*)malloc(len+1);
strcpy((books_ptr[i].pub_ptr)->phone, str);
}
printf("\nEnter code to search: ");
read_text(str, sizeof(str), 1);

for(i = 0; i < num; i++)
{
    if(strcmp(books_ptr[i].code, str) == 0)
    {
        printf("\nTitle: %s\tPublisher: %s\n\n", books_ptr[i].title, (books_ptr[i].pub_ptr)->name);
        break;
    }
}
if(i == num)
    printf("\nCode '%s' isn't registered\n", str);

for(i = 0; i < num; i++)
{
    free((books_ptr[i].pub_ptr)->name);
    free((books_ptr[i].pub_ptr)->addr);
    free((books_ptr[i].pub_ptr)->phone);
```