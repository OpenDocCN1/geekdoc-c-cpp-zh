
The feof() function returns non-zero, if the file associated with fp has reached the end of file, otherwise it returns 0. This function works for both binary files and text files. The ferror() function returns non-zero if the file associated with fp has experienced an error, otherwise it returns 0.

The fwrite() function is the opposite of fread(). It writes to file associated with fp, num number of objects, each object size in bytes, from the buffer pointed to by buffer. It returns the number of objects written. This value will be less than num only if an output error has occurred. To check for errors, fwrite() is usually programmed as follows:

```c
if((fwrite(buffer, size, num, fp)) != num)
    fprintf(stderr, "Error writing to file.");
```

The following program describes the use of fread() and fwrite() functions. The program initializes an array. Then, the fwrite() function is used to save the array to disk. After that, the fread() function is used to read the data into a different array. Finally, it displays both the arrays on screen to show that they now hold the same data.

### EXAMPLE

```c
15. #include <stdlib.h>
#include <stdio.h>
#define SIZE 10
int main()
{
    int i, a[SIZE], b[SIZE];
    FILE *fp;
    for(i = 0; i < SIZE; i++)
        a[i] = 2 * i;
    if((fp = fopen("dfile.txt", "wb")) == NULL)
    {
        fprintf(stderr, "Error opening file.");
        exit(1);
    }
    if(fwrite(a, sizeof(int), SIZE, fp) != SIZE)
    {
        fprintf(stderr, "Error writing to file.");
        exit(1);
    }
    fclose(fp);
    if((fp = fopen("dfile.txt", "rb")) == NULL)
    {
        fprintf(stderr, "Error in opening file.");
        exit(1);
    }
    if(fread(b, sizeof(int), SIZE, fp) != SIZE)
    {
        fprintf(stderr, "Error in reading file.");
        exit(1);
    }
    fclose(fp);
    for(i = 0; i < SIZE; i++)
        printf("%d\t%d\n", a[i], b[i]);
    return 0;
}
```

```text
Output
0 0
2 2
4 4
6 6
8 8
10 10
12 12
14 14
16 16
18 18
```

### 15.5.1 Sequential Versus Random File Access

Every open file has an associated file position indicator, which describes where read and write operations take place in the file. The position is always specified in bytes from the beginning of the file. When a new file is opened, the position indicator is always at the beginning of the file, i.e., at position 0. Because the file is new and has a length of 0, there is no other location to indicate. When an existing file is opened, the position indicator is at the end of the file if the file was opened in the append mode, or at the beginning of the file if the file was opened in any other mode.

The file I/O functions covered earlier in this chapter make use of the position indicator, although the manipulations go on behind the scenes. Writing and reading operations occur at the location of the position indicator and update the position indicator as well. Thus, if one wishes to read all the data in a file sequentially or write data to a file sequentially, it is not necessary to be concerned about the position indicator because the stream I/O functions take care of it automatically.

When more control is required, the C library functions that help determine and change the value of the file position indicator, have to be used. By controlling the position indicator, random access of a file can be made possible. Here, random means that data can be read from, or written to, any position in a file without reading or writing all the preceding data. This will be covered in the later sections of the chapter.

### Note

- Direct I/O is used only with binary-mode files.
- fread() and fwrite() functions can read and write any type of data, using any kind of representation.
- There are two types of file accessing method—sequential and random.
- Every open file has an associated file position indicator. The position is always specified in bytes from the beginning of the file.

## 15.6 FILES OF RECORDS

Most C program files may be binary files, which can logically be divided into fixed-length records. Each record will consist of data that conforms to a previously defined structure. In C, this structure can be formed using a `struct` data type. The records are written into disk sequentially. This happens because as each record is written to disk, the file position indicator is moved to the byte immediately after the last byte in the record just written. Binary files can be written sequentially to the disk or in a random access manner.

### 15.6.1 Working with Files of Records

**Using `fscanf()` and `fprintf()`** The following structure records the code, name, and price of an item. Using this structure, a file of records can be processed. Here, 0 is used as end-of-file marker (logically) to indicate there are no records in the file.

### EXAMPLE

