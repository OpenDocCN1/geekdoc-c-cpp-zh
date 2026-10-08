

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

# 输出：

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

scan 函数的用法与普通变量类似，除了变量名有所不同外，没有其他区别。图 6 展示了这种差异：

![](img/5d422ba7108ffdf64376be51eaf0c459_239_0.png)

在图 6 中，`contact1` 指的是结构体类型的变量，而 `c_name` 是在模板中定义的数据成员。为了将它们关联起来，我们在两者之间加了一个点。因此，现在可以轻松地区分两个数据元素，例如，`contact1.c_email` 和 `contact2.c_email` 指的是两个完全不同的数据元素。第一个数据元素指的是 `contact1` 的电子邮件，而第二个数据元素指的是 `contact2` 的电子邮件。

在程序 2 中，我们要求用户通过键盘输入结构体数据成员的值。也可以预先定义这些值。下一节将讨论如何预定义结构体数据成员的值。

### 11.6 初始化结构体成员

与其他变量类似，结构体变量可以在声明时进行初始化。程序 3 展示了在编译时初始化结构体变量：

**▶ 程序 3**

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

# 程序 5

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
/* 主函数结束 */

**输出：**

请输入信息：

