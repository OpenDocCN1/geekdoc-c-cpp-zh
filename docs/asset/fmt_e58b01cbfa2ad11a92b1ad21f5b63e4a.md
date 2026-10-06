
```c
#include <string.h>
int main()
{
    char st[20];      /* 定义一个字符数组 */

    strcpy(st,"abc");  /* st 指向字符数组 */
    return 0;
}
```

### 或者

```c
#include <string.h>
#include <stdlib.h>
int main() {
    char *st = malloc(20); /* st 指向分配的数组 */
    strcpy(st, "abc"); /* st 指向字符数组 */
    free(st);
    return 0;
} /* 不要忘记释放内存 */
```

实际上，对于这段代码，第一种方案更好。为什么？动态分配只有在需要时才使用。它比定义普通数组慢且更容易出错。

## 3. 字符串错误

### 3.1 混淆字符和字符串常量

C 将字符和字符串常量视为完全不同的东西。字符常量使用单引号，字符串常量使用双引号。字符串常量作为指向字符串常量的指针。考虑以下代码：

```c
char ch = 'A'; /* 正确 */
char ch = "A"; /* 错误 */
```

第二行将字符变量 `ch` 赋值为字符串常量的地址。这将产生编译器错误。如果字符串指针赋值给字符常量，也会发生这种情况：

```c
const char *st = "A"; /* 正确 */
const char *st = 'A'; /* 错误 */
```

### 3.2 使用 == 比较字符串

永远不要使用 `==` 运算符比较字符串的值！字符串是字符数组。字符数组的名字就像指向字符串的指针（就像 C 中的其他数组类型一样）。那怎样？考虑以下代码：

```c
char st1[] = "abc";
char st2[] = "abc";
if ( st1 == st2 )
    printf("Yes");
else
    printf("No");
```

这段代码输出 `No`。为什么？因为 `==` 运算符比较的是 `st1` 和 `st2` 的指针值，而不是它们指向的数据。比较字符串的正确方法是使用 `strcmp()` 库函数。

### 3.3 未终止字符串

```c
if ( strcmp(st1, st2) == 0 )
    printf("Yes");
else
    printf("No");
```

比较字符串的正确方法是使用 `strcmp()` 库函数。

### 3.4 未为空终止符留出空间

```c
fclose(fp);
return 0;
```

此程序将两次打印输入文件的最后一行。为什么呢？在最后一行被读取并打印后，`feof()` 仍然会返回 0（假），循环将继续。下一次 `gets()` 失败，因此存储最后一行内容的 `line` 变量不会改变，并被再次打印。之后，`feof()` 将返回真（因为 `fgets` 失败且循环结束）。

应该如何修复这个问题？一种方法如下所示：

```c
#include <stdio.h>
int main()
{
    FILE * fp = fopen("test.txt", "r");
    char line[100];
    while( 1 )
    {
        fgets(line, sizeof(line), fp);
        if ( feof(fp) ) /* 在 fgets() 之后检查 EOF */
        break;
        fputs(line, stdout);
    }
    fclose(fp);
    return 0;
}
```

然而，这不是最好的方法。实际上没有理由使用 `feof()`。C 的输入函数的返回值可以用来检查 EOF。例如，`fgets` 在遇到 EOF 时会返回 `NULL` 指针。

这里是程序的更好版本：

```c
#include <stdio.h>
int main()
{
    FILE * fp = fopen("test.txt", "r");
    char line[100];
    while( fgets(line, sizeof(line), fp) != NULL )
        fputs(line, stdout);
    fclose(fp);
    return 0;
}
```

作者还没有见过任何学生正确地使用 `feof()` 函数！顺便一下，这种讨论也适用于 C++ 和 Java。`istream` 的 `eof()` 方法用法与 C 的 `feof()` 相同。

## 4.3 在输入缓冲区中留下字符

C 输入（和输出）函数会对数据进行缓冲。缓冲将数据存储在内存中，只有在需要时才从（或向）I/O 设备读取（或写入）数据。分块读写数据比一次处理一个字节（或字符）要高效得多。缓冲区通常对编程没有影响。

缓冲现象可见的一个地方是使用 `scanf()` 进行输入。键盘通常是缓冲的。这意味着每行输入都存储在缓冲区中。当程序在想要处理下一行输入之前，没有处理完行中的所有数据时，就会出现问题。例如，考虑以下代码：

