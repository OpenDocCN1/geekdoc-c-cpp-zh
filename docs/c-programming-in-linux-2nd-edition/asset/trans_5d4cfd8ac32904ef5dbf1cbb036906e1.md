
A **space** character has become a **+** and ! has become **%21**.

这种编码发生是因为某些字符在传输协议本身中被明确使用。例如 **&** 用于分隔 `QUERY_STRING` 的各部分，而空格根本无法按原样发送。

任何希望使用来自 HTML 表单信息的程序都必须能够解码所有这些内容，而我们现在将尝试做到这一点。

程序 `chapter4_2.c` 实现了我们目前看到的功能。它在同一个文件中包含 main 函数和 `decode_value` 函数。

`decode_value` 函数接受三个参数：

-   我们要查找的值的名称 “`ITEM1=`” 或 “`ITEM2=`”。
-   如果找到，将要放入值的变量的地址
-   要复制的最大字符数

该函数在 `QUERY_STRING` 中查找值的开始和结束位置，然后逐个将找到的字符复制到 value 变量中，并添加一个 `NULL` 字符来终止字符串。

```
/* **************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter4_2.c
 * **************************************************/
#include <stdio.h>
#include <string.h>

void decode_value(const char *key, char *value, int size)
{
    int length = 0, i = 0, j = 0;
    char *pos1 = "0", *pos2 = "0";
    //if the string key is in the query string
    if ( (pos1 = strstr(getenv("QUERY_STRING"), key)) != NULL )
    {
        //find start of value for this key
        for(i=0; i<strlen(key); i++) pos1++;
        //find length of the value
        if ( (pos2 = strstr(pos1,"&") ) != NULL )
            length = pos2 - pos1;
        else length = strlen(pos1);
        //character by character, copy value from query string
        for(i = 0, j = 0; i < length ; i++, j++)
        {
            if(i < size) value[j] = pos1[i];
        }
        //add NULL character to end of the value
        if(j < size) value[j] = '\0';
        else value[size-1] = '\0';
    }
}
int main(int argc, char *argv[], char *env[])
{
    printf("Content-type:text/html\n\n<html><body bgcolor=#23abe2>\n");
    char value[255] = "";
    strncpy(value,(char *) getenv("QUERY_STRING"),255);
    printf("QUERY_STRING : %s<BR>\n", value );
    printf("<form>\n");
    //call the decode_value function to get value of "ITEM1"
    decode_value("ITEM1=", (char *) &value, 255);
    if(strlen(value) > 0)
        printf("<input type=\"TEXT\" name=\"ITEM1\" value=\"%s\">\n",value);
    else
        printf("<input type=\"TEXT\" name=\"ITEM1\">\n");
    //call the decode_value function to get value of "ITEM2"
    decode_value("ITEM2=", (char *) &value, 255);
    if(strlen(value) > 0)
        printf("<input type=\"TEXT\" name=\"ITEM2\" value=\"%s\">\n",value);
    else
        printf("<input type=\"TEXT\" name=\"ITEM2\">\n");
    printf("<input type=\"SUBMIT\">");
    printf("</form></body></html>\n");
    return 0;
}
```

看起来我们需要对这个 decode_value 包进行一些认真的工作，因为这是我们预计会反复做的工作，所以编写一个可重用的 **function** 是有意义的。

首先我们可以将此函数放入名为 decode_value.c 的单独文件中，并为我们可能编写的所有函数创建一个名为 c_in_linux.h 的文件，然后将所有这些编译成一个库。在 Makefile 中我们可以添加：

```
SRC_CIL = decode_value.c
OBJ_CIL = decode_value.o
#CIL_INCLUDES = -I/usr/include/apache2 -I -I/usr/include/apache2 -I/usr/include/apr-I
#CIL_LIBS = -L/usr/lib/mysql -lmysqlclient -L/usr/lib -lgd -L/home/david/public_html/Ventus/code

all: lib_cil 4-4

lib_cil:
    gcc -c -s $(SRC_CIL)
    ar rcs c_in_linux.a $(OBJ_CIL)
    $(RM) *.o

4-4:
    gcc -o logic4 chapter4_3.c c_in_linux.a -lc
    cp logic4 /home/david/public_html/cgi-bin/logic4
```

这看起来很糟糕且复杂，但其含义如下：

输入 “make all” 将会：

-   编译列表 SRC_CIL 中列出的所有 *.c 文件并生成对象文件 *.o
-   将所有对象文件编译成名为 lib_c_in_linux.a 的库归档文件
-   使用这个新归档编译 4-4。

这是我们将使用的模型，以使我们的文件尽可能小，并使代码的可共享性达到最大。

