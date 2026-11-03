
Position ———→ 0 1 2 ........ 25
Character
stored ———→ A B C ........ Z

We read the file twice. First, we read the contents of every fifth position and print its value along with its position on the screen. The second time, we read the contents of the file from the end and print the same on the screen.

During the first reading, the file pointer crosses the end-of-file mark when the parameter n of fseek (fp,n,0) becomes 30. Therefore, after printing the content of position 30, the loop is terminated. (There is nothing in the position 30.)

For reading the file from the end, we use the statement

```
fseek(fp, -1L,2);
```

to position the file pointer to the last character. Since every read causes the position to move forward by one position, we have to move it back by two positions to read the next character. This is achieved by the function

```
fseek(fp, -2L, 1);
```

in the while statement. This statement also tests whether the file pointer has crossed the file boundary or not. The loop is terminated as soon as it crosses it.

```
Program
/*************************************************/
/*************************************************/
/* ILLUSTRATION OF fseek & ftell FUNCTIONS */
/*************************************************/

#include <stdio.h>
main()
{
 FILE *fp;
 long n;
 char c;
 fp = fopen("RANDOM", "w");
 while((c=getchar())!=EOF)
 putc(c,fp);
 printf("No. of characters entered = %ld\n", ftell(fp));
 fclose(fp);
 fp = fopen("RANDOM", "r");
 n = 0L;
 while(feof(fp) == 0)
 {
 fseek(fp, n, 0); /* Position to (n+1)th character */
 printf("Position of %c is %ld\n", getc(fp), ftell(fp));
 n = n+5L;
 }
 putchar('\n');
 fseek(fp, -1L,2); /* Position to the last character */
 do
 {
 putchar(getc(fp));
}
while(fseek(fp,-2L,1));
fclose(fp);
}
Output
ABCDEFGHIJKLMNOPQRSTUVWXYZ
No. of characters entered = 26
Position of A is 0
Position of F is 5
Position of K is 10
Position of P is 15
Position of U is 20
Position of Z is 25
Position of ? is 30
ZYXWVUTSRQPONMLKJIHGFEDCBA
```

Fig. 13.6 Illustration of fseek and ftell functions

## 13.7 COMMAND LINE ARGUMENTS

What is a command line argument? It is a parameter supplied to a program when the program is invoked. This parameter may represent a filename the program should process. For example, if we want to execute a program to copy the contents of a file named X_FILE to another one named Y_FILE, then we may use a command line like

```
C>PROGRAM X_FILE Y_FILE
```

PROGRAM is the filename where the executable code of the program is stored. This eliminates the need for the program to request the user to enter the filenames during execution. How do these parameters get into the program? We know that every C program should have one main function and that it marks the beginning of the program. But what we have not mentioned so far is that it can also take arguments like other functions. In fact main can take two arguments called argc and argv and the information contained in the command line is passed on to the program through these arguments, when main is called up by the system. The variable argc is an argument counter that counts the number of arguments on the command line. The argv is an argument vector and represents an array of character pointers that point to the command line arguments. The size of this array will be equal to the value of argc. For instance, for the command line given above, argc is three and argv is an array of three pointers to strings as shown below:

```
argv[0] ------> PROGRAM
argv[1] ------> X_FILE
argv[2] ------> Y_FILE
```

In order to access the command line arguments, we must declare the main function and its parameters as follows:

```
main(argc, argv)
int argc;
char *argv[];
{
    ....
    ....
}
```

The first parameter in the command line is always the program name and therefore argv[0] always represents the program name.

## Example 13.5

Write a program that will receive a filename and a line of text as command line arguments and write the text to the file.

Figure 13.7 shows the use of command line arguments. The command line is

F12_6 TEXT AAAAA BBBBBB CCCCCC DDDDDD EEEEEE FFFFFF GGGGGG.

Each word in the command line is an argument to the main and therefore the total number of arguments is 9.

The argument vector argv[1] points to the string TEXT and therefore the statement

```
fp = fopen(argv[1], "w");
```

