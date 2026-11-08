

```c
char tempName[20];

fp = fopen("D:\\studentRecords.dat", "wb+");

if(!fp)
{
    printf("\n Cannot Open File ");
    exit(0);
}

do
{
    printf("\n 1. Add Records to a file ");
    printf("\n 2. Display Records ");
    printf("\n 3. Modify Record ");
    printf("\n 4. Delete Record ");
    printf("\n 5. Exit");
    printf("\n Enter your choice -> ");
    scanf("%d", &choice);

    switch(choice)
    {
        case 1:
            fflush(stdin);
            fseek(fp, 0, SEEK_END);
            printf("\n Enter Name Class Age ->");
            scanf("%s %d %d", &stu.name, &stu.class, &stu.age);
            fwrite(&stu, sizeof(stu), 1, fp);
            break;
        case 2:
            rewind(fp);
            while(fread(&stu, sizeof(stu), 1, fp))
            {
                printf("\n %s %d %d ", stu.name, stu.class, stu.age);
            }
            break;
        case 3:
            fflush(stdin);
            rewind(fp);
            printf("\n Enter Name of the Student -> ");
            gets(tempName);
            while(fread(&stu, sizeof(stu), 1, fp))
            {
                if(!strcmp(stu.name, tempName))
                {
                    fflush(stdin);
                    printf("\n Enter New Name Age Class ->");
                    scanf("%s %d %d", &stu.name, &stu.class, &stu.age);
                    fseek(fp, -sizeof(stu), SEEK_CUR);
                    fwrite(&stu, sizeof(stu), 1, fp);
                    break;
                }
            }
            break;
        case 4:
            fflush(stdin);
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
        default:
            break;
    }
} while(choice != 5);

fclose(fp);
getch();
return 0;
}
```

前面程序的输出如下：

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
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 1

Enter Name Class Age ->RONALD 3 9

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 4

Enter Student Name for Deletion -> CRISTINA

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 2

BRIAN 1 5
RONALD 3 9
1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 1

Enter Name Class Age ->EMMIE 5 11

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 2

BRIAN 1 5
RONALD 3 9
EMMIE 5 11
1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 3

Enter Name of the Student -> BRIAN

Enter New Name Age Class->VICKY 5 10

1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 2

VICKY 5 10
RONALD 3 9
EMMIE 5 11
1. Add records to a file
2. Display Records
3. Modify Record
4. Delete Record
5. Exit
Enter your choice -> 5
```

在清单 5.26 中，以二进制模式创建文件，并设置一个文件指针，它指向文件的第一条记录。使用 fread() 和 fwrite() 函数时，文件指针会移动到下一条记录的开头；然而，在关闭文件时，文件指针会失效。文件指针的移动在此程序中至关重要，因为它控制着 fread() 将读取下一条记录的位置，以及 fwrite() 将写入下一条记录的位置。rewind() 函数将文件指针置于文件开头。fseek() 函数有助于将文件指针从一条记录移动到另一条记录。如果要移动到上一条记录，可以使用以下语法：

```c
fseek(fp, -(sizeof(stu)), SEEK_CUR);
```

类似地，以下语法将文件指针移动到文件中的最后一条记录：

```c
fseek(fp, 0, SEEK_END);
```

现在，我们来讨论 C 语言中的文件管理函数。

## 文件管理函数

C 提供了若干文件管理函数，可用于执行各种与文件相关的任务。所有文件管理函数都定义在 <stdio.h> 头文件中。以下是 C 语言中的一些文件管理函数：

- fclose()
- feof()
- ferror()
- fgetpos()
- freopen()
- ftell()

下面详细学习这些函数。

### fclose()

fclose() 函数关闭与流关联的文件并刷新其缓冲区。fclose() 的签名如下：

```c
int fclose(FILE*stream);
```

调用 fclose() 后，流不再与文件保持连接，已分配的缓冲区会自动释放。成功时，fclose() 返回 0；否则，返回 EOF。

### feof()

feof() 函数确定是否已到达与流关联的文件末尾。feof() 的签名如下：

```c
int feof(FILE *stream);
```

如果文件指针位于文件末尾，则返回非零值；否则，返回 0。清单 5.27 展示了 feof() 的工作方式：

清单 5.27：展示 feof() 的工作方式

```c
#include<stdio.h>
int main()
{
    char *end_char;
    char sentence[100];
    FILE *fp;

    fp = fopen("D:\\readme.txt","r");

    if(!fp)
    {
        printf("\n Failed to open the file");
        return 0;
    }
    while(!feof(fp))
    {
        end_char = fgets(sentence, 100, fp);
        printf("%s \n",sentence);
    }

    fclose(fp); /* For closing the file pointer */
    getch();

    return 0;
}
```

在清单 5.27 中，我们以只读模式打开了一个已存在的文件，并从该文件中获取信息。feof() 函数用于表示是否已到达文件末尾。从文件中获取信息的过程会一直持续到文件末尾。

### ferror()

ferror() 函数检查给定流上的文件错误。ferror() 的签名如下：

```c
int ferror(FILE *stream);
```

返回值为 0 表示未发生错误，而非零值表示发生了错误。清单 5.28 展示了 ferror() 的工作方式：

清单 5.28：使用 ferror()

```c
#include<stdio.h>
int main()
{
    char *end_char;
    char sentence[100];
    FILE *fp;

    fp = fopen("D:\\readme.txt","r");

    if(!fp)
    {
        printf("\n Failed to open the file");
        return 0;
    }
    while(!feof(fp))
    {
        end_char = fgets(sentence, 100, fp);
        if(ferror(fp)) {
            printf("\n Error Occurred while reading ");
        }
        printf("%s \n",sentence);
    }

    fclose(fp); /* for closing the file pointer */
    getch();

    return 0;
}
```

在清单 5.28 中，我们正在从以只读模式打开的文件中读取信息。从文件读取时，如果遇到任何错误，ferror() 函数会通知该错误，并可以针对它采取适当措施。

### fgetpos()

fgetpos() 的签名如下：

```c
int fgetpos(FILE *stream, fpos_t *position);
```

fgetpos() 函数将文件指针的当前值存储到 position 所指向的对象中。position 所指向的对象必须是 fpos_t 类型。如果发生错误，则 fgetpos() 返回非零值；否则，返回 0。

### freopen()

freopen() 函数将现有流与另一个文件关联。在此过程中，文件末尾标志和错误标志会被清除。freopen() 函数的签名如下：

```c
FILE *freopen(const char *fname, const char *mode, FILE *stream);
```

新文件的名称由 fname 指向，访问模式由 mode 指向，要重新分配的流由 stream 指向。

### ftell()

ftell() 函数返回指定流的文件指针当前值。ftell() 函数的签名如下：

```c
long int ftell(FILE *stream);
```

对于二进制流，该值以字节数为单位。对于文本流，返回值可能没有意义，因为可能发生字符转换，例如用回车/换行替换换行符，这会影响文件的外观大小。

接下来，我们来讨论 C 语言中的按位运算符。

