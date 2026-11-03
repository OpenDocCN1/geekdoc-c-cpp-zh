
```
{
	int i = 2;
	float f = 2.5367;
	char str[ ] = "Life is like that";
	printf( "%4d%3.5f\n%4s",i,f,str);
}
```

输出：--2（2 前面有 3 个空格，因为 i 以 4 列宽度打印） --3.536（数字前有 2 个空格，数字将按 3 位小数打印。）

is like that.（因为 str 包含超过 4 个字符，所以它会忽略最大长度并打印整个 str。）

## 3. main()

```
{
	int a=250;
	printf("%1d", a);
}
```

输出 250

## 4. main()

```
{
	float a =3.15529;
	printf("%6.2f",a);
	printf("%6.3f",a);
	printf("%5.4f",a);
	printf("%2.1f",a);
	printf("%0.0f",a);
}
```

输出：
--3.16
3.155
3.1553
3.2
3

## 7. char p[] = "The sixth sick sheikh's sixth ship is sick";

```
main()
{
	int i = 0;
	while(p[i]!='\0')
	{
		putchar(p[i]);
		i++;
	}
}
```

输出：
The sixth sick sheikh's sixth ship is sick
因为循环从 0 开始并成功执行，直到遇到空字符，所以字符串的每个字符都会从开头开始打印。

## 8. 以下程序的输出会是什么：

```
printf("%/%/%");
```

输出：%%

## 9. 以下代码能工作吗？如果能，输出会是什么：

```
int n=5;
printf("n=%*d",n,n);
```

输出：能。n= 5
* 表示将使用参数列表中的一个 int 值作为字段宽度。在参数列表中，宽度位于要打印的值之前。在这种情况下，格式说明符

## 5. 指出以下程序中存在的错误（如果有）：

```
char ch;
int i;
scanf("%c", &i);
scanf("%d", &ch);
printf("%c %d",ch, i);
```

输出：你将没有机会为第二个 scanf() 语句输入字符。此问题的解决方法是在第二个 scanf() 之前加上以下语句。

```
fflush(stdin);
```

这将把上一次 scanf() 命中的回车从输入流（即键盘）中刷新出去。

变成 %5d

## 10. 可以在 scanf() 格式字符串中指定可变字段宽度吗？

输出：
不可以。scanf() 格式字符串中 % 符号后的 * 用于抑制赋值。也就是说，当前输入字段会被扫描但不存储。

## 11. 在 fgets() 和 gets() 中，哪个函数使用起来安全？

输出：
fgets()，因为与 fgets() 不同，gets() 无法被告知所提供字符串将存入的缓冲区大小。因此，缓冲区始终存在溢出的可能性。

## 指出以下程序段中的错误（如果有）：

| 1. main( ) { int i; char a[] = "Hello"; while(a != '\0') { printf("%c",*a); a++; } } | 5. main( ) { int dd,mm,yy; printf("\n Enter day,month and year\n"); scanf("%d %*c %d %*c%d",&dd,&mm,&yy); printf("The date is:%d-%d-%d",dd,mm,yy); } 输出：无错误。 6. main( ) { char buffer[50]; int no = 97; double val = 2.34174; char name[10] = "Shweta"; |
|---|---|

输出：错误。“需要值”，因为数组不能递增。

```
2. main()
{
double dual;
scanf("%f",&dual);
printf("\nDouble Value = %lf",dual);
}
```

输出：无错误，但输出将是 -0.000000。因为 double 占 8 字节，float 占 4 字节。

```
3. main()
{
int level;
scanf("%d\n",&level);
printf("\nInteger Value = %d",level);
}
```

输出：错误。未定义符号 n。

```
4. main()
{
char *mess[5];
```

```
sprintf(buffer,"%d %lf %s",&no,&val.name);
printf("\n%d %lf %s",no,val.name);
sscanf(buffer,"%d %2.2lf %s",&no,&val.name);
printf("\n%s",buffer);
printf("\n%d %lf %s",no,val.name);
```

无错误。
因为 sprintf() 将变量打印到指定字符串中（例如，从字符串读取字符并转换，并将它们存储在变量中，复制到 buffer 数组中，当我们打印出 buffer 字符串并将它们存储到变量和 v 值中时）。

输出：无错误，但输出将是 -0.000000。因为 double 占 8 字节，float 占 4 字节。

输出：错误。未定义符号 n。

```
for(i = 0; i<5; i++)

scanf("%s",mess[i]);
}
```

**输出：** 错误。未定义符号 i；此外，当我们谈论指针数组时，它不应接收任何字符串，它可以接收任何字符串或字符的地址。

![](img/3a2b6e5e90a58a56458b0539952c0cd2_252_0.png)

## **回答以下问题：-**

|  |  |
|---|---|
| 1) 要在 char str[100] 数组中接收字符串 "We have got the guts, you get the glory!!"，你会使用以下哪个函数？<br>a) scanf("%s",str);<br>b) gets(str);<br>c) getche(str);<br>d) fgetchar(str);<br>输出：gets(str)<br><br>2) 如果要从键盘接收单个键，你会使用哪个函数？<br>a) scanf( ) | 5) getchar( )、fgetchar( )、getch( ) 和 getche( ) 之间有什么区别？<br>输出：<br>所有函数都从键盘接收一个字符。它们之间有细微差别：<br>getchar( )：从键盘接收一个字符，但必须在字符后按回车键。<br>fgetchar( )：与 getchar( ) 相同。<br>getchar( ) 是宏，而 fgetchar( ) 是函数。<br>getch( )：从键盘接收一个字符，但不 |

