
```c
{
    case 1:
        insert(fp);
        break;
    case 2:
        del(fp);
        break;
    case 3:
        display(fp);
        break;
    case 4:
        modify(fp);
        break;
    case 5:
        list(fp);
        break;
    case 6:
        booksold(fp);
        break;
    case 7:
        fclose(fp);
        exit(1);
    default :
        printf("Wrong choice\n");
}/*End of switch */
}/*End of main */
void insert(FILE *fp)
{
    fseek(fp, 0, 2);
    printf("Enter book name : ");
    scanf("%s", book.name);
    printf("Enter number of copies : ");
    scanf("%d", &book.ncopies);
    printf("Enter cost of book : ");
    scanf("%f", &book.cost);
    fwrite(&book, sizeof(book), 1, fp);
}/*End of insert */
void del(FILE *fp)
{
    FILE *fptmp;
    char name[20];
    printf("Enter the name of book to be deleted from database : ");
    scanf("%s", name);
    if(search(fp, name) == 0)
        return;
    fptmp = fopen("tempfile.dat", "wb");
    rewind(fp);
    while(fread(&book, sizeof(book), 1, fp) == 1)
    {
        if(strcmp(name, book.name) != 0)
            fwrite(&book, sizeof(book), 1, fptmp);
    }
    fclose(fp);
    fclose(fptmp);
    remove("books.dat");
    rename("tempfile.dat", "books.dat");
    printf("\nRecord deleted.......\n\n");
    fp = fopen("books.dat", "rb+");
}/*End of del()*/

void modify(FILE *fp)
{
    char name[50];
    long size = sizeof(book);
    printf("Enter the name of the book to be modified : ");
    scanf("%s", name);
    if(search(fp, name) == 1)
    {
        printf("Enter new data-->\n\n");
        printf("Enter book name : ");
        scanf("%s", book.name);
        printf("Enter number of copies : ");
        scanf("%d", &book.ncopies);
        printf("Enter cost of book : ");
        scanf("%f", &book.cost);
        fseek(fp, -size, 1);
        fwrite(&book, sizeof(book), 1, fp);
        printf("\nRecord successfully modified\n\n");
    }
}/*End of modify()*/

void booksold(FILE *fp)
{
    char name[50];
    long size = sizeof(book);
    printf("Enter the name of the book to be sold : ");
    scanf("%s", name);
    if(search(fp, name) == 1)
    {
        if(book.ncopies > 0)
        {
            book.ncopies--;
            fseek(fp, -size, 1);
            fwrite(&book, sizeof(book), 1, fp);
            printf("One book sold\n");
            printf("Now number of copies = %d\n", book.ncopies);
        }
        else
            printf("Book is out of stock\n\n");
    }
}
/*End of booksold()*/
void display(FILE *fp)
{
    char name[50];
    printf("Enter the name of the book : ");
    scanf("%s", name);
    search(fp, name);
    printf("\nName\t%s\n", book.name);
    printf("Copies\t%d\n", book.ncopies);
    printf("Cost\t%f\n\n", book.cost);
}
/*End of display()*/
int search(FILE *fp, char *name)
{
    unsigned flag = 0;
    rewind(fp);
    while(fread(&book, sizeof(book), 1, fp) == 1)
    {
        if(strcmp(name, book.name) == 0)
        {
            flag = 1;
            break;
        }
    }
    if(flag == 0)
        printf("\nName not found in file\n\n");
    return flag;
}
/*End of search()*/
void list(FILE *fp)
{
    rewind(fp);
    printf("\nNAME\tCOPIES\t\tCOST\n\n");
    while(fread(&book, sizeof(book), 1, fp) == 1)
    {
        printf("%s\t", book.name);
        printf("%d\t\t", book.ncopies);
        printf("%f\n", book.cost);
    }
    printf("\n");
}
/*End of list()*/
```

We have opened the file books.dat in update(rb+) mode. If the file doesn't exist then fopen() will return NULL, so we'll create the file by opening in "wb+" mode. So first time when we'll run this program, file will be opened in "wb+" mode. The operations permitted in "wb+" mode and "rb+" mode are same but the problem with "rb+" mode is that it can't create a file and with "wb+" mode is that it erases the contents of the file each time file is opened.

The function insert( ) is simple, we place the position pointer at the end of file by fseek( ) and then insert a new record there.

The function search( ) searches for a record in the file, and if the record does not exist then it displays a message and returns 0. If the record exists then the position pointer is placed at the end of the record, which was searched and the function returns 1. Before starting our search we have called rewind( ) function so that search starts from the beginning of the file. This function search( ) is used in del( ), modify, booksold( ) and display( ) functions.