opens a file with the name TEXT. The for loop that follows immediately writes the remaining 7 arguments to the file TEXT.

Program also prints two outputs, one from the file TEXT and the other from the system memory. The argument vector argv contains the entire command line in the memory and, therefore, the statement:

```
printf("%s\n", argv[i]);
```

prints the arguments from the memory.

```
Program
/*.........................................................................*/
/* COMMAND LINE ARGUMENTS */
/*.........................................................................*/

#include <stdio.h>
main(argc, argv)    /* main with arguments */
int argc;           /* argument count */
char *argv[];       /* list of arguments */
{
    FILE *fp;
    int i;
    char word[15];
    fp = fopen(argv[1], "w");    /* open file with name argv[1] */
    printf("\nNo. of arguments in Command line = %d\n", argc);
    for(i = 2; i < argc; i++)
        fprintf(fp, "%s ", argv[i]);    /* write to file argv[1] */
    fclose(fp);
    /* Writing content of the file to screen */
    printf("Contents of %s file\n", argv[1]);
    fp = fopen(argv[1], "r");
    for(i = 2; i < argc; i++)
{
    fscanf(fp, "%s", word);
    printf("%s", word);
}
fclose(fp);
printf("\n");
/* Writing the arguments from memory          */
for(i = 0; i < argc; i++)
    printf("%s\t\n", argv[i]);
}
Output
C:\F12_6 TEXT AAAAAA BBBBBB CCCCCC DDDDDD EEEEEE FFFFFF GGGGGG
No. of arguments in Command line = 9
Contents of TEXT file
AAAAAA BBBBBB CCCCCC DDDDDD EEEEEE FFFFFF GGGGGG
C:\F12_6.EXE
TEXT
    AAAAAA
        BBBBBB
            CCCCCC
                DDDDDD
                    EEEEEE
                        FFFFFF
                            GGGGGG
```

Fig. 13.7 Use of command line arguments

## CASE STUDY

### Appending Items to a File

A program to append additional items to the file INVENTORY and print the total contents of the file has been developed here. The program is shown in Fig. 13.8. It uses a structure definition to describe each item and a function append () to add an item to the file.

On execution, the program requests for the filename to which data is to be appended. After appending the items, the position of the last character in the file is assigned to n and then the file is closed.

The file is reopened for reading and its contents are displayed. Note that reading and displaying are done under the control of a while loop. The loop tests the current file position against n and is terminated when they become equal.

```
Program
/* ************************************************************/
/*      APPENDING ITEMS TO AN EXISTING FILE                   */
/* ************************************************************/
#include <stdio.h>
struct invent_record
{
    char name[10];
    int  number;
    float price;
    int  quantity;
};
main()
{
    struct invent_record item;
    char filename[10];
    int  response;
    FILE *fp;
    long n;
    printf("Type filename:");
    scanf("%s", filename);
    fp = fopen(filename, "a+");
    do
    {
        append(&item, fp);
        printf("\nItem %s appended \n",item.name);
        printf("\nDo you want to add another item \\(1 for YES /0 for NO)?");
        scanf( "%d", &response);
    } while (response == 1);
    n = ftell(fp);        /* Position of last character */
    fclose(fp);
    fp = fopen(filename, "r");
    while(ftell(fp) < n)
    {
        fscanf(fp, "%s %d %f %d",
        item.name, &item.number, &item.price, &item.quantity);
        printf("%8s %7d %7.2f %8d\n",
        item.name, item.number, item.price, item.quantity);
    }
    fclose(fp);
}
append(product, ptr)
struct invent_record *product;
FILE  *ptr;
{
    printf("Item name:");
    scanf("%s", product->name);
    printf("Item number:");
    scanf("%d", &product->number);
    printf("Item price:");
    scanf("%f", &product->price);
    printf("Quantity:");
    scanf("%d", &product->quantity);
    fprintf(ptr, "%s %d %f %d",
    product->name,
    product->number,
    product->price,
    product->quantity);
}
```
