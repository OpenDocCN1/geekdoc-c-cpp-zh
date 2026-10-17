
现在我们可以定义图 2 中所示的结构 `contact` 的变量了。假设我们需要定义两个联系人，那么定义方式如下所示：

```
struct contact contact1, contact2;
```

我们声明了两个类型为 `contact` 的结构变量，即 `contact1` 和 `contact2`。正如在图 3 中所示，每个这样的结构变量现在都可以包含一个名为 `c_name` 的字符串（保存 25 个字符），一个名为 `li_phoneno` 的无符号长整型变量，以及一个名为 `c_email` 的字符串（保存 30 个字符）：

![](img/5d422ba7108ffdf64376be51eaf0c459_235_0.png)

**图 3：占据独立内存空间的结构变量**

正如前文所述，结构在与其结构变量关联之前不占用任何内存。在声明两个结构变量的上述情况中，结构 `contact` 的声明不会占用任何内存，直到结构变量 `contact1` 和 `contact2` 被声明。因此，结构的成员在与结构变量关联之前不具有任何存在性。

结构变量也可以在声明模板时定义，如表 1 所示：

**表 1：结构的替代定义方式**

| 方法 1 | 方法 2 |
| :--- | :--- |
| `struct contact` | `struct` |
| `{` | `{` |
| `char c_name[25];` | `char c_name[25];` |
| `unsigned long int li_phoneno;` | `unsigned long int li_phoneno;` |
| `char c_email[30];` | `char c_email[30];` |
| `} contact1, contact2;` | `} contact1, contact2;` |

从表 1 可以看出，我们在终止结构模板之前声明了变量。虽然表 1 中提到的两种方法在 C 语言中均可用，但程序员很少使用它们来声明结构。第二种不包含模板名称的定义不允许我们在程序中声明新的结构变量。

与普通变量类似，结构变量也会预留内存空间。这种内存空间不像 `int`、`char` 和其他数据类型那样是预定义的，因为结构中的成员数量可能会变化。C 语言提供了一种特殊运算符来查找结构的大小。`sizeof` 运算符的用法将在下一节中展示。

### 11.4 结构变量的大小

分配给结构的内存大小等于其包含的所有数据成员大小之和。程序 1 演示了结构模板的声明、结构变量的定义以及打印结构类型变量所占用的内存：

**程序 1**

```c
/* 演示结构大小的程序 */
#include<stdio.h>
/* main 函数开始 */
main()
{
  /* 结构声明 */
  struct contact
  {
    char c_name[25];
    unsigned long int li_phoneno;
    char c_email[30];
  };
  /* 显示结构 contact 的大小 */
  printf("The size of structure contact is %d\n", sizeof(struct contact));
  return;
}
/* main 函数结束 */
```

**输出：**

```
The size of structure contact is 64
```

在程序 1 中可以观察到，程序的输出是 64 字节，而不是预期的 59 字节。编译器在为结构变量分配内存时，如果需要，会添加额外的字节，以便按照最大尺寸的数据成员对齐所有数据成员的地址。这就是我们得到 64 字节而不是 59 字节的原因。

让我们更清楚地理解这个概念。对于模板 `contact`，`char` 数据类型占用 1 个字节，而 `unsigned long int` 占用 4 个字节。两者中较大的尺寸是 4 个字节。因此，编译器将所有变量地址对齐到 4 的倍数。因此，第一个变量 `c_name` 将占用 28 (25 + 3) 个字节，`unsigned long int` 将占用 4 个字节，而 `c_email` 将占用 32 (30 + 2) 个字节。如图 4 所示，编译器额外添加了 3 + 2 = 5 个字节，以均匀对齐所有结构成员：

![](img/5d422ba7108ffdf64376be51eaf0c459_236_0.png)

这种额外的字节填充也称为结构成员对齐。用于对齐地址的额外字节被称为孔（holes）。进行这种填充是为了使结构的每个成员都能更快地访问，而不会延迟。现代中央处理单元 (CPUs) 在基本数据类型（如整型和浮点型）存储在以其长度为倍数的内存地址中时，数据传输性能更好。具有非对齐内存分配的数据成员需要额外的数据传输，从而导致性能下降。

建议在声明结构时将相同数据类型的成员组合在一起，以最小化对齐所需的额外填充字节。例如，如果图 4 中所示的结构定义如 图 5 所示，单个结构成员将占用 60 字节，而不是 64 字节：

![](img/5d422ba7108ffdf64376be51eaf0c459_237_0.png)

**图 5：重新排列结构成员后的结构**

如图 4 和图 5 所示，两个具有相同数据元素但数据元素排列不同的结构，会产生大小不同的结构。

### 11.5 给结构成员赋值

