
`printf("you entered %d\n", a);`

`return 0;`

}

```

Program:

```c

#include <stdio.h>

int getint();

int main()

{

  int a;

  printf("Enter a numeric string...");

  a = getint();

  printf("You entered %d\n", a);

  return 0;

}

int getint()

{

  char str[6];

  int i, j, k, val;

  i = 0;

  while (i <= 5) {

    str[i] = getche(); /* string input from keyboard */

    if (str[i] == '\r') {

      str[i] = '\0';

      break;

    }

    if (str[i] == '\b') {

      i--;

      printf("\b");

    }

    else

      i++;

  }

  val = 0;

  k = 1;

  for (j = i-1; j >= 0; j--) {

    val = val + (str[j] - 48) * k; /* convert to numeric value */

    k = k * 10;

  }

  return ( val );

}

```

(c) 定义一个函数 `getfloat()`，它从键盘接收一个数字字符串，将其转换为浮点值并将浮点值返回给调用函数。

Program:

```c

/* Program to convert a string to a float value and return the float to the calling function */

#include <stdio.h>

float getfloat();

int main() {

    float floatresult = 0.0f;

    floatresult = getfloat();

    printf("After converting string to float, result is : ");

    printf("%%0.2f\n", floatresult);

    return 0;

}

```

```c

float getfloat() {

    char str[] = "1234.56";

    float temp = 0.0f, result = 0.0f;

    int i, j, decimal;

    for (i = 0; str[i] != '\0'; i++) {

        result = (result * 10) + (str[i] - '0');

        if (str[i] == '.') {

            decimal = 10;

            break;

        }

    }

    if (decimal != 0) {

        for (j = i + 1; str[j] != '\0'; j++) {

            temp += ((str[j] - '0') / decimal);

            decimal *= 10;

        }

    }

    return result + temp;

}

```

如果要正确对齐以下内容，应该使用哪些格式说明？

| | | |
| :--- | :--- | :--- |
| Discovery of India | Jawaharlal Nehru | 425 |
| Experiments with Truth | Mahatma Gandhi | 375 |
| Sunny Days | Sunil Gavaskar | 95 |
| One More Over | Ali Prasanna | 85 |

Program:

```c

#include <stdio.h>

int main() {

    printf("%-30s%20s%10d\n", "Discovery of India", "Jawaharlal Nehru", 425);

    printf("%-30s%20s%10d\n", "Experiments with Truth", "Mahatma Gandhi", 375);

    printf("%-30s%20s%10d\n", "Sunny Days", "Sunil Gavaskar", 95);

    printf("%-30s%20s%10d\n", "One More Over", "Ali Prasanna", 85);

}

```

# CHAPTER II
# 文件输入/输出

指出以下程序中的错误（如果有）：

(a) `#include <stdio.h>`
`void openfile(char *, *);`
`int main()`
`{`
`    FILE *fp;`
`    openfile("myfile.txt", fp);`
`    if (fp == NULL)`
`        printf("Unable to open file...\n");`
`    return 0;`
`}`
`void openfile(char *fn, FILE **f)`
`{`
`    *f = fopen(fn, "r");`
`}`
Error: `openfile`应该返回 `FILE *` 或处理指针，逻辑是正确的；但指针在 `main` 中没有初始化。

(b) `#include <stdio.h>`
`#include <stdlib.h>`
`int main()`
`{`
`    FILE *fp;`
`    char c;`
`    fp = fopen("TRY.C", "r");`
`    if (fp == null)`
`    {`
`        puts("Cannot open file\n");`
`        exit(0);`
`    }`
`    while (c = getc(fp)) != EOF)`
`        putch(c);`
`    close(fp);`
`    return 0;`
`}`
Error: `exit()` 函数调用应该使用 `NULL` 而不是 `null`。

(c) `#include <stdio.h>`
`int main()`
`{`
`    char fname[] = "c:\\students.dat";`
`    FILE *fp;`
`    fp = fopen(fname, "r");`
`    if (fp == NULL)`
`        printf("Unable to open file...\n");`
`    return 0;`
`}`
Error: 未定义符号 `FILE`。应该包含头文件 `"stdio.h"`。

