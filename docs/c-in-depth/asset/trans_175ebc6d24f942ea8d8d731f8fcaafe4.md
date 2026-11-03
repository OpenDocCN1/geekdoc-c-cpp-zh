
```c
/*P11.25 Program to understand the use of rename()*/
#include <stdio.h>
main()
{
    char old_name[80],new_name[80];
    printf("Enter the name of file to be renamed : ");
    gets(old_name);
    printf("Enter a new name for the file : ");
    gets(new_name);
    if(rename(old_name,new_name)==0)
        printf("File %s renamed to %s\n",old_name, new_name);
    else
        perror("File not renamed");
}
```

假设我们给出一个不存在的文件名，那么 errno 的值将被设置为 ENOENT，perror 显示的消息将是：

文件未重命名：没有那个文件或目录

### 11.14.6 unlink( )

声明：int unlink(const char *filename);

此函数用于从目录中删除文件。我们也可以将完整路径名作为参数传入。删除前应先关闭文件。成功时返回 0，出错时返回 -1，并将 errno 设置为以下值之一：

- ENOENT    路径或文件名未找到
- EACCES    权限被拒绝

```c
/*P11.26 Program to understand the use of unlink()*/
#include<stdio.h>
main()
{
    FILE *fptr;
    char name[15];
    printf("Enter the file name:");
    scanf("%s",name);
    fptr=fopen(name,"r");
    fclose(fptr);
    if(unlink(name)==0)
        printf("File %s is deleted\n",name);
    else
        perror("File not deleted : ");
}
```

### 11.14.7 remove( )

声明：int remove(const char *filename);

remove 是一个从目录中删除文件的宏。它类似于函数 unlink()。

### 11.14.8 fflush( )

声明：int fflush(FILE *fptr);

此函数将任何已缓冲但未写入的输出写入与 fptr 关联的文件。调用 fflush( ) 后文件不会关闭。成功时返回 0，出错时返回 EOF。如果我们用 stderr 调用此函数，那么所有未写入的缓冲错误消息都将被写出。

```c
fflush(stderr);
```

要刷新所有输出流，我们可以写：

```c
fflush(NULL);
```

尽管 fflush( ) 仅为输出流定义，但在某些编译器中，fflush( ) 可以与 stdin 一起使用，以丢弃标准输入上未读取的字符。例如考虑以下情况：

```c
printf("Enter an integer : ");
scanf("%d", &i);
printf("Enter a character : ");
scanf("%c", &ch);
```

输入整数后，我们按 Enter 键，使第一个 scanf( ) 终止。整数值被 scanf( ) 读取，但换行符（ASCII 10）仍在输入缓冲区中。因此，下一个 scanf( ) 会把这个换行符读入变量 ch，并在用户输入任何字符之前就终止。当我们在 scanf( ) 之后使用 gets( ) 时，也可能出现类似问题，因为 gets( ) 在遇到换行符时就会终止。为避免此类问题，我们可以使用 fflush(stdin) 丢弃任何未读取的字符。例如：

```c
printf("Enter an integer : ");
scanf("%d", &i);
printf("Enter a character : ");
fflush(stdin);
scanf("%c", &ch);
```

注意，fflush(stdin) 不可移植，它可能无法在每个编译器上工作。

### 11.14.9 tmpfile( )

声明：FILE *tmpfile(void);

tmpfile( ) 创建一个临时二进制文件，并以 "wb+" 模式打开它。成功时返回一个 FILE 类型的指针，指向该临时文件；出错时返回 NULL。由 tmpfile( ) 创建的文件是临时的，因为它在关闭时或程序终止时会自动删除。

### 11.14.10 tmpnam( )

声明：char *tmpnam(char str[L_tmpnam]);

此函数用于为文件生成唯一名称。参数 str 可以是 NULL，也可以是最少 L_tmpnam 个字符的数组。如果 str 为 NULL，则 tmpnam( ) 将临时文件名存储在内部静态数组中，并返回指向该数组的指针。如果 str 不为 NULL，则 tmpnam( ) 将临时文件名存储在 str 中并返回 str。在程序执行期间，tmpnam( ) 可以生成的不同文件名的数量由 TMP_MAX 指定，TMP_MAX 定义在 stdio.h 文件中。注意，tmpnam( ) 只创建文件名，不创建文件。可以用 fopen( ) 打开使用 tmpnam( ) 生成的名称的文件，并应使用 fclose( ) 关闭它。

