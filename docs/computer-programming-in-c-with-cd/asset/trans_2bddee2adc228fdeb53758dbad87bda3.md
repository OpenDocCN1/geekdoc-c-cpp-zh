

```cpp
}

cout << sum;

delete [] arr;

return 0;
}
```

**输出：**

```text
Enter number of digits you want to add: 6

Enter number 1: 25

Enter number 2: 50
Enter number 3: 60

Enter number 4: 78

Enter number 5: 98

Enter number 6: 74
Sum of the Numbers you entered is :
```

### Q7. 编写一个程序，接受用户输入的一个数字，并显示该数字及其倒数。要获得该数字的倒数，必须使用一个单独的函数。

答。

```cpp
#include <iostream.h>

void reciprocal(double *p1)
{
    *p1=1/(*p1);
}

int main()
{
    double n1;
    cout <<"Enter the number whose reciprocal is required ";
    cin >> n1;
    cout<<"\nThe Number you have entered is: "<<n1<<"\n";
    reciprocal(&n1); // calling function with arguments matching the pointer variables
    cout<<"The reciprocal of the number is: "<<n1;

    return 0;
}
```

**输出：**

```text
Enter the number whose reciprocal is required 12.2356

The Number you have entered is: 12.2356
The reciprocal of the number is: 0.0817287
```

### Q8. 编写一个程序，接受用户输入的字符串，并显示其中元音字母的数量。

答。

```cpp
#include <iostream.h>
#include <string.h>

int vowels(char *str)
{
    int NumVowels = 0;
    for (int i=0; str[i] != '\0'; i++)
    {
        if((str[i] == 'A') || (str[i] == 'E') || (str[i] == 'I') ||
           (str[i] == 'O') || (str[i] == 'U') || (str[i] == 'a') || (str[i] == 'e') ||
           (str[i] == 'i') || (str[i] == 'o') || (str[i] == 'u'))
        {
            NumVowels +=1;
        }
    }
    return NumVowels;
}

int main()
{
    char str[50];
    int NumVowels;
    cout<<"Enter string in which you want to find vowels: ";
    cin>>str;
    NumVowels = vowels(str);
    cout<<endl;
    cout<<"The Number of Vowels in the String are: ";
    cout<<NumVowels;

    return 0;
}
```

**输出：**

```text
Enter string in which you want to find vowels: Dheeraj_Gupta

The Number of Vowels in the String are: 5
```

### Q9. 创建一个程序，接受员工的基本工资，然后显示其总工资，总工资包括基本工资以及 D.A. 10%、HRA 25% 和 PF 10.3%。

答。

```cpp
#include <iostream.h>

void Cal_Salary (double *bSal)
{
    double da, hra, pf ;
    da = (*bSal * 10)/100;
    hra = (*bSal * 25)/100;
    pf = (*bSal * 10.3)/100;

    *bSal = *bSal + da + hra + pf;
}

int main()
{
    double bSal, *tSal;
    cout<<"Enter your basic Salary to know Total salary ";
    cin>>bSal;

    tSal = &bSal;
    Cal_Salary (tSal);
    cout<<endl<< *tSal;

    return 0;
}
```

**输出：**

```text
Enter your Basic Salary to know Total salary 1200

1743.6
```

### Q10. 创建一个程序，接受学生获得的分数，并显示结果（通过或未通过）以及等级。如果获得的分数大于或等于 40，则结果为通过，否则为未通过。等级将根据以下标准分配：

| 获得分数 | 等级 |
|---|---|
| 小于 40 | E |
| 40 到 50 之间 | D |
| 50 到 60 之间 | C |
| 60 到 70 之间 | B |
| 大于 70 | A |

答。

```cpp
#include <iostream.h>

char* get_result (int marks)
{
    char *result;
    if (marks < 40)
    {
        result = "F";
    }
    else
    {
        result = "P";
    }
    return result;
}

char* get_grade (int marks)
{
    char *grade;
    if (marks < 40)
    {
        grade = "E";
    }
    if ((marks >=40) && (marks <=50))
    {
        grade = "D";
    }
    if ((marks >50) && (marks <=60))
    {
        grade = "C";
    }
    if ((marks >60) && (marks <=70))
    {
        grade = "B";
    }
    if (marks > 70)
    {
        grade = "A";
    }
    return grade;
}

int main ()
{
    int marks;
    char *result, *grade;
    cout<<"Enter the marks you obtained in the exam: ";
    cin>> marks;
    result = get_result (marks);
    grade = get_grade (marks);
    cout<<"The result of your exam: " << *result<<endl;
    cout<<"Your Grade is: " << *grade;
    return 0;
}
```

**输出：**

```text
Enter the marks you obtained in the exam: 50
The result of your exam: P
Your Grade is: D
```

### Q11. 创建一个程序，接受用户输入的本金和年数。然后按年利率 8% 计算利息，并将其显示在屏幕上。

答。

