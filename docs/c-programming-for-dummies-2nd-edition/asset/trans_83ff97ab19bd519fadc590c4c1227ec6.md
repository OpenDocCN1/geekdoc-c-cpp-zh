
同样在`time.h`头文件中还定义了以下时间函数：

| 函数 | 描述 |
| --- | --- |
| *time()* | *time()*函数使用*time_t*变量的地址作为其参数。该函数用当前Unix纪元时间填充*time_t*变量，并返回一个*time_t*值。 |
| *ctime()* | *ctime()*函数接收一个*time_t*变量，并将其转换为可显示的日期时间字符串。 |
| *localtime()* | 该函数根据存储在*time_t*变量中的时间值，将信息填入*tm*结构体。*localtime()*函数返回*tm*结构体的地址，因此它会与结构体、指针以及那个`->`运算符纠缠不清。 |
| *difftime()* | *difftime()*函数比较两个*time_t*值之间的差异，并返回一个*float*值作为秒数差。 |

C语言库通常还带有其他与时间相关的函数，例如*sleep()*和*clock()*。这些函数可能并非在所有系统上都可用——但这不应成为问题，因为你总是可以自己编写时间函数。

## 开始编程

我可以想象，发明了指针和链表的那些编程大神们，本可以用时间编程把你的大脑搅得一团糟。幸运的是，他们没有这么做。虽然了解指针和结构体有助于你掌握门道，但C语言中的时间编程其实直截了当。

### 查看时钟

计算机，或者说你所编程的任何设备，都会在其数字深处的某个地方保存一个时间值。要访问这个值，你需要编写一个使用*time()*函数的程序。它会把当前的时钟滴答值塞进一个*time_t*变量中，如清单21-1所示。

### 清单21-1：哦，原来这就是时间？

```c
#include <stdio.h>
#include <time.h>

int main()
{
    time_t tictoc;

    time(&tictoc);
    printf("The time is now %ld\n",tictoc);
    return(0);
}
```

清单21-1中的第2行引入了time.h头文件，C语言中各种时间函数都需要它。

第6行声明了time_t变量tictoc。第8行的time()函数需要time_t变量的地址作为其参数。时间值被直接放入变量tictoc（在其内存位置）中。

最后，在第9行，结果值——Unix纪元——通过使用%ld转换字符（long int）输出。

- **练习21-1：** 将清单21-1中的源代码输入到你的编辑器中。编译并运行。

- **练习21-2：** 修改练习21-1中的解决方案，将第8行替换为

    ```c
    tictoc=time(NULL);
    ```

    time()函数需要一个内存位置作为参数，但它也会返回一个time_t值。你可以使用上面给出的格式，也可以使用清单21-1中第8行所示的格式，具体取决于&或NULL这两个古怪符号中哪个最让你害怕。

![](img/dcc0cd79d4a45cfce24fa49d85442884_347_0.png)

早在20世纪70年代和80年代，BASIC程序员会在代码中编写for循环来暂停程序执行。我记得我那可靠的老式TRS-80需要从1数到100的循环来延迟一秒钟的执行。如今的系统要快得多，不能再依赖这种循环来精确延迟程序执行了。

### time()如何影响随机数

在C语言中生成随机数的最佳方法是给随机数生成器设置种子。在第11章中，我描述了如何使用time()函数来完成这个过程。格式如下：

```c
srand((unsigned)time(NULL));
```

当以NULL值（一个指针）作为参数调用时，time()函数会以Unix纪元格式返回当前时间。为了确保返回的值——Unix纪元——不为负数，它被强制转换为无符号类型。这一步可能并非必需，因为在某些系统上time_t值可能本来就是无符号的。不过，强制转换可以确保该值始终为正。

### 查看时间戳

将当前日期和时间显示为整数不会让你的用户开心。事实上，我甚至不知道有哪个Unix极客能看着一个Unix纪元数字就判断出它是哪个日期。因此，需要进行某种转换。C语言库中承担这一职责的函数是ctime()，即时间转换函数，如清单21-2所示。

### 清单21-2：哦，原来这就是时间！

```c
#include <stdio.h>
#include <time.h>

int main()
{
    time_t tictoc;

    time(&tictoc);
    printf("The time is now %s",ctime(&tictoc));
    return(0);
}
```

