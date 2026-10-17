
```c
for (j = 0; j < n; j++)
{
    for (k = j + 1; k < n; k++)
    {
        if (strcmp(stud[j].name, stud[k].name) > 0)
        {
            temp = stud[j];
            stud[j] = stud[k];
            stud[k] = temp;
        }
    }
}
close ( fp );
for (j = 0; j < n; j++)
{
    printf("Name: %s, age:%d\n", stud[j].name, stud[j].age);
}
return 0;
}
```

- (d) 编写一个程序复制一个文件的内容到另一个文件。在此过程中将所有小写字符转换为大写。

## 程序：

```c
/* 复制一个文件到另一个并将小写字符转换为大写 */
#include <stdio.h>
#include <ctype.h>
int main()
{
FILE *fs, *ft;
char ch;
char source[67 ], target[67 ];
puts ("Enter source file: ");
gets ( source );
puts ("Enter target file: ");
gets ( target );
fs = fopen ( source, "r"); /* 源文件的只读模式 */
if ( fs == NULL)
{
    puts("Unable to open source");
    exit ( 0 );
}
ft = fopen ( target, "w"); /* 目标文件的写入模式 */
if ( ft == NULL)
{
    fclose ( fs );
    puts("Unable to open target");
    exit ( 0 );
}
while ( ch = fgetc ( fs ) != EOF )
{
    /* 如果是小写字母则转换为大写 */
    if (islower ( ch ))
        fputc ( toupper ( ch ), ft );
    else
        fputc ( ch, ft );
}
printf ("File copied!!\n");
fclose ( fs );
fclose ( ft );
return 0;
}
```

- (e) 编写一个程序交替合并两个文件的行并将结果写入新文件。如果一个文件的行比另一个少，则较大文件的剩余行应直接复制到文件中。

## 程序：