(d) `#include <stdio.h>`
`int main()`
`{`
`    FILE *fp;`
`    char str[80];`
`    fp = fopen("TRY.C", "r");`
`    while (gets(str, 80, fp) != EOF)`
`        puts(str);`
`    fclose(fp);`
`}`
Error: 应该包含 `'stdio.h'`。`fputs()` 需要两个参数。应该配合 `fgets()` 使用 `NULL` 来检查文件结束。

(e) `#include <stdio.h>`
`int main()`
`{`
`    unsigned char;`
`    FILE *fp;`

`    fp = fopen("trial", "r");`
`    while (ch = getc(fp)) != EOF) {`
`        printf("%c", ch);`
`    }`
`    fclose(fp);`
`    return 0;`
`}`
Error: `fopen()` 调用中的参数 `'__mode'` 类型不匹配。错误：未定义符号 `'ch'`。`fclose()` 调用中的参数 `'__stream'` 类型不匹配。

(f) `#include <stdio.h>`
`int main()`
`{`
`    FILE *fp;`
`    char names[20];`
`    int i;`
`    fp = fopen("students.dat", "wb");`
`    for (i = 0; i <= 10; i++) {`
`        puts("\nEnter name: ");`
`        gets(name);`
`        fwrite(name, sizeof(name), 1, fp);`
`    }`
`    close(fp);`
`    return 0;`
`}`
Error: 应该包含头文件 `'stdio.h'`。`sizeof` 应该是一个单词。应该使用 `fclose()` 来关闭文件。

(g) `#include <stdio.h>`
`int main()`
`{`
`  FILE *fp;`
`  char name[20] = "Ajay";`
`  int i;`
`  fp = fopen("students.dat", "r");`
`  for (i = 0; i <= 10; i++)`
`    fwrite(name, sizeof(name), 1, fp);`
`  close(fp);`
`  return 0;`
`}`

(h) `#include <fcntl.h>`
`#include <stdio.h>`
`int main()`
`{`
`  int *fp;`
`  fp = open("pr2.c", "r");`
`  if (fp == -1)`
`    puts("cannot open file\n");`
`  else`
`    close(fp);`
`  return 0;`
`}`
Error: 打开文件时应该使用 `O_RDONLY` 代替 `"r"`。应该包含 `"stat.h"` 而不是 `"STDIO.H"`。此外，在 `READ` 和 `BINARY` 处应该使用 `O_RDONLY` 和 `O_BINARY`。

350 Let Us C 答案

- 2. I am a boy
- 3. I am a boy
- 4. I am a boy

答案：

- 1. I am a boy

(c) 判断判断题对错：

- 1. 高级文件 I/O 函数的缺点是程序员必须管理文件缓冲区。

答案：错误 (False)

- 2. 如果以读取模式打开一个文件，则该文件必须存在。

答案：正确 (True)

- 3. 如果以写入模式打开的文件已经存在，则其内容将被覆盖。

答案：正确 (True)

- 4. 以追加模式打开文件时，该文件必须存在。

答案：错误 (False)

(d) 以读取模式打开一个文件时，执行了以下哪些活动：

- 1. 在磁盘中搜索文件是否存在。
- 2. 将文件读入内存。
- 3. 设置一个指向文件中第一个字符的指针。
- 4. 以上所有。

答案：

4. 以上所有

(e) 以文本模式创建的文件在后续操作中是否必须始终以文本模式打开？

答案：

是 (Yes)

(f) 使用语句，

```
fp = fopen("myfile.c", "r");
```

如果出现以下情况会发生什么：

- 磁盘上不存在 'myfile.c'
- 磁盘上存在 'myfile.c'

答案：

如果 `myfile.c` 不存在磁盘上，返回 `NULL`
如果 `myfile.c` 存在磁盘上，则文件被加载到内存并设置一个指向文件中第一个字符的文件指针

(g) 库函数 `fflush( )` 的作用是什么？

答案：

清除指定的缓冲区。`fflush( stdin )` 清除键盘缓冲区

(h) 使用语句，

