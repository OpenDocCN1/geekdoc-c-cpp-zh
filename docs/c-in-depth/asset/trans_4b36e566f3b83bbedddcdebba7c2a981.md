
```c
/* P11.9 Program to understand the use of fscanf() */
#include<stdio.h>
struct student
{
    char name[20];
    float marks;
} stu;
main()
{
    FILE *fopen(),*fp;
    fp=fopen("students.dat","r");
    printf("NAME\tMARKS\n");
    while(fscanf(fp,"%s%f",stu.name,&stu.marks)!=EOF)
        printf("%s\t%f\n",stu.name,stu.marks);
    fclose(fp);
}
```

我们之前提到过文件指针 stdout 和 stdin 是自动打开的。如果我们在函数 fprintf() 和 fscanf() 中使用这些文件指针，那么这些函数调用就等同于 printf() 和 scanf()。

如果我们用 stdout 替换文件指针 fp 那么—
fprintf( stdout, "My age is %d", age); 等同于 printf("My age is %d", age);

如果我们用 stdin 替换文件指针 fp 那么—
fscanf(stdin,"%s%d", name, &age); 等同于 scanf("%s%d", name, &age);

## 11.12 块读写

将数据块存储到文件中而不是单个元素是有用的。每个块都有固定的大小，它可以是结构体或数组。很容易从文件中读取整个块或将整个块写入文件。为此有两个有用的函数——fread() 和 fwrite()。虽然我们可以通过这些函数读写从单个字符到数组和结构体的任何类型的数据，但它们主要用于读写结构体和数组。

使用这些函数时，文件通常以二进制模式打开（例如 "wb"、"rb"）。

### 11.12.1 fwrite()

此函数用于将整个块写入给定文件。

声明：size_t fwrite( const void *ptr, size_t size, size_t n, FILE *fptr );

size_t 在 stdio.h 中定义为—
typedef unsigned int size_t;

ptr 是一个指针，它指向包含要写入文件的信息的内存块，size 表示每个项目以字节为长的长度，n 是要写入文件中的项目数，fptr 是一个 FILE 指针，它指向要写入数据的那文件。

如果成功，fwrite( ) 将向文件写入 n 个项目或总共 ( n * size ) 字节并返回 n。在出错或文件结束时它将返回小于 n 的数字。

要将变量 fval 中包含的单个 float 值写入文件

```c
fwrite( &fval, sizeof(float), 1, fp);
```

要将整数数组 arr[10] 写入文件。

```c
fwrite( arr, sizeof(arr), 1, fp);
```

要仅将上述数组的前 5 个元素写入文件

```c
fwrite( arr, sizeof(int), 5, fp);
```

请注意，这里在第三个参数中我们将发送整数的大小，因为这里我们要写入的项目是整数而不是数组。

要写入一个结构体变量，其定义为

```c
struct record{
        char name[20];
        int roll;
        float marks;
        }student;
```

```c
fwrite(&student,sizeof(student),1,fp);
```

这将把单个结构体变量写入文件。

要写入结构体数组

假设 stu_arr[200] 是上面定义的结构体数组—

```c
fwrite( stu_arr, sizeof(stu_arr), 1, fp);
```

这里它将把数组 stu_arr 的全部 200 个元素写入文件。

要仅写入结构体数组的一部分

假设在上述数组 stu_arr[200] 中我们只输入了 100 个学生的记录，那么将整个数组写入文件是没有用的（会写入垃圾值）。我们可以按如下方式写入 100 条记录—

```c
fwrite(stu_arr, sizeof(struct record), 100, fp);
```

我们使用了 sizeof 运算符而不是直接发送大小，这样我们的程序就具有可移植性，因为不同计算机上数据类型大小可能不同。而且如果向我们的结构体添加新元素，我们无需重新计算并更改程序中的大小。

```c
/*P11.10 Program to understand the use of fwrite()*/
#include<stdio.h>
struct record
    {
        char name[20];
        int roll;
        float marks;
    }student;
main()
{
    int i,n;
    FILE *fp;
    fp=fopen("stu.dat","wb");
    if(fp==NULL)
    {
        printf("Error in opening file\n");
        exit(1);
    }

    printf("Enter number of records : ");
    scanf("%d", &n);
    for(i=0;i<n;i++)
    {
        printf("Enter name : ");
        scanf("%s",student.name);
        printf("Enter roll no : ");
        scanf("%d", &student.roll);
        printf("Enter marks : ");
        scanf("%f",&student.marks);
        fwrite(&student,sizeof(student),1,fp);
    }

    fclose(fp);
}
```

### 11.12.2 fread()

声明：size_t fread(void *ptr, size_t size, size_t n, FILE *fptr);

这里 ptr 是一个指针，它指向接收从文件中读取的数据的内存块，size 是每个项目以字节为长的长度，n 是要从文件中读取的项目数，fptr 是一个文件指针，它指向要从中读取数据的那文件。