```c
/* 交替合并两个文件的行到新文件 */
#include <stdio.h>
#include <string.h>
int main()
{
FILE *fs1, *fs2, *ft;
char str1[ 80 ], str2[ 80 ], source1[ 67 ], source2[ 67 ], target[ 67 ];
char *ptrch, *newl = "\n";
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
    exit (0);
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
while ( gets (str1, fs1) != NULL && gets (str2, fs2) != NULL )
{
    ptrch = strchr(str1, newl);
    fputs (str1, ft);
    if (ptrch )
        fputs("\n", ft);
    ptrch = strchr(str2, newl);
    fputs (str2, ft);
    if (ptrch )
        fputs("\n", ft);
}
while ( gets (str1, fs1) != NULL )
{
    ptrch = strchr(str1, newl);
    fputs (str1, ft);
    if (ptrch )
        fputs("\n", ft);
}
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

```c
ft = fopen ( target, "w+" ); /* 目标文件的写入/修改模式 */
if ( ft == NULL ) {
    fclose ( fs1 );
    fclose ( fs2 );
    puts ( "无法创建目标文件" );
    exit ( 0 );
}
/* 读取源文件并交替复制字符串 */
/* 持续读取，直到其中任一个文件到达结束符 (eof) 为止 */
while ( gets ( str1, 79, fs1 ) != NULL ) {
    ptrch = strchr ( str1, newl );
    fputs ( str1, ft );
    if ( ptrch )
        fputs ("\n", ft );
    }
    if ( gets ( str2, 79, fs2 ) != NULL ) {
        fputs ( str2, ft );
        ptrch = strchr ( str2, newl );
        flag = 1 ;
        if ( ptrch )
            fputs ("\n", ft );
    } else
        fputs ("\n", ft );
}
/* 在未到达文件结束符 (eof) 时复制文件内容 */
if ( flag == 1 ) {
    while ( gets ( str2, 79, fs2 ) != NULL ) {
        ptrch = strchr ( str1, newl );
        fputs ( str2, ft );
```

# 第 19 章：文件输入/输出

```c
if ( ptrch )
    fputs("\n", ft );
}
printf("\n文件复制完成!!\n");
fclose ( fs1);
fclose ( fs2);
fclose ( ft );
return 0;
}
```

- 编写一个程序在屏幕上显示文本文件的内容。满足以下要求：

在对角线坐标为 (0, 1) 和 (79, 23) 的框内显示内容。在第 0 行显示正在显示的文件名和页码。当一页文件内容显示完毕后，在第 24 行闪烁显示“按任意键...”的消息。当按下按键时，应显示下一页的内容，依此类推，直到文件末尾。

程序：

```c
/* 显示文件的内容 */
#include <stdio.h>
#include <windows.h>
void dropbox ( int, int, int, int );
void gotoxy ( short int col, short int row );
int main ( int argc, char *argv[])
{
    FILE *fp;
    char ch;
    int pg=1, r=2, c=1;
```

362

Let Us C Solutions

```c
if ( argc != 2 )
{
    puts ("用法错误... ");
    exit (1);
}
fp = fopen (argv[ 1 ], "r");
if ( fp == NULL)
{
    puts ("无法打开源文件... ");
    exit (2);
}
```

```c
drawbox ( 1, 0, 22, 79 );
gotoxy ( 0, 0 );
printf ("Filename: %s", argv[1] );
gotoxy ( 65, 0 );
printf ("Page :- %d", pg);
```

```c
while (( ch = getc ( fp) ) != EOF )
{
    if ( ch != '\n')
    {
        gotoxy ( r, c);
        printf ("%c", ch);
        c++;
    }
    else
    {
        r++;
        c = 1;
        if (r > 20)
        {
            pg++;
            r = 2;
            gotoxy ( 0, 23 );
            puts ("Press any key ... ");
            system ("cls");
        }
    }
}
```

```c
drawbox ( 1, 0, 22, 79 );
gotoxy ( 0, 0 );
printf ( ("Filename : %s", argv[ 1 ] );
gotoxy ( 65, 0 );
printf ( ("Page : %d", pg );
}
}
fclose ( fp );
return 0;
}
```

```c
void dropbox ( int a, int b, int i, int j)
{
int x, k;
gotoxy ( b, a );
printf ( ("%c", 201 );
gotoxy ( b, i );
printf ( ("%c", 200 );
gotoxy ( j, i );
printf ( ("%c", 188 );
gotoxy ( j, a );
printf ( ("%c", 187 );
}
```

```c
for ( x=a + 1; x<=i - 1; x++ )
{
gotoxy ( b, x );
printf ( ("%c", 186 );
gotoxy ( j, x );
printf ( ("%c", 186 );
}
for ( k=b + 1; k<=j - 1; k++ )
{
gotoxy ( k, a );
printf ( ("%c", 205 );
gotoxy ( k, i );
printf ( ("%c", 205 );
}
}
```

```c
void gotoxy ( short int col, short int row ) {
    HANDLE hStdout = GetStdHandle ( STD_OUTPUT_HANDLE );
    COORD position = { col, row };
    SetConsolePosition ( hStdout, position );
}
```

编写一个程序使用以下方法加密/解密文件：

- 偏移位加密（offset cipher）：在偏移位加密中，源文件中的每个字符都与一个固定值进行偏移，然后写入目标文件。例如，如果从源文件中读取的字符是 'A'则通过对 'A' 偏移固定值 128 将其转换为新字符，然后将新字符写入目标文件。

程序：

```c
/* 使用偏移位加密加密/解密文件 */
#include <stdio.h>
FILE *fs, *ft;
void code();
void decode();
int main (int argc, char *argv[]) {
    if (argc != 4) {
        puts("用法错误。正确用法是:\n");
        puts("program <源文件> <目标文件> <C/D>\n");
        exit(1);
    }
    fs = fopen(argv[1], "r"); /* 源文件 - 只读模式 */
if ( fs == NULL )
{
    puts("无法打开源文件\n");
    exit ( 2 );
}
ft = fopen ( argv[ 2 ], "w" ); /* 目标文件 - 写入模式 */
if ( ft == NULL )
{
    puts("无法打开目标文件\n");
    fclose (fs);
    exit ( 3 );
}
if (*argv[ 3 ] == 'c' || argv[3] == 'C')
    code();
else {
    decode();
}
fclose ( fs );
fclose ( ft );
printf ( "任务完成\n" );
return 0;
}
void code()
{
    char ch;
    int i = 0;
    char arr1[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()_+-=[]{}|;;':\",.<>?`";
    char arr2[] = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ09876543210~!@#$%^&*()_+-=[]{}|;;':\",.<>?`";
    while ( ch = getc ( fs ) ) != EOF) {
        for ( i = 0; i <= 96; i++) {
            if (ch == arr1[i]) {
                putc(arr2[i], ft);
                break;
            }
        }
    }
}
void decode() {
    int ch;
    while ( ch = getc ( fs ) ) != EOF) {
        ch = ch - 128; /* 解密 - 偏移 -128 */
    }
}
```

- (2) 替换加密（substitution cipher）：源中的每个字符都被替换为预定义的字符，并将该字符写入目标文件。例如，如果从源文件中读取到 'A'，且我们决定将每个 'A' 替换为 '!'，则会将 '!' 写入目标文件。同样，每个 'B' 将被替换为 '@'，以此此类推。

程序：

```c
/* 使用替换加密加密/解密文件 */
#include <stdio.h>
FILE *fs, *ft;
void code();
void decode();
int main (int argc, char *argv[]) {
    if (argc != 4) {
        puts("用法错误。正确用法是:\n");
        puts("program <源文件> <目标文件> <C/D>\n");
        exit(1);
    }
    fs = fopen(argv[1], "r"); /* 源文件 - 只读模式 */
if ( fs == NULL )
{
    puts("无法打开源文件\n");
    exit ( 2 );
}
ft = fopen ( argv[ 2 ], "w" ); /* 目标文件 - 写入模式 */
if ( ft == NULL )
{
    puts("无法打开目标文件\n");
    fclose (fs);
    exit ( 3 );
}
if (*argv[ 3 ] == 'c' || argv[3] == 'C')
    code();
else {
    decode();
}
fclose ( fs );
fclose ( ft );
return 0;
}
void code()
{
    char ch;
    int i = 0;
```
