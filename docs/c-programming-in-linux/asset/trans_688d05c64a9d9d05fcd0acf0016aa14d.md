
请注意用于字符的单引号 ' 与用于字符串的双引号 " 之间的区别。

```c
/*****************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter2_2.c
 *****************************************************/
#include <stdio.h>

int main(int argc, char *argv[], char *env[])
{
        char c1 = 'd';
        char c2 = 'a';
        char c3 = 'v';
        char c4 = 'i';
        char c5 = 'd';
        char name[6] = "";

        sprintf(name,"%c%c%c%c%c",c1,c2,c3,c4,c5);
        printf("%s\n",name);
        return 0;
}
```

编译命令：**gcc -o data2 chapter2_2.c -lc**  
使用以下命令调用程序时的输出：**./data2**

*大卫*

### 2.3 字符串能“意味着”什么

任何东西——赋予**变量**的**名称**及其**含义**或**用途**完全取决于观察者的理解。试试这个

```c
/*************************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter2_3.c
 *************************************************************/
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[], char *env[])
{
    printf("Content-type:text/html\n\n");
    printf("<html>\n");
    printf("<body bgcolor=\"%s\">\n",argv[1]);
    printf("</body>\n");
    printf("</html>\n");
    return 0;
}
```

编译命令：gcc -o data3 chapter2_3.c -lc

以超级用户身份将程序复制到你的 public_html/cgi-bin 目录（或 /srv/www/cgi-bin（OpenSuse）或 /usr/lib/cgi-bin（Ubuntu））。

在浏览器中输入：http://localhost/cgi-bin/data3?red

你应该看到如下内容：

![](img/a0cbda189e54d8cb1121c7e151992506_28_0.png)

或者，如果你发送任意参数，你会得到令人惊讶的结果：

![](img/a0cbda189e54d8cb1121c7e151992506_29_0.png)

我们在这里所做的是使用字符串参数 argv[1] 作为 HTML body 标签内的背景颜色代码。我们将 Content-type 规范改为 text/html，于是奇迹般地，我们的程序现在正在生成 HTML 内容。一种语言在另一种语言中被表达。Web 浏览器理解有限的颜色词集合，颜色也可以通过十六进制代码定义，例如 #FFFFFF（白色）、#FF0000（红色）、#00FF00（绿色）、#0000FF（蓝色）。

这个有趣的练习并不只是一个轻量级的小把戏；一个程序能够用另一种语言生成另一个程序，这一想法非常强大，并且支撑着整个互联网的力量。当我们从这样的通用网关接口程序生成 HTML（或 XML 或其他任何内容）时，我们是在创建动态内容，这些内容可以链接到实时变化的数据，而不是预先编辑好的静态网页。在实践中，大多数网站都混合了动态内容和静态内容，但在这里我们看到的是在非常简单的层面上如何做到这一点。

在本书中，我们将把浏览器作为程序的首选界面，因此我们将生成 HTML 和二进制图像流形式的 Web 内容，纯粹作为让程序威力立即可见的一种手段。在终端屏幕上盯着看的代码并不太令人印象深刻，而编写窗口式应用程序也远没有那么简单直接。

在实践中，你可能被要求编写的大多数软件都会在 Web 上运行，因此我们不妨直接从这一理念开始。大多数 Web 应用也会涉及多种语言，例如 CSS、(X)HTML、XML、JavaScript、PHP、JAVA、JSP、ASP、.NET、SQL。如果这听起来很吓人，不要慌张。C 语言知识会让你看到，这些语言虽然各自执行不同功能，但其中许多语言的语法都以 C 为基础。

### 2.4 解析字符串

从某种输入字符串中提取含义或有价值信息的工作称为“解析”。现在我们将构建另一个有趣的、可通过互联网调用的 CGI 程序，来展示我们手中掌握的能力。

请点击广告

![](img/a0cbda189e54d8cb1121c7e151992506_30_0.png)