成功时它从文件中读取 n 个项目并返回 n，如果发生错误或文件结束则返回小于 n 的值。我们可以使用 feof() 和 ferror() 来检查这些条件。

```c
fread(&fval, sizeof(float), 1, fp);
```

```c
fread(arr, sizeof(arr), 1, fp);
```

```c
fread(arr, sizeof(int), 5, fp);
```

```c
struct record{
char name[20];
int roll;
float marks;
}student;

fread(&student, sizeof(student),1,fp);
```

这将从文件中读取单个结构体变量并将其存储在变量 student 中。

### 要读取结构体数组

假设 stu_arr[200] 是上面定义的结构体数组。

```c
fread( stu_arr, sizeof(stu_arr), 1, fp);
```

这里它将从文件中读取结构体数组并将其存储在 stu_arr 中。

要从文件中读取 100 条记录并将它们存储在 stu_arr[200] 的前 100 个结构体中。

```c
fread( stu_arr, sizeof(struct record), 100, fp);
```

以下程序读取在 P11.10 中创建的文件 stu.dat。

```c
/*P11.11 Program to understand the use of fread()*/
#include<stdio.h>
struct record
{
    char name[20];
    int roll;
    float marks;
}student;
main()
{
    FILE *fp;
    fp=fopen("stu.dat","rb");
    if(fp==NULL)
    {
        printf("Error in opening file\n");
        exit(1);
    }
    printf("\nNAME\tROLLNO\tMARKS\n");
    while(fread(&student,sizeof(student),1,fp)==1)
    {
        printf("%s\t",student.name);
        printf("%d\t",student.roll);
        printf("%f\n",student.marks);
    }
    fclose(fp);
}
```

fread() 函数返回成功读取的记录数，因此只要文件中还有记录它就会返回 1，而当文件中没有记录时它会返回小于 1 的数字。因此我们在 while 循环中使用了此条件以在到达文件末尾时停止读取。

## 11.13 文件随机访问

我们可以以两种方式访问文件中存储的数据，顺序访问或随机访问。到目前为止，我们的程序中只使用了顺序访问。例如，如果我们想访问第四十四条记录，则必须顺序读取前四十三条记录才能到达第四十四条记录。在随机访问中，数据可以随机访问和处理，即在这种情况下可以直接访问第四十四条记录。如果想访问特定记录，就无需顺序读取每条记录。随机访问比顺序访问花费的时间更少。

C 支持以下用于随机访问文件处理的函数：
- fseek()
- ftell()
- rewind()

在研究这些函数之前，有必要理解文件位置指针的概念。文件位置指针指向文件中的特定字节，并且对文件的所有读写操作都在该字节处进行。当进行读写操作时，该指针会自动向前移动。为了随机访问数据，我们必须控制该位置指针。

### 11.13.1 fseek()

此函数用于将文件位置指针设置在指定的字节处。

```c
Declaration: int fseek( FILE *fp, long displacement, int origin );
```

这里 fp 是一个文件指针，displacement 是一个 long 整数，可以为正或负，它表示从第三个参数指定的位置向前（如果为正）或向后（如果为负）跳过的字节数。该参数声明为 long 整数，以便可以在大文件中移动。

第三个参数名为 origin，是位移发生相对的位置。它可以取以下三个值之一。

| 常量 | 值 | 位置 |
|---|---|---|
| SEEK_SET | 0 | 文件开头 |
| SEEK_CUR | 1 | 当前位置 |
| SEEK_END | 2 | 文件末尾 |

这三个常量在 stdio.h 中定义，因此我们可以使用这些名称或它们的值。

fseek( ) 函数使用示例—

- 1. `fseek ( p, 10L , 0 );`  
  起始位置为 0，这意味着位移将相对于文件开头，因此位置指针从文件开头向前跳过 10 个字节。由于第二个参数是 long 整数，因此附加了 L。
- 2. `fseek ( p, 5L , 1 );`  
  位置指针从当前位置向前跳过 5 个字节。
- 3. `fseek ( p, 8L , SEEK_SET );`  
  位置指针从文件开头向前跳过 8 个字节。
- 4. `fseek ( p , -5L , 1 );`  
  位置指针从当前位置向后跳过 5 个字节。
- 5. `fseek ( p, 0L , 2 );`  
  起始位置为 2，表示文件末尾，位移为 0，表示从文件末尾跳过 0 个字节。因此在此语句之后，位置指针将指向文件末尾。
- 6. `fseek( p, -6L, SEEK_END );`  
  位置指针从文件末尾向后跳过 6 个字节。
- 7. `fseek ( p, 0L , 0 );`  
  这表示从文件开头跳过 0 个字节。在此语句之后，位置指针指向文件开头。
