
输入 arr[1][0] 元素 := 17

输入 arr[1][1] 元素 := 19

输入 arr[1][2] 元素 := 10

输入 arr[1][3] 元素 := 26

数组元素为

行 1-> 12      45      89      11
行 2-> 17      19      10      26

排序后的数组元素为

数组元素为

行 1-> 11      12      45      89
行 2-> 10      17      19      26

**说明：** 前面已经介绍了一维数组排序的逻辑。现在，将二维数组的每一行视为一维数组，排序已经完成。第二个和第三个循环共同执行排序，外层循环对所有行执行此操作。

## /* 程序6.22 方阵对角线元素之和 */

```
#include <iostream.h>
#include <conio.h>
#define R 3
#define C 3

class sqr_mat
{
    int arr[R][C];
public :
    void input();
    int diag_sum();
    void display();
};

void sqr_mat ::input()
{
	int i,j;
	for(i=0;i<R;i++)
	for(j=0;j<C;j++)
	{
		cout << "\nEnter arr[" << i << "][" << j << "] elements :";
		cin >> arr[i][j];
	}
}
```

```
int sqr_mat :: diag_sum()
{
	int i,j,sum = 0;
	for(i=0;i<R;i++)
	{
		for(j=0;j<C;j++)
		if(i==j)
			sum += arr[i][j];
	}
	return sum;
}
```

```
void sqr_mat ::display()
{
	int i, j;
	cout << "Matrix is \n";
	for(i=0;i<R;i++)
	{
		for(j=0;j<C;j++)
		{
			cout << arr[i][j] << "\t";
		}
		cout << endl;
	}
}
```

```
void main()
{
	clrscr();
	sqr_mat obj;
	obj.input();
	cout << "Sum of diagonal elements is" << obj.diag_sum() << endl;
	getch();
}
```

## 输出：

输入 arr[0][0] 元素 := 1
输入 arr[0][1] 元素 := 2
输入 arr[0][2] 元素 := 3
输入 arr[1][0] 元素 := 4
输入 arr[1][1] 元素 := 5
输入 arr[1][2] 元素 := 6
输入 arr[2][0] 元素 := 7
输入 arr[2][1] 元素 := 8
输入 arr[2][2] 元素 := 9
矩阵为
1    2    3
4    5    6
7    8    9
对角线元素之和为 15

## 说明：

行数和列数相等的二维数组称为方阵。对角线元素是指数组中行号和列号相等的那些元素，例如 [0,0]、[1,1]、[2,2] 等。为了求对角线元素之和，我们比较 ‘i’ 和 ‘j’，当它们相等时，将 arr[i][j] 加到 sum 中。这个操作在函数 diag_sum( ) 中完成。

```
/*PROG 6.23 DEMO OF STRING, FINDING LENGTH VER 1 */
```

```
#include <iostream.h>
#include <conio.h>
class demo_str
{
char str[12];
int len;
public :

void input( )
{
	cout << "ENTER A STRING :=";
	cin >> str;
}

void find_len( )
{
	int i=0;
	while(str[i++]!=0);
	len =i;
}

void show( )
{
	cout << "String :=" << str << endl;
	cout << "Length :=" << len << endl;
}
};

void main( )
{
	demo_str str;
	clrscr( );
	str.input( );
	str.find_len( );
	str.show( );
	getch( );
}
```

输出：

输入一个字符串 :=Hari Mohan

字符串 :=Hari

长度 :=5

字符串只不过是以空字符 `\0` 结尾的字符数组。我们有三个函数：input、find_len 和 show。函数 input 从用户获取输入，并将字符串存储在变量 str 中。函数 find_len 通过控制变量 i 查找字符串的长度，直到 str[i]!=0。while 循环的循环体只是一个空语句。最后，当循环终止时，将 `` 赋给 len。通过 show 我们显示 str 和 len。从输出可以得出，cin 在第一个空白字符处停止，并且“hari”（包括它停止处的空格）被赋给 str。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_252_0.png)

# 图6.3 cin语句的逻辑实现。

若要扫描整个字符串，请参见下一个程序。

```
/* PROG 6.24 DEMO OF STRING, FINDING LENGTH OF STRING VER 2*/
```

```
#include <iostream.h>
#include <conio.h>

class demostr
{
    char str[12];
    int len;

public :

    void input()
    {
        cout << "Enter a string \n";
        cin.getline(str,12);
    }

    void find_len()
    {
        int i =0;
        while(str[i]!=0)
        i++;
        len = i;
    }

    void show()
    {
        cout << "String := " << str << endl;
        cout << "Length := " << len << endl;
    }
};
void main()
{
    demostr str;
    clrscr();
    str.input();
    str.find_len();
    str.show();
    getch();
}
```