### 11.14.11 freopen( )

声明：FILE *freopen(const char *filename, const char *mode, FILE *fptr);

此函数用于将新文件与文件指针关联。与 fptr 关联的文件会像通过 fclose() 一样关闭；之后，第一个参数中指定的文件名会按指定模式像通过 fopen() 一样打开，并且此 fptr 现在与该文件关联。成功时 freopen() 返回 fptr，出错时返回 NULL。

此函数通常用于更改与文件指针 stdin、stdout 和 stderr 关联的文件。例如，文件指针 stderr 与屏幕关联；如果我们想把错误消息存储在文件中而不是显示在屏幕上，那么可以这样使用 freopen()：freopen("errorfile", "a", stderr);

## 11.15 命令行参数

函数 main() 可以接受两个参数。当 main() 接受参数时，其定义可以写成：

```c
main(int argc,char *argv[ ])
```

第一个参数是 int 类型，第二个是指向字符串的指针数组。按照惯例，这些参数命名为 argc（argument counter，参数计数器）和 argv（argument vector，参数向量），用于访问在命令提示符下提供的参数。让我们看看这是如何完成的。

程序被编译并创建可执行文件。在 DOS 中，可执行文件的名称与程序名相同，并具有 .exe 扩展名。在 UNIX 中，可执行文件命名为 a.out。在 UNIX 中，我们可以使用 -o 选项为可执行文件指定任何其他名称，例如：cc -o myprog myprog.c

现在程序在命令提示符下执行，并向其提供参数。第一个参数始终是可执行文件的名称。参数 argc 和 argv 可用于访问命令行参数。参数 argc 表示命令行上的参数个数。在命令行提供的所有参数在内部都存储为字符串，它们的地址存储在名为 argv 的指针数组中。

```c
/*11.27 Program to understand command line arguments*/
#include<stdio.h>
main(int argc,char *argv[ ])
{
int i;
printf("argc=%d\n",argc);
for(i=0;i<argc;i++)
printf("argv[%d]=%s\n",i,argv[i]);
}
```

假设程序名为 myprog.c，并在命令提示符下执行：myprog you r 2 good

变量 argc 的值为 5，因为在命令提示符下总共提供了五个参数。第一个参数是程序名，所以 argv[0] 指向字符串 "myprog" 的基地址（它可能包含文件的完整路径）。类似地，argv[1] 指向字符串 "you" 的基地址，argv[2] 指向字符串 "r" 的基地址，argv[3] 指向字符串 "2" 的基地址，argv[4] 指向字符串 "good" 的基地址。

输出将是：

- argc = 5
- argv[0] = myprog
- argv[1] = you
- argv[2] = r
- argv[3] = 2
- argv[4] = good

注意每个参数都存储为字符串，所以 argv[3] 并不表示整数 2，而是指向字符串 "2" 的指针。如果我们想在程序中将其用作整数，则必须使用函数 atoi() 将其转换为整数。

## 11.16 一些附加问题

### 问题 1

编写一个程序，将一个文件复制到另一个文件。两个文件的名称应作为命令行参数传递。

```c
/*P11.28 Program to copy a file to another*/
#include<stdio.h>
main(int argc,char *argv[])
{
    FILE *source,*dest,*fopen();
    int c;
    if(argc!=3)
    {
        printf("Wrong number of arguments\n");
        exit(1);
    }
    if((source=fopen(argv[1],"r"))==NULL)
    {
        printf(" Can't open source file\n");
        exit(1);
    }
    if((dest=fopen(argv[2],"w"))==NULL)
    {
        printf(" Can't open destination file\n");
        exit(1);
    }
    while((c=fgetc(source))!=EOF)
        fputc(c,dest);
    fclose(source);
    fclose(dest);
}
```

在此程序中，我们首先使用 argc 检查命令行参数的数量，这样做是一种良好实践。