```c
16. #include <stdio.h>
struct item
{
    int itemcode;
    char name[30];
    double price;
};
void append();
void modify();
void dispall();
void dele();
int main()
{
    int ch;
    struct item it;
    FILE *fp;
    fp=fopen("item.dat","w");
    if(fp==NULL)
    {
        printf("\n ERROR IN OPENING FILE...");
        exit(0);
    }
    printf("\n ENTER ITEM CODE:");
    scanf("%d",&it.itemcode);
    printf("\n ENTER ITEM NAME:");
    fflush(stdin);
    scanf("%[^\n]",it.name);
    printf("\n ENTER PRICE:");
    scanf("%lf",&it.price);
    fprintf(fp,"%d |\t%s|\t%f\n",it.itemcode,
            it.name,it.price);
    fprintf(fp,"%d",0);
    fclose(fp);
    while(1)
    {
        printf("\n \t 1.APPEND RECORD");
        printf("\n \t 2.DISPLAY ALL RECORD");
        printf("\n \t 3.EDIT RECORD");
        printf("\n \t 4.DELETE RECORD");
        printf("\n \t 5.EXIT");
        printf("\n \t ENTER UR CHOICE:");
        scanf("%d",&ch);
        switch(ch)
        {
            case 1:append(); break;
            case 2:dispall(); break;
            case 3:modify(); break;
            case 4:dele(); break;
            case 5:exit(0);
        }
    }
    return 0;
}

void append()
{
    FILE *fp;
    struct item it;
    fp=fopen("item.dat","a");
    if(fp==NULL)
    {
        printf("\n ERROR IN OPENING FILE...");
        exit(0);
    }
    printf("\n ENTER ITEM CODE:");
    scanf("%d",&it.itemcode);
    printf("\n ENTER ITEM NAME:");
    fflush(stdin);
    scanf("%[^\n]",it.name);
    printf("\n ENTER PRICE:");
    scanf("%lf",&it.price);
    fprintf(fp,"%d |\t%s|\t%f\n",it.itemcode,
            it.name,it.price);
    fprintf(fp,"%d",0);
    fclose(fp);
}

void dispall()
{
    FILE *fp;
    struct item it;
    fp=fopen("item.dat","r");
    if(fp==NULL)
    {
        printf("\n ERROR IN OPENING FILE...");
        exit(0);
    }
    while(1)
    {
        fscanf(fp, "%d",&it.itemcode);
        if(it.itemcode==0)
            break;
        fscanf(fp,"%s",it.name);
        fscanf(fp,"%lf",&it.price);
        printf("\n \t %d\t%s\t%lf",it.itemcode,
                              it.name,it.price);
    }
    fclose(fp);
}
void modify()
{
    FILE *fp,*fptr;
    struct item it;
    int icd,found=0;
    fp=fopen("item.dat","r");
    if(fp==NULL)
    {
        printf("\n ERROR IN OPENING FILE...");
        exit(0);
    }
    fptr=fopen("temp.dat","w");
    if(fptr==NULL)
    {
        printf("\n ERROR IN OPENING FILE...");
        exit(0);
    }
    printf("\n ENTER THE ITEM CODE TO EDIT");
    scanf("%d",&icd);
    while(1)
    {
        fscanf(fp,"%d",&it.itemcode);
        if(it.itemcode==0)
            break;
        if(it.itemcode==icd)
        {
            found=1;
            fscanf(fp,"%s",it.name);
            fscanf(fp,"%lf",&it.price);
            printf("\n EXISTING RECORD IS...\n");
            printf("\n \t %d\t%s\t%lf",it.itemcode,
                          it.name,it.price);
            printf("\n ENTER NEW ITEM NAME:");
            fflush(stdin);
            scanf("%[^\n]",it.name);
            printf("\n ENTER NEW PRICE:");
            scanf("%lf",&it.price);
            fprintf(fptr,"%d \t%s\t%lf\n",
                it.itemcode,it.name,it.price);
        }
        else
        {
            fscanf(fp,"%s",it.name);
            fscanf(fp,"%lf",&it.price);
            fprintf(fptr,"%d \t%s\t%lf\n",
                it.itemcode,it.name,it.price);
        }
    }
    fprintf(fptr,"%d",0);
    fclose(fptr);
    fclose(fp);
    if(found==0)
        printf("\nRECORD NOT FOUND...");
    else
    {
        fp=fopen("item.dat","w");
        if(fp==NULL)
        {
            printf("\n ERROR IN OPENING FILE...");
            exit(0);
        }
        fptr=fopen("temp.dat","r");
        if(fptr==NULL)
        {
            printf("\n ERROR IN OPENING FILE...");
            exit(0);
        }
        while(1)
        {
            fscanf(fptr,"%d",&it.itemcode);
            if(it.itemcode==0)
                break;
            fscanf(fptr,"%s",it.name);
            fscanf(fptr,"%lf",&it.price);
            fprintf(fp,"%d \t%s\t%lf\n",it.itemcode,
                it.name,it.price);
        }
        fprintf(fp,"%d",0);
        fclose(fptr);
        fclose(fp);
    }
}
```