```c
int x;
char st[31];
printf("Enter an integer: ");
scanf("%d", &x);
printf("Enter a line of text: ");
gets(st, 31, stdin);
```

`gets()` 不读取你输入的文本行。相反，它可能只读到一个空行。事实上，程序甚至不会等待 `gets()` old的输入。为什么呢？`scanf()` 读取了表示整数所需的所有字符，但它将 `\n` 留在了输入缓冲区中。然后 `gets()` 开始从输入缓冲区中读取数据。它发现了一个 `\n` 并停止，没有任何额外的键盘输入。

解决方案是什么？一个简单的方法是在 `scanf()` 调用后读取并丢弃输入缓冲区中的所有字符，直到遇到 `\n`。由于这可能在很多地方使用，将其封装成函数是有意义的。这里有一个实现此此函数

- *函数 dump_line*

- 该函数读取并丢弃文件当前输入行上的任何剩余字符。

- 参数：

    - `fp` - 指向 `FILE` 的指针，用于从其中读取字符

- 前置条件：

    - `fp` 指向一个已打开的文件

- 后置条件：

    由 `fp` 引用的文件定位在下一行的末尾或文件末尾。

```c
void dump_line(FILE * fp )
{
    int ch;

    while((ch = fgetc(fp)) != EOF && ch != '\n') {
        /* 函数体 */
    }
}
```

以下是使用上述函数修复后的代码：

```c
int x;
char st[31];
printf("Enter an integer: ");
scanf("%d", &x);
dump_line(stdin);
printf("Enter a line of text: ");
fgets(st, 31, stdin);
```

一种错误的解决方案是使用：

```c
fflush(stdin);
```

这可以编译，但其行为在 ANSI 标准中未定义。`fflush()` 函数仅用于输出流而不是输入。这种方法在某些 C 编译器中可能有效，但是不可接受的！

## 4.4 使用 gets() 函数

不要使用这个函数！它不知道传递给它的可以安全地存储多少字符。因此，如果读取的过多，内存将被破坏。互联网上有许多安全漏洞是利用了这一点！改用 `fgets()` 函数（从 stdin 读取）。但请记住，`fgets()` 不丢弃输入中的 `\n`。`scanf()` 函数也可以危险地使用。通过指定宽度可以安全使用，例如，`20s` 格式不会读取超过 20 个字符。

## 第二章 - 使用 C 开发

## 提示

如果你在代码中发现任何错误，不要沮丧。用你的大脑调试，你至少可以在文本中找到地址。

```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>

int main() {
  char line[1024];
  char address[256];
  char *ptr1 = NULL;
  char *ptr2 = NULL;

  while(fgets(line, 1024, stdin) != NULL) {
    if(strchr(line, '\n')) {
      for(ptr1 = line, ptr2 = address; *ptr1; ptr1++) {
        if(isalpha(*ptr1) || isdigit(*ptr1)) {
          *ptr2++ = *ptr1;
        }
      }
      *ptr2 = '\0';
      if(strlen(address) >= 6) {
        printf("%s\n", address);
      }
    }
  }
  return 0;
}
```

## 161. 求解三元线性方程

```c
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>

main()
{
    float a,b,c,d,l,m,n,k,p,D,q,r,s,x,y,z;
    printf("求解三元方程组程序");
    printf("\方程方程为 ax+by+cz=0\nl+my+nz=0");
    printf("\n按顺序输入系数 a,b,c,d,l,m,n,k,p,q,r,s:");
    scanf("%f%f%f%f%f%f%f%f%f%f", &a,b,c,l,m,n,p,q,r);
    printf("\n你输入的方程为:");
    printf("\n%.2fx + %.2fy + %.2fz = 0", a,b,c);
    printf("\n%.2fx + %.2fy + %.2fz = 0", l,m,n);
    printf("\n%.2fx + %.2fy + %.2fz = 0", p,q,r);
    D = (a*m*r+b*p*n+c*l*q)-(a*n*q+b*l*r+c*m*p);
    x = ((b*r*k+c*m*s+d*q*m)-(b*n*q+c*k*r+d*m*p))/D;
    y = ((a*n*s+c*p*k+d*l*r)-(a*l*r+c*k*s+d*n*p))/D;
    z = ((a*q*k+b*l*s+d*m*p)-(a*m*s+b*p*k+d*q*q))/D;
    printf("\n上述方程的解为:");
    printf(" x = %5.2f\ny = %5.2f\nz = %5.2f\n",x,y,z);
}else{
    getch();
    return 0;
}
```