```
fp = fopen("myfile.c", "wb");
```

如果出现以下情况会发生什么：

- 磁盘上不存在 'myfile.c'。
- 磁盘上存在 'myfile.c'

答案：

如果文件不存在磁盘上，则创建一个新文件。
如果文件存在磁盘上，则删除该文件并创建一个新文件

- (i) 一个浮点数组包含学生在考试中获得的百分比分数。为了将这些分数存储在文件 ‘marks.dat’ 中，你会用哪种模式打开文件？为什么？

答案：

以二进制模式打开文件，因为在二进制模式下，浮点数存储在文件中时仅占用四个字节，而文本模式文件中的，浮点数占据的字节数取决于浮点数的长度。

## [C] 尝试以下操作：

- (a) 编写一个程序读取文件并显示其内容，并在每行前显示行号。

## 程序：

```
/* 显示带行号文件的程序 */
#include <stdio.h>

int main()\
{
    FILE *fp;
    char ch;
    char source[ 67 ];
    int count = 1;
    puts ("Enter the file name : ");
    gets ( source );
    fp = fopen ( source, "r"); /* 源文件的只读模式 */
```

```c
if ( fp == NULL )
{
    puts ("Unable to open the file.");
    exit ( 0 );
}
```

```c
system ("cls");
printf ("Filename : %s", source ) ;
```

```c
printf ("InLine - %d", count ) ;
while ( ch = getc( fp ) != EOF )
{
    if ( ch == '\n')
    {
        count++;
        printf ("InLine - %d", count );
    }
    else
        printf ("%c", ch );
}
```

```c
fclose ( fp );
return 0 ;
}
```

- 编写一个程序将一个文件的内容追加到另一个文件的末尾。

## 程序：

```c
/* 在文本文件中交替复制两个文件的内容 */
#include <stdio.h>
#include <string.h>

int main()
{
FILE *fs1, *fs2, *ft;
char str1[ 80 ], str2[ 80 ], source1[ 67 ], source2[ 67 ], target[ 67 ];
char *ptrch, newl = "\n";
int flag = 0;
puts("Enter source1 file name: ");
gets (source1);
puts("Enter source2 file name: ");
gets (source2);
puts("Enter target file name: ");
gets (target);
fs1 = fopen (source1, "r"); /* 源文件的只读模式 */
if ( fs1 == NULL)
{
    puts("Unable to open source1");
    exit(0);
}
fs2 = fopen (source2, "r"); /* 源文件的只读模式 */
if ( fs2 == NULL)
{
    puts("Unable to open source2");
    fclose (fs2);
    exit (0);
}
ft = fopen (target, "w+"); /* 目标文件的写/修改模式 */
if ( ft == NULL)
{
    fclose (fs1);
    fclose (fs2);
    puts("Unable to create target file.");
    exit ( 0 );
}
```

# 第19 章：文件输入/输出

```c
/* 读取第一个文件直到 */
while ( gets (str1, fs1) != NULL )
{
    ptrch = strchr(str1, newl);
    fputs (str1, ft);
    if (ptrch )
        fputs("\n", ft);
}
/* 复制第二个文件的内容 */
while ( gets (str2, fs2) != NULL )
{
    ptrch = strchr(str2, newl);
    fputs (str2, ft);
    if (ptrch )
        fputs("\n", ft);
}
printf ("Copying files completed!!\n");
close (fs1);
close(fs2);
close (ft);
return 0;
}
```

- (c) 假设一个文件包含学生姓名和年龄的记录。编写一个程序读取这些记录并按姓名字母顺序显示它们。

## 程序：

```c
/* 从文件中读取记录并按字母顺序显示
/* 注意 STUDENT.DAT 文件已创建并已写入其中数据 */
#include <stdio.h>
#include <string.h>

int main()
{
    FILE *fp;
    struct stud
    {
        char name[40];
        int age;
    };
    struct stud s, stud[10], temp;
    int n, j, k;
    fp = fopen ("STUDENT.DAT","rb");
    n = 0;
    while (fread (&s, sizeof(struct stud), 1, fp) == 1)
    {
        stud[n] = s;
        n++;
    }
