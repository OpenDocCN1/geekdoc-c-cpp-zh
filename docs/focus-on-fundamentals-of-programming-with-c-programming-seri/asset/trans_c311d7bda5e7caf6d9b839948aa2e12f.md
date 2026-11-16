

## 通过引用将结构体传递给函数

结构体也可以通过引用传递给函数。因此，对在函数中传递的结构体所做的任何更改都会反映回调用函数。

```
// struct8.c

#include <stdio.h>

typedef struct {
    int month;
    int day;
    int year;
} Date;

void foo(Date *now);

int main(void) {
    Date today = { 5, 27, 2013 };
    printf("month = %d day = %d year = %d\n", today.month,
        today.day, today.year);
    foo(&today);
    printf("month = %d day = %d year = %d\n", today.month,
        today.day, today.year);
    return 0;
}

void foo(Date *now) {
    (*now).month = 7;
    (*now).day = 29;
    (*now).year = 2014;
}
```

输出如下：

```
month = 5 day = 27 year = 2013
month = 7 day = 29 year = 2014
```

请注意，如果通过引用传递 `struct`，则必须使用解引用运算符 * 来访问每个字段的值。因为选择运算符（句点）的优先级高于解引用运算符，所以必须在结构体名称和解引用运算符周围使用括号。

然而，将选择运算符（句点）与括号一起使用变得相当笨拙，因此 C 语言专门为此目的添加了一个新的、更简单的运算符。它被称为箭头运算符，由连字符和大于号组成：->

我们可以将上面示例中的函数重写如下：

```
// struct9.c
void foo(Date *now) {
    now->month = 7;
    now->day = 29;
    now->year = 2014;
}
```

因此，选择运算符 (.) 用于访问 `struct` 的成员，而箭头运算符 (->) 用于访问由指针引用的 `struct` 的成员。

## 结构体示例：今天的日期和明天的日期

让我们构建一个程序，它接受今天的日期作为输入并输出明天的日期。我们可以为程序的控制流程开发一个通用算法，如下所示：

```
Input today's date.
Calculate tomorrow's date.
Output today's date.
Output tomorrow's date.
```

由于我们的程序将处理日期，因此通过创建一个名为 Date 的新数据类型将日期的概念建模到程序中似乎很自然，这将允许我们创建多个 Date 结构体。

```
// date1.c
typedef struct {
    int month;
    int day;
    int year;
} Date;
```

我们上面的算法现在变成了 main() 函数的代码：

```
// date2.c
#include <stdio.h>
int main(void) {
    Date today, tomorrow;
    getTodaysDate(&today);
    getTomorrowsDate(today, &tomorrow);
    printf("Today: ");
    printDate(today);
    printf("Tomorrow: ");
    printDate(tomorrow);
    return 0;
}
```

让我们先处理 I/O 函数。请注意，我们创建了一个名为 today 的 Date 结构体来保存今天的日期。我们必须通过引用将此结构体传递给 getTodaysDate() 函数，该函数将提示用户输入当前的月、日和年。

```
// date3.c
void getTodaysDate(Date *today) {
   printf("Enter today's date mm/dd/yyyy: ");
   scanf_s("%d/%d/%d", &today->month, &today->day, &today->year);
}
```

由于 today 被定义为指向 Date 结构体的指针，我们必须使用箭头运算符来解引用结构体并访问结构体的每个组件。但是，因为每个组件变量 today->month、today->day 和 today->year 都在 scanf_s() 语句中使用，所以我们必须对每个变量使用取地址运算符 (&)，因为 scanf_s() 要求变量的地址。

请注意读取数据的 scanf_s() 格式字符串：

```
"%d/%d/%d"
```

指定非格式字符（例如 '/'）会向 scanf_s() 函数表明预期输入为 '/'。这在前面的 printf() 语句的输入提示中显示：

```
mm/dd/yyyy
```

我们的输出函数更简单，因为我们可以按值传递要输出的 Date 结构体。