b) gets()
c) getche()
d) getchar()
输出：getche()

回显（显示）在屏幕上。
getche()：从键盘接收一个字符并将其回显在屏幕上。

## 3) 如果要从键盘输入一个整数，你会使用哪个函数？

- a) scanf()
- b) gets()
- c) getch()
- d) getche()

输出：scanf()

## 4) 如果要从键盘接收一个字符串，哪个函数工作得更快？

- a) scanf()
- b) gets()

输出：gets()

## 6) printf() 的格式字符串可以包含：

- a) 字符、格式说明和转义序列
- b) 字符、整数和浮点数
- c) 字符串、整数和转义序列
- d) 引号、百分号和反斜杠字符

输出：a) 字符、格式说明和转义序列

![](img/3a2b6e5e90a58a56458b0539952c0cd2_253_0.png)

![](img/3a2b6e5e90a58a56458b0539952c0cd2_254_0.png)

## 章节

## ∞ 12 ∞

## （通过 C 进行文件处理）

## 简介-

到目前为止，我们一直使用 scanf 和 printf 函数来读写数据。这些是面向控制台的输入和输出函数，始终以键盘和屏幕作为目标位置。当数据量较小时，这没问题。然而，现实生活中的问题涉及大量数据，在这种情况下，面向控制台的输出和输入操作有两个主要问题：

A. 处理大量数据非常耗时。
B. 一旦程序关闭或计算机关闭，所有数据都会丢失。为了克服这些问题，我们使用文件处理。文件可用于将数据存储在硬盘上，以便数据永久保存，即使计算机关闭也不会被删除。

文件可以定义为磁盘上存储一组相关数据的位置。可以对文件执行许多函数操作：

- 命名文件。
- 打开文件。
- 从文件读取数据。

- 向文件写入数据。
- 关闭文件。

## 让我们看看一些文件函数

| 函数名 | 操作 |
|---|---|
| fopen() | 创建一个新文件或打开一个现有文件以供使用。 |
| fclose() | 关闭文件。 |
| fgetc() | 从文件读取一个字符。 |
| fputc() | 向文件写入一个字符。 |
| fprintf() | 向文件写入数据。 |
| fscanf() | 从文件读取数据。 |
| fgetw() | 读取一个整数。 |
| fputw() | 写入一个整数。 |
| fseek() | 将位置设置到文件中所需的位置。 |
| ftell() | 给出文件中的当前位置（即从开头开始的字节数）。 |
| rewind() | 将位置设置到文件开头。 |
| fwrite() | 向文件写入数据。 |
| fread() | 从文件读取数据。 |
| feof() | 测试是否已到达文件末尾。 |
| fflush() | 刷新流。 |
| Remove() | 删除指定的文件。 |
| Rename() | 更改文件的名称或路径。 |
| ferror() | 测试文件中是否发生了错误。 |

## 打开文件-

在我们能够从硬盘上的文件读取信息或向其中写入信息之前，我们必须打开文件。

要打开文件，使用 fopen( ) 函数和一个模式，该模式告诉编译器我们将要写入、读取或修改文件。这个 fopen( ) 函数执行三项任务：

- 在磁盘上搜索文件。