## 162. 在“C”中开发模拟或数字时钟

```c
#include<graphics.h>
#include<conio.h>
#include<math.h>
#include<dos.h>
void main()
{
int gd=DETECT,gm;
int x=320,y=240,r=200,i,h,m,s,theamin,tasec;
struct time t;
char n[12][3]="3","2","1","12","11","10","9","8","7","6","5","4"};
initgraph(&gd,&gm,"F:\\arun\tttc"); // 包含 egavga.bgi 的目录
circle(x,y,210);
setcolor(4);
setstyle(4,0,5);
for(i=0;i<12;i++)
{
    if(i!=3)
    outtextxy(x+(r-14)*cos(M_PI/6*i)-10,y-(r-14)*sin(M_PI/6*i),n[i]);
    else
    outtextxy(x+(r-14)*cos(M_PI/6*i)-10,y-(r-14)*sin(M_PI/6*i),n[i]);
}
gettime(&t);
printf("当前时间为: %02d:%02d:%02d.%02d\n",t.ti_hour,t.ti_min,t.ti_sec,t.ti_hund);
getch();
while(!kbhit())
{
setcolor(5);
setstyle(1);
circle(x,y,10);
floodfill(x,y,5);
gettime(&t);
if(t.ti_min!=m)
{
setcolor(0);
line(x,y,x+(r-60)*cos(M_PI/180),y-(r-60)*sin(M_PI/180));
circle(x-(r-80)*cos(M_PI/180),y-(r-80)*sin(M_PI/180),10);
}
}
```

circle(x+(r-130)*cos(M_PI/6*h-(m/2)*M_PI/180)),y-(r-130)*sin(M_PI/6*h-(m/2)*M_PI/180)),10);

line(x,y,x+(r-60)*cos(thetamin*(M_PI/180)),y-(r-60)*sin(thetamin*(M_PI/180)));

circle(x+(r-80)*cos(thetamin*(M_PI/180)),y-(r-80)*sin(thetamin*(M_PI/180)),10);

setcolor(15);

line(x,y,x+(r-70)*cos(theasec*(M_PI/180)),y-(r-70)*sin(theasec*(M_PI/180)));

delay(1000);

setcolor(0);

line(x,y,x+(r-70)*cos(theasec*(M_PI/180)),y-(r-70)*sin(theasec*(M_PI/180)));

}

}
```

## 163. 编写 C 语言打印文本“C”中的 IP 地址。

```c
#include <stdio.h>
#include <regex.h>
#include <locale.h>
#include <string.h>
#include <stdlib.h>
#include <sys/types.h>
#define IPEXPR "([0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3})""
int main(void)
{
  char line[1024];
  char *address = NULL;
  char delim[] = ":;;/\\^~_()<>*&%$@!?~/ \t\r\n";
  int retval = 0;
  regex_t re;
  setlocale(LC_ALL, "");

  if(regcomp(&re, IPEXPR, REG_EXTENDED) != 0)
    return 1;
```

```c
  while((fgets(line, 1024, stdin)) != NULL)
  {
    if(strchr(line, ',')) == NULL)
      continue;

    address = strtok(line, delim);
    while(address != NULL)
    {
      if(strlen(address) <= 15)
        if((retval= regexec(&re, address, NULL, 0)) == 0)
          printf("%s\n", address);

      address = strtok(NULL, delim);
    }
    /* while */
  } /* while */
  return 0;
}
```

## 164. 编写 C 语言打印进度条“C”。

```c
#include<graphics.h>
#include<conio.h>
#include<alloc.h>
#include<dos.h>
void main()
{
  int gd=DETECT,gm;
  initgraph(&gd,&gm,"c:\t tc ");
  // 将存放 egavga.bgi 的目录在这里
  void *buffer;
  unsigned int size;
  setbkcolor(BLUE);
  line(230,330,370,330);
  line(230,350,370,350);
  line(226,335,226,345);
  line(226,335,230,330);
```

```c
line(226,345,230,350);
line(374,335,374,345);
line(374,335,370,330);
line(374,345,370,350);
```

## 165. 编写 C 语言计算面积和体积。