```
// date4.c
void outputDate(Date d) {
    printf("%d/%d/%d\n", d.month, d.day, d.year);
}
```

接下来是计算明天日期的函数。当今天的日期处于月末或年末时，我们必须小心。我们可以通过设置每个月天数的数组来轻松确定今天的日期是否处于月末。

```
// date5.c
int daysPerMonth[] = {
    31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31
};
```

然后在数组中查找特定月份即可得到该月的天数。对于每个月份 i，daysPerMonth[i-1] 中包含的值对应于该特定月份的天数。

如果确定今天的日期处于月末，那么我们可以通过将月份加 1 并将日期设置为 1 来计算明天的日期。

```
Increment day.
If day is greater than the number of days in the month
    Set day to 1.
    Increment month.
```

我们还必须解决日期出现在第 12 个月末尾的问题。如果是这种情况，我们不仅必须将日期设置为 1，还必须将月份设置为 1 并将年份加 1。

```
Increment day.
If day is greater than the number of days in the month
    Set day to 1.
    Increment month.
    If month is now greater than 12
        Set month to 1.
        Increment year.
```

我们现在按如下方式实现 getTomorrowsDate() 函数：

```
// date6.c
void getTomorrowsDate(Date today, Date *tomorrow) {
    int daysPerMonth[] = {
        31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31
    };

    *tomorrow = today;
    tomorrow->day++;
    if (tomorrow->day > daysPerMonth[tomorrow->month-1]) {
        tomorrow->day = 1;
        ++tomorrow->month;
        if (tomorrow->month > 12) {
            tomorrow->month = 1;
            ++tomorrow->year;
        }
    }
}
```

请注意，我们按值传递 today 给函数，并按引用传递 tomorrow。为什么？我们不希望修改 today 的内容，但确实希望更新 tomorrow 的内容。看看我们的代码多么紧密地遵循我们之前开发的算法。

我们还有一个最终问题需要处理。闰年呢？我们可以使用之前开发的闰年函数：

```
// date7.c

int isLeapYear(int year) {
    return (((year % 4) && (year % 100)) || !(year % 400));
}
```

请注意我们如何将闰年测试集成到函数中：

```
// date8.c

int daysPerMonth[] = {31, 0, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
if (isLeapYear(today.year)) {
    daysPerMonth[1] = 29;
} else {
    daysPerMonth[1] = 28;
}
```

我们的完整程序如下：

```
// date9.c

#include <stdio.h>

typedef struct {
    int month;
    int day;
    int year;
} Date;

int main(void);
void getTodaysDate(Date *today);
void getTomorrowsDate(Date today, Date *tomorrow);
int isLeapYear(int year);
void outputDate(Date d);

int main(void) {
    Date today, tomorrow;
    getTodaysDate(&today);
    getTomorrowsDate(today, &tomorrow);
    printf("Today: ");
    outputDate(today);
    printf("Tomorrow: ");
    outputDate(tomorrow);
    return 0;
}
void getTodaysDate(Date *today) {
    printf("Enter today's date mm/dd/yyyy: ");
    scanf_s("%d/%d/%d", &today->month, &today->day, &today->year);
}
void getTomorrowsDate(Date today, Date *tomorrow) {
    int daysPerMonth[] = {
        31, 0, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31
    };
    if (isLeapYear(today.year)) {
        daysPerMonth[1] = 29;
    }
    else {
        daysPerMonth[1] = 28;
    }
    *tomorrow = today;
    tomorrow->day++;
    if (tomorrow->day > daysPerMonth[tomorrow->month-1]) {
        tomorrow->day = 1;
        ++tomorrow->month;
        if (tomorrow->month > 12) {
            tomorrow->month = 1;
            ++tomorrow->year;
        }
    }
}
int isLeapYear(int year) {
    return ((!year % 4) && year % 100) || !(year % 400));
}
void outputDate(Date d) {
    printf("%d/%d/%d\n", d.month, d.day, d.year);
}
```

