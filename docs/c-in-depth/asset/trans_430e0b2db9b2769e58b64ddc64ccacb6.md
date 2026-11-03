
```c
printf("Enter the element : ");
scanf("%d",&m);
printf("Enter the position after which this element is inserted : ");
scanf("%d",&position);
addafter(m,position);
break;
case 4:
if(start==NULL)
{
printf("List is empty\n");
continue;
}
printf("Enter the element for deletion : ");
scanf("%d",&m);
del(m);
break;
case 5:
display();
break;
case 6:
printf("Enter the element to be searched : ");
scanf("%d",&m);
search(m);
break;
case 7:
exit();
default:
printf("Wrong choice\n");
}/*End of switch*/
/*End of while*/
/*End of main()*/

create_list(int data)
{
struct node *q,*tmp;
tmp=malloc(sizeof(struct node));
tmp->info=data;
tmp->link=NULL;
if(start==NULL) /*If list is empty*/
start=tmp;
else
{
/*Element inserted at the end*/
q=start;
while(q->link!=NULL)
q=q->link;
q->link=tmp;
}
}
/*End of create_list()*/
```

```c
addatbeg(int data)
{
struct node *tmp;
tmp=malloc(sizeof(struct node));
tmp->info=data;
tmp->link=start;
start = tmp;
}
/*end of addatbeg()*/
```

```c
addafter(int data, int pos)
{
struct node *tmp, *q;
int i;
q=start;
for(i=0;i<pos-1;i++)
{
    q=q->link;
    if(q==NULL)
    {
        printf("There are less than %d elements", pos);
        return;
    }
}
/*End of for*/
tmp=malloc(sizeof(struct node));
tmp->link=q->link;
tmp->info=data;
q->link=tmp;
}
/*End of addafter()*/
```

```c
del(int data)
{
struct node *tmp,*q;
if(start->info==data)
{
    tmp=start;
    start=start->link; /*First element deleted*/
    free(tmp);
    return;
}
q=start;
while(q->link->link!=NULL)
{
    if(q->link->info==data)/*Element deleted in between*/
    {
        tmp=q->link;
        q->link=tmp->link;
        free(tmp);
        return;
    }
    q=q->link;
}
/*End of while */
if(q->info==data) /*Last element deleted*/
{
    tmp=q->link;
    free(tmp);
    q->link=NULL;
    return;
}
printf("Element %d not found\n",data);
}/*End of del()*/
```

```c
display()
{
    struct node *q;
    if(start==NULL)
    {
        printf("List is empty\n");
        return;
    }
    q=start;
    printf("List is :\n");
    while(q!=NULL)
    {
        printf("%d ",q->info);
        q=q->link;
    }
    printf("\n");
}/*End of display() */
```

```c
search(int data)
{
    struct node *ptr=start;
    int pos=1;
    while(ptr!=NULL)
    {
        if(ptr->info==data)
        {
            printf("Item %d found at position %d\n",data,pos);
            return;
        }
        ptr=ptr->link;
        pos++;
    }
    printf("Item %d not found in list\n",data);
}/*End of search() */
```

## 10.15.10 反转链表

让我们取一个链表-

第二节点的链接应指向第一个节点，因此
`p2->link = p1;`
现在我们将使用 p3 指针遍历链表并向前移动指针 p1 和 p2。我们将 p1 设置为 p2 的链接部分，以便每个节点的链接现在指向其前一个节点。

```c
p2->link=p1;
while(p3!=NULL)
{
    p1=p2;
    p2=p3;
    p3=p3->link;
    p2->link=p1;
}
```

当此循环终止时，p3 将为 NULL，p2 将指向最后一个节点，并且每个节点的链接现在指向其前一个节点。现在 start 应指向链表的最后一个节点，即反转后链表的第一个节点。
`start = p2;`

![](img/a76c706396af8b310f291a5313a27079_334_0.png)

如果链表只包含一个元素，则在初始化 p3 时会出现问题，因此我们在开始时检查此条件-

```c
if ( start->link == NULL )
return;
```

以下是反转链表的函数 reverse。

```c
reverse()
{
    struct node *p1,*p2,*p3;
    if(start->link==NULL) /*if only one element in the list*/
    return;
    p1=start;
    p2=p1->link;
    p3=p2->link;

    p1->link=NULL;
    p2->link=p1;

    while(p3!=NULL)
    {
        p1=p2;
        p2=p3;
        p3=p3->link;
        p2->link=p1;
    }
    start=p2;
}
/*End of reverse() */
```