我们现在可以拥有一个更简单的 “main” 函数文件，以及一些文件，用于我们可能想要编写的内容，这些内容可以作为可从任何地方调用的函数，实际上我们还不知道。所有这些都组织在一个库文件 (*.a 代表 archive 归档) 中——这些也可以编译为动态可加载的共享对象 *.so，它们很像 Windows DLL。这正是所有 Linux 软件的编写和交付方式。

例如 MySQL C 应用程序编程接口 (API) 包括：

-   /usr/include/mysql 中的所有头文件
-   库文件 /usr/lib/mysql/libmysqlclient.a

我们真正做的事情就是 Linux 的组装方式——我们只是以同样的方式添加内容。

我们现在的主文件如下所示：

```
/*************************************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter4_3.c
 *************************************************************************/

#include <stdio.h>
#include <string.h>
#include "c_in_linux.h"

int main(int argc, char *argv[], char *env[])
{
    printf("Content-type:text/html\n\n<html><body bgcolor=#23abe2>\n");
    char value[255] = "";
    strncpy(value,(char *) getenv("QUERY_STRING"),255);
    printf("QUERY_STRING : %s<BR>\n", value );
    printf("<form>\n");
    //call the decode_value function to get value of "ITEM1"
    decode_value("ITEM1=", (char *) &value, 255);
    if(strlen(value) > 0 )
        printf("<input type=\"TEXT\" name=\"ITEM1\"\nvalue=\"%s\">\n",value);
    else
        printf("<input type=\"TEXT\" name=\"ITEM1\">\n");
    //call the decode_value function to get value of "ITEM2"
    decode_value("ITEM2=", (char *) &value, 255);
    if(strlen(value) > 0 )
        printf("<input type=\"TEXT\" name=\"ITEM2\"\nvalue=\"%s\">\n",value);
    else
        printf("<input type=\"TEXT\" name=\"ITEM2\">\n");
    printf("<input type=\"SUBMIT\">");
    printf("</form></body></html>\n");
    return 0;
}
```

这段代码以相同的方式调用 decode_value 函数，但由于库 c_in_linux.a 在编译时被链接，并且它可以访问列出库中所有函数的头文件 c_in_linux.h，因此一切都能正常工作。

尝试用 **pseudocode** 描述解码此 QUERY STRING 的过程：

    get the QUERY_STRING
    find the search string “ITEM1=” inside it
    look for the end of the value of “ITEM1=”
    copy the value to our “value” variable, translating funny codes such as:
        %21 is ! %23 is #

这些特殊代码由浏览器生成，这样无论你在 HTML 表单中输入什么，都能安全地传输并且不会干扰 HTTP 协议。它们有很多，而本章的任务是 **finish this task off**，以便键盘上的每个键都能按你认为的方式工作！！

程序 chapter4_3.c 调用这个未完成的函数 **decode_value**，到目前为止它只能处理 **space** 字符和 ! ——它使用 **if** 和 **else** 和 **for** 以及库函数 **getenv, strcpy, strlen, strstr**，在一个 **conditional logic** 中，字符串被分析以找到特定项，然后该项被复制到名为 **value** 的内存块中，该内存块已传递给它。

结果显示解码后的值被粘贴到第一个字段中；

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_50_0.png)

```
/* **************************************************
 * program: decode_value.c           *
 * version: 0.1                      *
 * author: david haskins February 2008 *
 * **************************************************/
#include <stdlib.h>
#include <string.h>
void decode_value(const char *key, char *value, int size)
{
    unsigned int length = 0;
    unsigned int i = 0;
    int j = 0;
    char *pos1 = '\0',*pos2 = '\0',code1 = '\0',code2 = '\0';

    strcpy(value,"");
    if( ( pos1 = strstr(getenv("QUERY_STRING"), key)) != NULL )
    {
        for(i=0; i<strlen(key); i++) pos1++;
        if( (pos2 = strstr(pos1,"&")) != NULL )
        {
            length = pos2 - pos1;
        }
        else length = strlen(pos1);
        for(i=0, j=0; i < length ;i++,j++)
        {
            if(j < size)
            {
                if(pos1[i] == '%')
                {
                    i++;   code1 = pos1[i];
                    i++;   code2 = pos1[i];
                    if(code1 == '2' && code2=='0')
                        value[j] = ' '; //0x20
                    else if(code1 == '2' && code2=='1')
                        value[j] = '!';//0x21
                }
                else value[j] = pos1[i];
            }
        }
        if(j < size)
        {
            value[j] = '\0';
        }
        else value[size-1] = '\0';
    }
}
```
