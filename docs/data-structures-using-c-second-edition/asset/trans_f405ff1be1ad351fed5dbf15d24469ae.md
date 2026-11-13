

```c
int main()
{
 typedef struct employee
 {
 int emp_code;
 char name[20];
 };
 FILE *fp;
 struct employee e;
 int i;
 clrscr();
 fp = fopen("employee.txt", "rb");
 if(fp==NULL)
 {
 printf("\n Error opening file");
 exit(1);
 }
 printf("\n THE DETAILS OF THE EMPLOYEES ARE ");
 while(1)
 {
 fread(&e, sizeof(e), 1, fp);
 if(feof(fp))
 break;
 printf("\n\n Employee Code: %d", e.emp_code);
 printf("\n\n Name: %s", e.name);
 }
 fclose(fp);
 getch();
 return 0;
}
```

### 输出

员工代码: 01
姓名: Gargi
员工代码: 02
姓名: Nikita

## 附录 F

### 地址计算排序

编写一个程序，使用地址计算排序对数组元素进行排序。

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX 5
struct node
{
    int data;
    struct node *next;
}*nodes[10]={NULL};

struct node *insert(struct node *start, int num)
{
    struct node *ptr,*new_node;
    ptr=start;
    new_node=(struct node*)malloc(sizeof(struct node));
    new_node->data=num;
    new_node->next=NULL;
    if(start==NULL)
    {
        start = new_node;
    }
    else
    {
        //insert the new node at its right position
        while((ptr->next->data!=num) && (ptr->next!=NULL))
            ptr=ptr->next;
        if(new_node->data < ptr->data)
        {
            new_node->next=ptr;
            start=new_node;
        }
        else
        {
            new_node->next=ptr->next;
            ptr->next=new_node;
        }
    }
    return start;
}
void add_calc_sort(int arr[],int n)
{
    int i,j=0,pos;
    for(i=0;i<n;i++)
    {
        pos = arr[i] / 10;
        nodes[pos]=insert(nodes[pos],arr[i]);
    }
    for(i=0;i<10;i++)
    {
        while(nodes[i]!=NULL)
        {
            arr[++j]=nodes[i]->data;
            nodes[i]=nodes[i]->next;
        }
    }
    printf("\nSorted output is : ");
    for(i=0;i<n;i++)
        printf("%d\t",arr[i]);
    getch();
}
void main()
{
    int arr[MAX],i,n;
    printf("\n Enter the number of elements : ");
    scanf("%d",&n);
    printf("\n Enter the elements : ");
    for(i=0;i<n;i++)
        scanf("%d",&arr[i]);
    addr_calc_sort(arr,n);
}
```

### 输出

输入元素个数 : 5
输入元素 : 23 53 14 78 22
排序后的输出是 : 14 22 23 53 78

## 附录 G

### 答案

## 第 1 章

### 选择题

- 1. (b) 2. (c) 3. (d) 4. (d) 5. (b) 6. (b) 7. (d)
- 8. (c) 9. (e) 10. (d) 11. (c) 12. (b) 13. (c) 14. (a)
- 15. (b)

### 判断题

- 1. 错误 2. 正确 3. 错误 4. 错误 5. 正确 6. 错误 7. 正确
- 8. 错误 9. 正确 10. 错误 11. 错误 12. 错误 13. 正确 14. 正确
- 15. 错误 16. 错误 17. 正确 18. 错误 19. 正确 20. 错误 21. 正确
- 22. 正确 23. 正确 24. 正确 25. 正确

### 填空题

- 1. 丹尼斯·里奇 2. main() 3. ASCII 码
- 4. 操作系统 5. 取模运算符 (%) 6. 一元
- 7. 类型转换 8. 默认情况 9. printf()
- 10. 右括号 11. \n 12. const
- 13. sizeof 14. %hd 15. %x
- 16. – 17. 调用函数 18. 调用函数
- 19. 参数/形参 20. 函数头和函数体 21. 引用调用
- 22. 1 字节 23. NULL 24. 右值
- 25. *

## 第 2 章

### 选择题

- 1. (a) 2. (c) 3. (a) 4. (b) 5. (a) 6. (b) 7. (a)
- 8. (d) 9. (d) 10. (b) 11. (b) 12. (a) 13. (b)

### 判断题

- 1. 错误 2. 正确 3. 错误 4. 错误 5. 错误 6. 正确 7. 错误
- 8. 错误 9. 错误 10. 错误 11. 错误 12. 正确 13. 错误 14. 错误
- 15. 错误

### 填空题

- 1. 数据结构
- 2. 函数
- 3. 数组
- 4. 数据类型
- 5. Root = NULL
- 6. 与详细规格或实现分离考虑
- 7. 输入规模
- 8. 摊还情况
- 9. 下标或索引
- 10. 栈顶
- 11. 窥视
- 12. 尝试向已满的数组、栈或队列中插入元素。
- 13. 队列
- 14. 队尾，队首
- 15. 线性数据结构
- 16. 程序
- 17. 时间复杂度
- 18. 平均情况运行时间
- 19. O(1)
- 20. 模块
- 21. 自顶向下
- 22. 最坏
- 23. Ω
- 24. 非渐近地
- 25. 位于

## 第 3 章

### 选择题

- 1. (b) 2. (b) 3. (d) 4. (b) 5. (b) 6. (d)

### 判断题

- 1. 正确 2. 正确 3. 正确 4. 错误 5. 错误 6. 正确 7. 正确
- 8. 正确 9. 错误 10. 正确 11. 正确 12. 错误 13. 错误 14. 错误
- 15. 正确

### 填空题

- 1. 索引或下标 2. 连续 3. n
- 4. 指针 5. 数据类型、名称和大小 6. 基地址
- 7. 其中存储的元素个数 8. 数组的数组
- 9. 整数值 10. 第四个

## 第 4 章

### 选择题

- 1. (b) 2. (c) 3. (a) 4. (c) 5. (d) 6. (a) 7. (c)
- 8. (b) 9. (b) 10. (b)

### 判断题

- 1. 错误 2. 错误 3. 正确 4. 正确 5. 错误 6. 错误 7. 正确
- 8. 错误 9. 正确 10. 错误 11. 正确 12. 错误 13. 正确 14. 错误
- 15. 错误

### 填空题

- 1. 以空字符结尾的字符数组 2. 空字符
- 3. 5 4. 零 5. 连续
- 6. 99 7. scanf() 8. 65-97
- 9. 将字符转换为大写
- 10. 当按字典顺序 S1 将在 S2 之后 11. 早晨
- 11. strev() 12. 早晨
- 13. 15
- 14. 索引操作 15. str2 小于 str1 16. strlen
- 17. puts

## 第 5 章

### 选择题

- 1. (d) 2. (c) 3. (b) 4. (b) 5. (b) 6. (b) 7. (d)

### 判断题

- 1. 错误 2. 错误 3. 正确 4. 正确 5. 正确 6. 错误 7. 正确
- 8. 错误 9. 错误 10. 正确 11. 正确 12. 正确 13. 正确 14. 错误

### 填空题

- 1. 用户定义 2. 结构体声明 3. 结构体名称
- 4. typedef 5. 零 6. 空字符
- 7. 点运算符 8. 嵌套结构 9. 自引用
- 10. 我们声明一个结构体变量
- 11. 联合体 12. 引用结构体或联合体的各个成员
- 13. 联合体

## 第 6 章

### 选择题

- 1. (b) 2. (c) 3. (d) 4. (c) 5. (b) 6. (d) 7. (b)

### 判断题

- 1. 正确 2. 正确 3. 错误 4. 错误 5. 错误 6. 错误 7. 正确
- 8. 错误 9. 正确 10. 正确

### 填空题

- 1. AVAIL 2. O(1) 3. O(n) 4. 两个 5. 一个 6. 两个 7. 两个
- 8. 一个 9. 两个 10. 一个 11. 节点 12. START 13. 节点 15. 第一个
- 14. 没有可用内存来为要插入的新节点分配空间

## 第 7 章

### 选择题

- 1. (a) 2. (b) 3. (a) 4. (c)

### 判断题

- 1. 错误 2. 正确 3. 正确 4. 正确 5. 错误 6. 正确 7. 错误
- 8. 正确 9. 错误 10. 正确 11. 错误 12. 错误

### 填空题

- 1. 栈 2. 栈 3. O(n)
- 4. 我们尝试从空栈中删除节点 5. 从左到右
- 6. 不失败 7. 直接

## 第 8 章

### 选择题

- 1. (b) 2. (a) 3. (b) 4. (a) 5. (b)

### 判断题

- 1. 错误 2. 错误 3. 错误 4. 正确 5. 错误 6. 正确 7. 正确
- 8. 正确

### 填空题

- 1. 队尾 2. 双端队列 3. O(1)
- 4. 输入受限双端队列 5. 循环数组或循环双向链表
- 6. 优先队列 7. 队列

## 第 9 章

### 选择题

- 1. (a) 2. (a) 3. (d) 4. (a) 5. (c) 6. (d)

### 判断题

- 1. 正确 2. 正确 3. 正确 4. 错误 5. 正确 6. 错误 7. 正确
- 8. 错误

### 填空题

- 1. 祖先 2. 节点 3. 2^(n-1)
- 4. 两个 5. 兄弟节点 6. 结构和内容
- 7. n 和 log(n+1)。 8. 树中的每个节点要么没有子节点，要么恰好有两个子节点
- 9. 前序
- 10. 对源字符每个可能值出现概率的估计。

## 第 10 章

### 选择题

- 1. (a) 2. (b) 3. (b) 4. (d) 5. (a)

### 判断题

- 1. 正确 2. 错误 3. 错误 4. 正确 5. 正确 6. 错误 7. 正确
- 8. 错误 9. 错误 10. 错误

### 填空题

- 1. 双向线索二叉树 2. 右子树 3. 中序后继
- 4. 用左子树的高度减去右子树的高度。
- 5. 树的左子树比右子树低一层。
- 6. O(log n) 7. LL
- 8. 黑色和黑色
- 9. P（n 的父节点）是伸展树的根。
- 10. 伸展