ctime()函数接收一个time_t变量的地址。该函数返回一个指向时间戳字符串的指针，这个指针是内存中某个字符数组的地址。该字符串包含一个终止换行符。

- **练习21-3：** 使用清单21-2中的源代码创建一个新程序。别忘了printf()语句中的%s转换字符。编译并运行。输出看起来像这样：

    ```text
    The time is now Mon May 18 13:54:31 2020
    ```

    字符串的后半部分（从Mon开始）是由ctime()函数返回的。

- **练习21-4：** 编写代码，将time_t值94668800传给ctime()函数。输出返回的字符串。

### 解析时间字符串

别担心ctime()返回的字符串，也别担心你的代码需要从中解析才能获得具体的日期或时间信息。这是因为localtime()函数可以与特定的日期或时间值一起使用。这就是为什么localtime()函数可以用来提取当前时间的各个零碎部分。

localtime()函数根据time_t值提取时间和日期信息。它将相关部分填入tm结构体中，该结构体大致如下：

```c
struct tm {
    int tm_sec; /* seconds after the minute [0-60] */
    int tm_min; /* minutes after the hour [0-59] */
    int tm_hour; /* hours since midnight [0-23] */
    int tm_mday; /* day of the month [1-31] */
    int tm_mon; /* months since January [0-11] */
    int tm_year; /* years since 1900 */
    int tm_wday; /* days since Sunday [0-6] */
    int tm_yday; /* days since January 1 [0-365] */
    int tm_isdst; /* Daylight Saving Time flag */
};
```

清单21-3展示了如何使用tm结构体输出可识别的日期和时间格式。

### **清单21-3：** 今天是几号？

```c
#include <stdio.h>
#include <time.h>

int main()
{
    time_t tictoc;
    struct tm *today;

    time(&tictoc);
    today = localtime(&tictoc);
    printf("Today is %d/%d/%d\n",
        today->tm_mon,
        today->tm_mday,
        today->tm_year);
    return(0);
}
```

清单21-3中第9行的*time()*函数获取以Unix纪元滴答数计的当前时间。该值存储在*tictoc*变量中。

在第10行，*localtime()*函数返回**tm**结构体指针*today*。结构体的元素通过*printf()*在几行中输出。由于结构体是一个指针（内存地址），因此使用结构体指针表示法来访问其元素（第12、13和14行）。

- **练习21-5：** 将清单21-3中的源代码输入到你的编辑器中。编译并运行程序以查看当前日期。

    因为图拉真不再是罗马皇帝，而且现在也不是上个月，你必须对代码进行一些调整。参考本节前面给出的结构体定义，你就会明白要输出正确的月份和年份值需要怎样的数学计算。

- **练习21-6：** 修改练习21-5的解决方案，使程序输出当前年份和当前月份。

- **练习21-7：** 编写代码，以`hour:minute:second`的格式输出当前时间。确保分钟和秒的输出为两位数字，并带有前导零。

- **练习21-8：** 修改练习21-7的解决方案，使输出为12小时制，并根据一天中的时间添加A.M.或P.M.后缀。

- **练习21-9：** 编写代码，输出当前星期几的完整名称。

### 睡眠

大多数程序员都希望自己的代码运行得快。偶尔，你会希望代码慢下来，进行一段有节制的暂停，或者营造……悬念！在这些情况下，你可以依靠C语言的时间函数来产生一点点延迟。

sleep()函数是一个常见但非标准的时间函数。它在unistd.h头文件中声明。该函数的参数是暂停程序执行的秒数。

difftime()函数（见清单21-4）在time.h头文件中声明。使用它可以计算代码中now和then这两个time_t值之间的差异。该函数返回一个浮点值，表示经过的秒数。

### 清单21-4：稍等片刻！

```c
#include <stdio.h>
#include <time.h>

int main()
{
    time_t now,then;
    float delay=0.0;

    time(&then);
    puts("Start");
    while(delay < 1)
    {
        time(&now);
        delay = difftime(now,then);
        printf("%f\r",delay);
    }
    puts("\nStop");
    return(0);
}
```

- **练习21-10：** 将清单21-4中的源代码输入到你的编辑器中。编译该程序。运行。