## 10.16 联合

联合是一种派生数据类型，如结构体，它也可以包含不同数据类型的成员。联合的定义、联合变量的声明以及成员的访问所使用的语法与结构体中使用的语法相似，但这里使用关键字 union 而不是 struct。联合与结构体之间的主要区别在于为成员分配内存的方式。在结构体中，每个成员都有自己的内存位置，而联合的成员共享同一内存位置。当声明一个联合类型的变量时，编译器会分配足够的内存来容纳联合中最大的成员。由于所有成员共享同一内存位置，因此我们一次只能使用一个成员。因此联合用于节省内存。联合的概念在不需要同时使用联合的所有成员时很有用。

联合的定义语法为-

```c
union union_name{
    datatype member1;
    datatype member2;
    ...............
};
```

与结构体变量类似，联合变量可以在定义时一起声明或单独声明。例如-

```c
union union_name{
    datatype member1;
    datatype member2;
    ...........
}variable_name;
```

这也可以声明为-
`union union_name variable_name;`

我们可以访问联合成员使用与结构体相同的语法。如果我们有一个联合变量，则可以使用点(.)运算符访问其成员，如果我们有一个指向联合的指针，则可以使用箭头(->)运算符访问其成员。

```c
/*10.16 Program for accessing union members*/
#include<stdio.h>
main()
{
    union result{
        int marks;
        char grade;
        float per;
    }res;
    res.marks=90;
    printf("Marks : %d\n",res.marks);
    res.grade='A';
    printf("Grade : %c\n",res.grade);
    res.per=85.5;
    printf("Percentage : %f\n",res.per);
}
```

输出 :

Marks : 90
Grade : A
Percentage : 85.500000

在第一个 printf 之前，将值 90 分配给联合成员 marks，因此其他成员 grade 和 per 包含垃圾值。在第一个 printf 之后，将值 'A' 分配给联合成员 grade。因此现在另外两个成员 marks 和 per 包含垃圾值。联合一次只能有一个成员保存值，不要尝试同时使用所有成员。因此类型为 result 的联合变量可以被视为 int 变量或 char 变量或 float 变量。跟踪当前保存值的成员是程序员的责任。

联合变量也可以被初始化，但有一个限制。我们知道由于内存共享，所有成员不能同时保存值。因此在初始化期间也只能为一个成员赋初始值，并且这种特权给予第一个成员。因此只能为联合的第一个成员赋初始值。初始化器的类型应与第一个成员的类型匹配。例如，我们可以按如下方式初始化上述联合变量-

```c
union result res ={78};
```

现在我们将编写一个程序并比较为联合和结构体变量分配的内存

```c
/* P10.17 Program to compare the memory allocated for a union and structure variable*/
#include<stdio.h>
struct stag{
    char c;
    int i;
    float f;
};
union utag{
    char c;
    int i;
    float f;
};
main()
{
    union utag uvar;
    struct stag svar;
    printf("Size of svar = %u\n",sizeof(svar));
    printf("Address of svar : %u\t",&svar);
    printf("Address of members : %u %u %u\n",&svar.c,&svar.i,&svar.f);
    printf("Size of uvar = %u\n",sizeof(uvar));
    printf("Address of uvar : %u\t",&uvar);
    printf("Address of members : %u %u %u\n",&uvar.c,&uvar.i,&uvar.f);
}
```

输出 :

Size of svar = 7
Address of svar : 65514 Address of members : 65514 65515 65517
Size of uvar = 4
Address of uvar : 65522 Address of members : 65522 65522 65522

![](img/a76c706396af8b310f291a5313a27079_337_0.png)

![](img/a76c706396af8b310f291a5313a27079_337_1.png)

联合成员的地址相同，而结构体成员的地址不同。变量 svar 和 uvar 大小的差异也表明联合在内存使用上非常经济。请注意，如前所述，联合和结构体变量的大小都可能受到填充的影响。

结构体可以是联合的成员，或者联合可以是结构体的成员。例如-

```c
union result
{
    int marks;
    char grade;
};
```

```c
struct res
{
    char name[15];
    int age;
    union result performance;
} data;
```

这里 data 是类型为 struct res 的结构体变量。它有三个成员，一个字符数组 name，一个整数 age 以及一个联合成员 performance。联合一次只能取一个值，要么是整数值 marks，要么是字符值 grade。这也可以写成-