输出：

输入一个字符串
Hari Mohan
字符串 :=Hari Mohan
长度 :=11

说明：getline 函数会扫描整行，直到按下回车键或先扫描了最多19个字符。该函数甚至会扫描空白字符，如空格、制表符等。这次整个字符串被扫描，输出也如我们所预期。

## /* 程序6.25 字符串字符大小写转换 */

```
#include <iostream.h>
#include <conio.h>
#include <ctype.h>
class demo_str_case
{
    char str[12];

public :

    void input();
    void change_case();
};
void demo_str_case ::input()
{
    int i=0;
    cout<<"ENTER A STRING \n";
    char ch;
    ch=cin.get();
    while(i<12)
    {
        str[i]=ch;
        if(ch=='\n' || i==11)
        {
            str[i] = '\0';
            break;
        }
        ch = cin.get();
        i++;
    }
}
void demo_str_case ::change_case()
{
int i =0;
    char ch;
    while(str[i]!=0)
    {
        if(islower(str[i]))
        {
            ch = str[i]-32;
            cout.put(ch);
        }
        else if(isupper(str[i]))
        {
            ch = str[i]+32;
            cout.put(ch);
        }
        else
            cout.put(str[i]);
        i++;
    }
}
void main()
{
    demo_str_case str;
    clrscr();
    str.input();
    cout<<"STRING IN CHANGE CASE"<<endl;
    str.change_case();
    getch();
}
```

输出：

输入一个字符串
Hari Mohan
字符串大小写转换
hARI mOHAN

说明：在函数 input 中，我们借助 cin.get( ) 函数逐字符获取输入，该函数每次从键盘接受一个字符。字符数组 str 的最大大小为 12，因此我们使用一个控制变量 ‘i’ 运行 while 循环，当 ‘i’ 达到循环上限时退出循环。但在那之前，我们将空字符赋给 str[i] 以表示字符串结束。在函数 change_case 中，我们通过宏 islower 检查字符串 str 的每个字符是否为小写，通过宏 isupper 检查是否为大写，这要感谢 ctype.h。如果字符是小写，我们将其减去 32；如果字符是大写，我们将其加上 32。如果字符不是字母，则直接显示。

```
/*PROG 6.26 REVERSE A STRING */
```

```
#include <iostream.h>
#include <string.h>
#include <conio.h>

class string
{
    char str [20];
    int len;
public :
    void input( )
    {
        cout<<"Enter a string \n";
        cin.getline(str,20);
        len=strlen(str);
    }
    char* reverse( )
    {
        int i,j;
        char* rev = new char[len+1]; // Dynamic memory allocation
        for(i=len-1,j=0;i>=0 && j<len;i--,j++)
            rev[j]=str[i];
        rev[j]='\0';
        return rev;
    }
};
```

```
void main()
{
    string obj;
    clrscr();
    obj.input();
    cout << "Reverse string is\n";
    cout << obj.reverse() << endl;
    getch();
}
```

输出：

输入一个字符串
NMIMS
反转字符串为
SMIMN

说明：反转字符串的逻辑非常简单。我们从字符串末尾取出最后一个字符，放到新的反转字符串的起始位置。然后递减原字符串的计数器，递增反转字符串的计数器（即本例中的 j++ 和 i--）。由于我们是逐字符反转字符串，所以在复制完成时必须添加空字符。请注意，用于反转字符串的空间是根据原字符串的长度动态分配的。

## /* 程序6.27 检查字符串是否为回文 */

```
#include <iostream.h>
#include <string.h>
#include <conio.h>

class string
{
    char str[20];
    int len;

public :

    void input()
    {
        cout << "Enter a string \n";
        cin.getline(str,20);
        len=strlen(str);
    }
```

```
char* reverse()
{
    int i,j;
    char* rev= new char[len +1];
    for(i=len-1,j=0;i >=0 && j<len;i--,j++)
        rev[j]=str[i];
    rev[j]='\0';
    return rev;
}

void checkpalin()
{
    if(strcmp(reverse(),str)==0)
        cout<<"String is palindrome\n";
    else
        cout<<"String is not palindrome\n";
}
};
void main()
{
    string obj;
    clrscr();
    obj.input();
    cout<<"Reverse string is \n";
    cout<<obj.reverse()<<endl;
    obj.checkpalin();
    getch();
}
```

输出：

（第一次运行）

输入一个字符串
HARI
反转字符串为
IRAH
字符串不是回文

（第二次运行）