```cpp
#include <iostream.h>

void Cal_Int (double *Amount, double years)
{
    double interest ;
    interest = (((*Amount) * years * 8) / 100);
    *Amount = *Amount + interest;
}

int main()
{
    double years, P_Amount, *Amount;
    cout<<"Enter principal Amount: ";
    cin>>P_Amount;

    cout<<endl<<"Enter number of years: ";
    cin>>years;

    Amount = &P_Amount;
    Cal_Int (Amount, years);
    cout<<endl<< *Amount;

    return 0;
}
```

**输出：**

```text
Enter principal Amount: 2500

Enter number of years: 10.25

4550
```

### Q12. 创建一个税务计算器，接受员工详细信息，并显示员工应缴纳的税额。

答。

```cpp
#include <iostream.h>

char id[10];
char name[30];
char gender;

void Emp_Detail(double *monthSalary)
{
    cout<<"Enter employee id"<<endl;
    cin>>id;
    cout<<"Enter employee name"<<endl;
    cin>>name;
    cout<<"Enter monthly salary"<<endl;
    cin>>*monthSalary;
    cout<<"Enter gender (M/F)"<<endl;
    cin>>gender;
}

void taxCalculate(double *annualSalary, double *taxRate, double *monthSalary, double *taxAmount)
{
    double *as, *tr, *ms, *ta;
    as = annualSalary;
    tr = taxRate;
    ms = monthSalary;
    ta = taxAmount;

    if(gender=='M'||gender=='m')
    {
        *as=(*ms)*12;

        if((*as>150000)&&(*as<=300000))
        {
            *tr=10;
        }
        if((*as>300000)&&(*as<=500000))
        {
            *tr=20;
        }
        if(*as>500000)
        {
            *tr=30;
        }
        *ta=((*as)*(*tr))/100;
    }

    if(gender=='F'||gender=='f')
    {
        *as=(*ms)*12;

        if((*as>180000)&&(*as<=300000))
        {
            *tr=10;
        }
        if((*as>300000)&&(*as<=500000))
        {
            *tr=20;
        }
        if(*as>500000)
        {
            *tr=30;
        }
        *ta=((*as)*(*tr))/100;
    }
}

void display_Detail(double *annualSalary, double *taxRate, double *monthSalary, double *taxAmount)
{
    double *as, *tr, *ms, *ta;
    as = annualSalary;
    tr = taxRate;
    ms = monthSalary;
    ta = taxAmount;

    cout<<"Employee ID : "<<id<<endl;
    cout<<"Name : "<<name<<endl;
    cout<<"Monthly Salary : "<<*ms<<endl;
    cout<<"Annual Salary : "<<*as<<endl;
    cout<<"Tax Rate : "<<*tr<<endl;
    cout<<"Tax Amount : "<<*ta<<endl;
}

void main()
{
    double *monthSalary, *annualSalary, *taxRate, *taxAmount;
    double monthSalary1, annualSalary1, taxRate1, taxAmount1;
    monthSalary1=annualSalary1=taxRate1=taxAmount1=0;

    monthSalary = &monthSalary1;
    annualSalary = &annualSalary1;
    taxRate = &taxRate1;
    taxAmount = &taxAmount1;

    Emp_Detail(monthSalary);
    taxCalculate(annualSalary, taxRate, monthSalary, taxAmount);
    display_Detail(annualSalary, taxRate, monthSalary, taxAmount);
}
```

**输出：**

```text
Enter employee id

KLSI-0029

Enter employee name

Dheeraj

Enter monthly salary
25000
Enter gender (M/F)
M
Employee ID : KSI-T-0029
Name : Dheeraj
Monthly Salary : 25000
Annual Salary : 300000
Tax Rate : 10
Tax Amount : 30000
```

## 总结

本章中，你学习了使用指针管理内存。还学习了使用指针和指针算术访问并更改数组元素的值。然后，你学习了使用各种运算符，如 &、\*、new 和 delete，这些是在 C++ 中使用指针所必需的。你还学习了以指针变量作为参数的函数，这样在函数体内对变量所做的更改可以反映到函数体外。最后，你学习了创建能够以指针变量形式返回多个值的函数。

## 练习题

- **判断题**

  判断以下陈述是否正确：

  - Q1. 指针是可以存储其他变量引用的变量。**正确**
  - Q2. 使用指针的程序比不使用指针的程序运行得更慢。**错误**
  - Q3. 我们可以直接访问由指针变量所指向的其他变量中存储的值。**正确**
  - Q4. 我们不能在运行时为指针分配内存。**错误**
  - Q5. 指针变量的数据类型必须与其所指向变量的数据类型相同。**正确**
  - Q6. 从内存使用方面看，使用动态指针是可行的。**正确**
  - Q7. 我们可以在运行时使用 delete 运算符释放静态指针的内存。**错误**
  - Q8. & 运算符被称为指向运算符。**错误**
  - Q9. 要声明指针，需使用 `*` 运算符。**正确**