```c
/************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter2_4.c
 ************************************************/
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[], char *env[])
{
    char *token = NULL;
    char colour1[256] = "";
    char colour2[256] = "";
    int wide = 0;
    int high = 0;
    int columns = 0;
    int rows = 0;

    token = (char *) strtok(argv[1],":");
    strcpy(colour1,token);
    token = (char *) strtok(NULL,":");
    strcpy(colour2,token);
    token = (char *) strtok(NULL,":");
    wide = atoi(token);
    token = (char *) strtok(NULL,":");
    high = atoi(token);
    printf("Content-type:text/html\n\n");
    printf("<html>\n");
    printf("<body bgcolor=\"%s\">\n",colour1);
    printf("<center>\n");
    printf("<table bgcolor=\"%s\" border=2>\n",colour2);
    for(rows=1;rows<=high;rows++)
    {
        printf("<tr>\n");
        for(columns=1;columns<=wide;columns++)
        {
            printf("<td><h6>row=%d cell=%d</h6></td>\n",rows,columns);
        }
        printf("</tr>\n");
    }
    printf("</table>\n");
    printf("</body>\n");
    printf("</html>\n");
    return 0;
}
```

编译命令：`gcc -o data4 chapter2_4.c -lc`

以超级用户身份将程序复制到 `/srv/www/cgi-bin`（OpenSuse）或 `/usr/lib/cgi-bin`（Ubuntu）。

在浏览器中输入：**http://localhost/cgi-bin/data4?red:blue:5:5:**

你应该看到如下内容：

![](img/a0cbda189e54d8cb1121c7e151992506_32_0.png)

在这个程序中，我们取 argv[1]（此处为 *yellow:blue:5:5:*），并使用库函数 **strtok** 对其进行**解析**，该函数将字符串切分为由任意字符 ':' 分隔的标记；然后我们将这些标记用作字符串来指定颜色，并用整数来指定表格的行数和单元格数。

函数 **atoi** 将整数的字符串表示转换为整数（"1" 转换为 1）。

函数 **strtok** 有点奇特：第一次调用时传入要解析的字符串名称，而后继调用中第一个参数会改为 NULL。

**for(...)** 循环机制用于执行固定次数的操作。

引入的 HTML 术语有：

- `<html>`
- `<body>`
- `<table>`
- `<tr>` 表格行
- `<td>` 表格数据单元格

### 2.5 数据与内存——结论

我们使用了一些简单的数据类型来表示某些信息，向程序传递输入，并组织和显示一些可视化输出。

我们使用了嵌入在输出字符串中的 HTML，使输出能在 Web 浏览器中可见。

作为练习，试试这个：

编写一个程序，放入你的 **/public_html/cgi-bin** 文件夹；该程序可以在浏览器中通过**运动队**或**国家**的**名称**以及一系列**颜色**来调用，这些颜色或许以十六进制指定，例如 ff0000 = 红色（rrggbb），用于队伍颜色或地图颜色，并显示一些合理的内容。我的版本如下：

![](img/a0cbda189e54d8cb1121c7e151992506_33_0.png)

![](img/a0cbda189e54d8cb1121c7e151992506_33_1.png)

## 3. 函数、指针和结构体

### 3.1 函数

所有程序的入口点称为 main()，它是一个**函数**，或**一段代码**，会做某些事情，通常返回某个值。我们将程序组织成函数，以防止它们变成无法在一屏或一页中看全的冗长难读代码块，同时也确保不会到处出现重复相同的代码片段。我们可以调用属于 C 语言一部分的**库函数**，如 printf 或 strtok，也可以调用自己或他人的函数及函数库。我们必须确保相应的头文件存在并能被预处理器读取，同时确保源代码或编译后的库也存在且可访问。

正如之前所学，数据的**作用域**限制在声明它的**函数**内，因此我们使用指向数据和数据块的**指针**，将其传递给希望处理我们数据的函数。我们已经看到，字符串被当作指向以 NULL 字符结尾的单个字符数组的指针来处理。

![](img/a0cbda189e54d8cb1121c7e151992506_34_0.png)