正如前文所述，结构成员与结构变量相关联。结构的每个数据成员都可以作为独立的变量使用。要访问数据成员，我们需要在成员和结构的变量之间建立链接。这种链接使用成员运算符 `"."`（点）建立。程序 2 演示了点运算符的用法：

**程序 2**

```c
/* 使用结构存储和检索联系人的程序 */
#include<stdio.h>
/* main 函数开始 */
main()
{
/* 结构声明 */
struct contact
{
char c_name[25];
char c_email[30];
unsigned long int li_phoneno;
};

/* 结构别名 */
typedef struct contact Contact;

/* 结构体变量声明 */
Contact contact1, contact2;

/* 初始化 contact1 的结构体成员 */
printf("请输入联系人 1 的信息：\n");
scanf("%[^\n]",contact1.c_name);
printf("\n 请输入电话号码： ");
scanf("%ld",&contact1.li_phoneno);
printf("\n 请输入电子邮件地址： ");
scanf(" %s",contact1.c_email);

/* 初始化 contact2 的结构体成员 */
printf("\n请输入联系人 2 的信息：\n");
scanf("\n 请输入姓名： ");
scanf(" %[^\n]", contact2.c_name);
printf("\n 请输入电话号码： ");
scanf("%ld",&contact2.li_phoneno);
printf("\n 请输入电子邮件地址： ");
scanf(" %s", contact2.c_email);

/* 显示 contact1 的结构体成员 */
printf("\n以下是最近输入的联系人信息...");
printf("\n联系人 1 的信息\n");
printf("  姓名 : %s\n",contact1.c_name); /* 显示结构体
成员值 */
printf("  电话号码 : %ld\n", contact1.li_phoneno);
printf("  电子邮件地址 : %s\n", contact1.c_email);
printf("\n联系人 2 的信息\n");
printf("  姓名 : %s\n",contact2.c_name);
printf("  电话号码 : %ld\n", contact2.li_phoneno);
printf("  电子邮件地址 : %s\n", contact2.c_email);
return;
}
/* 主函数结束 */
```

##### 输出：

请输入联系人 1 的信息：

请输入姓名：Harshit Jain

请输入电话号码：2341234

请输入电子邮件地址：harshitjain123@rediffmail.com

请输入信息：

请输入姓名：Vidita Arolikar

请输入电话号码：30063450

请输入电子邮件地址：vidital23_aroikar@yahoo.com

以下是最近输入的联系人信息...

联系人 1 的信息

姓名 : Harshit Jain

电话号码 : 2341234

电子邮件地址 : harshitjain123@reddiffmail.com

联系人 2 的信息

姓名 : Vidita Aroldar

电话号码 : 30063450

电子邮件地址 : vidita123_arolokar@yahoo.com

可以看到，在程序 2 中，我们使用了诸如 `scanf("%[^\n]",contact1.c_name)`、`scanf("%ld", &contact1.li_phono)` 和 `scanf("%s", contact1.c_email)` 这样的语句来接收用户输入的值。

`scan` 函数的用法与普通变量类似，除了变量名有所不同外，没有其他区别。图 6 展示了这种差异：

![](img/5d422ba7108ffdf64376be51eaf0c459_239_0.png)

在图 6 中，`contact1` 指的是结构体类型的变量，而 `c_name` 是在模板中定义的数据成员。为了将它们关联起来，我们在两者之间加了一个点。因此，现在可以轻松地区分两个数据元素，例如，`contact1.c_email` 和 `contact2.c_email` 指的是两个完全不同的数据元素。第一个数据元素指的是 `contact1` 的电子邮件，而第二个数据元素指的是 `contact2` 的电子邮件。

在程序 2 中，我们要求用户通过键盘输入结构体数据成员的值。也可以预先定义这些值。下一节将讨论如何预定义结构体数据成员的值。

### 11.6 初始化结构体成员

与其他变量类似，结构体变量可以在声明时进行初始化。程序 3 展示了在编译时初始化结构体变量：

**▶ 程序 3**

```c
/* 程序：在声明时初始化一个新联系人 */
#include<stdio.h>
/* 主函数开始 */
main()
{
/* 结构体声明 */
struct contact
{
    char c_name[25];
    char c_email[30];
    unsigned long int li_phoneno;
};
/* 结构体别名 */
typedef struct contact Contact;
/* 在声明时初始化结构体变量 */
Contact contact1= {"Harshit Jain","harshitjain123@rediffmail.com",2341234};
/* 打印结构体数据元素 */
printf("\n联系人 1 的信息....\n");
printf(" 姓名 : %s\n",contact1.c_name);
printf(" 电话号码 : %ld\n", contact1.li_phoneno);
printf(" 电子邮件地址 : %s\n", contact1.c_email);
return;
}
/* 主函数结束 */
```

**输出：**

联系人 1 的信息

  姓名 : Harshit Jain

  电话号码: 2341234

  电子邮件地址: harshitjain123@rediffmail.com