The del( ) function first calls search( ), and if the record doesn't exist we return from the function. Otherwise the record is deleted using a temporary file as we have seen earlier. At the end of del( ) function the file books.dat is opened in "rb+" mode because this file was closed by this function, and it is the responsibility of this function to open the file in "rb+" before returning to main menu and performing any other operation.

The function modify( ) is simple. The function booksold( ) searches for the book to be sold and it reduces the number of copies by 1. If the number of copies is 0 then it displays the message that book is out of stock. For reducing number of copies we have written book.ncopies--. We could write this because book is a global variable and after calling search( ) it contains the record of the book to be sold.

The function display( ) searches for a particular record and displays its details on the screen while the function list( ) displays the details of the all the books on the screen.

## 11.14 Other File Functions

### 11.14.1 feof( )

So far we have used the return value of the function to detect the end of file while reading. For example fgetc( ), getc( ), getw( ), fprintf( ) return EOF and fgets( ) returns NULL on end of file. But these functions return the same value both on end of file and on error. So if a function stops reading we can't make out whether the end of file was reached or an error was encountered. We can check separately for these two conditions with the help of ferror( ) and feof( ).

Declaration: int feof( FILE *fptr );

The macro feof( ) is used to check the end of file condition. It returns a nonzero value if end of file has been reached otherwise it returns zero.

In the program P11.11 we could have used feof( ) function to read the file.

```c
fread(&student, sizeof(student), 1, fp);
while(!feof(fp))
{
    printf("%s\t", student.name);
    printf("%d\t", student.roll);
    printf("%f\n", student.marks);
    fread(&student, sizeof(student), 1, fp);
}
```

Let us see what would happen if we write the above code like this-

```c
while(!feof(fp))
{
    fread(&student, sizeof(student), 1, fp);
    printf("%s\t", student.name);
}
printf("%d\t", student.roll);
printf("%f\n", student.marks);
}
```

In this case, the last record of the program may be processed twice, since in C end of file is indicated only after an input function has made an attempt to read at the end of file.

### 11.14.2 ferror()

Declaration: int ferror(FILE *fptr);

The macro ferror() is used for detecting any error occurred during read or write operations on a file. It returns a nonzero value if an error occurs i.e. if the error indicator for that file is set, otherwise it returns zero.

```c
/*P11.22 Program to understand the use of ferror()*/
#include<stdio.h>
main()
{
    FILE *fptr;
    int ch;
    fptr = fopen("test", "w");
    ch = getc(fptr);
    if(ferror(fptr))
    {
        printf("Error in read operation\n");
        exit(1);
    }
    else
        printf("%c", ch);
    fclose(fptr);
}
```

### Output:

Error in read operation

Here the file is opened in write mode and an attempt is made to read from the file, this gives an error which is detected by ferror().

Generally the return value of the input function is checked to stop reading from the file. Almost all input functions return same value on end of file and on error, so to distinguish between these two cases, the functions feof() and ferror() are used.

```c
/*P11.23 Program to understand the use of feof() and ferror()*/
#include<stdio.h>
main()
{
    FILE *fptr;
    int ch;
    if((fptr = fopen("myfile.c", "r")) == NULL)
    {
        printf("File doesn't exist\n");
        exit(1);
    }
    else
    {
        while((ch = getc(fptr)) != EOF)
            printf("%c", ch);
    }
    if(feof(fptr))
        printf("End of file\n");
    if(ferror(fptr))
        printf("Error\n");
    fclose(fptr);
}
```

### 11.14.3 clearerr( )

Declaration: void clearerr(FILE *fptr);

This function is used to set the end of file and error indicators to 0.

```c
/*P11.24 Function to understand the use of clearerr()*/
#include<stdio.h>
main()
{
    FILE *fptr;
    int ch;
    fptr = fopen("test", "w");
    ch = getc(fptr);
    if(ferror(fptr))
    {
        printf("Error in read operation\n");
        clearerr(fptr);
    }
    fclose(fptr);
}
```

### 11.14.4 perror( )

Declaration: void perror(const char *str);

This function is used to display a message supplied by the user along with the error message generated by the system. It prints the argument str, then a colon, then the message related to the current value of errno, and then a newline. errno is a global variable which is set to a particular value whenever an error occurs. The use of this function can be understood by reading the next program P11.25.

### 11.14.5 rename( )

Declaration: int rename(const char *oldname, const char *newname);

This function is used to rename a file. We can give full path also in the argument, but the drives should be the same although directories may differ. On success it returns 0 and on error it returns -1 and errno is set to one of these values-

| Code | Meaning |
|------|---------|
| ENOENT | No such file or directory |
| EACCES | Permission denied |
| ENOTSAM | Not same device |