在程序 3 中，结构体变量的数据成员可以在定义时赋值。由于在 C 语言中结构体被用作数据类型，我们可以将一个结构体的值赋值给另一个结构体。结构体赋值的语法如下：

```
结构体变量 1 = 结构体变量 2;
```

但是，要执行赋值操作，两个结构体变量必须是相同的数据类型。程序 4 说明了如何将结构体变量 `contact1` 的所有数据成员的值复制到 `contact2` 中：

**▶ 程序 4**

```c
/* 程序：复制结构体变量 */
#include<stdio.h>
/* 主函数开始 */
main()
{
/* 结构体声明 */
struct contact
{
    char c_name[25];
    char c_email[30];
    unsigned long int li_phoneno;
};
/* 结构体别名 */
typedef struct contact Contact;
/* 在声明时初始化结构体变量 */
Contact contact1= {"Harshit Jain","harshitjain123@rediffmail.com",2341234};
/* 将联系人 1 的值赋给联系人 2 */
Contact contact2=contact1;
/* 打印结构体数据元素 */
printf("联系人 1 的详细信息....\n");
printf(" 姓名 : %s\n",contact1.c_name);
printf(" 电话号码 : %ld\n", contact1.li_phoneno);
printf(" 电子邮件地址 : %s\n", contact1.c_email);
printf("联系人 2 的详细信息....\n");
printf(" 姓名 : %s\n",contact2.c_name);
printf(" 电话号码 : %ld\n", contact2.li_phoneno);
printf(" 电子邮件地址 : %s\n", contact2.c_email);
return;
}
/* 主函数结束 */
```

**输出：**

联系人 1 的详细信息....

姓名: Harshit Jain

电话号码: 2341234

电子邮件地址: harshitjain123@rediffmail.com

联系人 2 的详细信息....

姓名: Harshit Jain

电话号码: 2341234

电子邮件地址: harshitjain123@rediffmail.com

可以看到，在程序 4 中，联系人 1 的所有数据元素的输出数据都被复制到了联系人 2 的数据元素中。在之前讨论的所有程序中，结构体数据成员的数据类型都是基本类型。也可以将派生数据类型与结构体数据类型一起使用。例如，我们可以定义数据类型为结构体的数据成员。在内部定义了其他结构体作为数据成员的结构体称为嵌套结构体。下一节将详细讨论嵌套结构体。

### 11.7 嵌套结构体

我们已经知道，结构体可以保存不同基本数据类型的成员，如整型、字符型、浮点型和双精度浮点型，以及像数组这样的派生数据类型。有趣的是，结构体还可以保存数据类型为结构体的数据成员。需要作为数据成员使用的结构体必须在使用它的结构体之前声明。

假设我们需要存储迄今为止在程序中使用的每个联系人的出生日期。我们知道出生日期由三个部分组成，即日、月和年。有时，需要对这些出生日期的各个组成部分进行计算。例如，要计算一个人的年龄，需要计算当前日期和出生日期之间的差值。因此，建议将日、月和年存储在单独的变量中。将它们存储在不同的变量中，并将它们作为一个组保存在结构体中，将使其使用更加容易。程序 5 说明了嵌套结构体的使用：

#### 程序 5

```c
/* 程序：说明结构体中的结构体 */
#include<stdio.h>
/* 主函数开始 */
main()
{
   /* 结构体声明 */
   struct date
   {
       unsigned int i_dd;
       unsigned int i_mm;
       unsigned int i_yyyy;
   };
   struct contact
   {
       char c_name[25];
       char c_email[30];
       unsigned long int li_phoneno;
       struct date dob;
       /* 结构体内部定义的结构体变量 */
   };
   typedef struct contact Contact;
   Contact contact1;
   /* 初始化 contact1 的结构体成员 */
   printf("\n 请输入信息：\n");
   printf("\n 请输入姓名： ");
   scanf(" %[\n]", contact1.c_name);
   printf("\n 请输入电话号码： ");
   scanf("%ld", &contact1.li_phoneno);
   printf("\n 请输入电子邮件地址： ");
   scanf(" %s", &contact1.c_email);
   printf("\n 请输入出生日期 (dd mm yyyy)： ");
   scanf("%u %u %u", &contact1.dob.i_dd, &contact1.dob.i_mm,
   &contact1.dob.i_yyyy);
   /* 打印结构体数据元素 */
   printf("\n最近输入的联系人信息....\n");
   printf(" 姓名 : %s\n\n", contact1.c_name);
   printf(" 电话号码 : %ld\n\n", contact1.li_phoneno);
   printf(" 电子邮件地址 : %s\n\n", contact1.c_email);
   printf(" 出生日期 : ");
   printf("%u-%u-%u\n\n", contact1.dob.i_dd, contact1.dob.i_mm,
   contact1.dob.i_yyyy);
   return;
}
```
