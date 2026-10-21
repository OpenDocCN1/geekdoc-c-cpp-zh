

生成的函数 GenericBubbleSort() 不包含 size 变量，而是使用编译器推导出的值 16 作为 size 参数，该值是传递给函数的数组的大小。

因此，我们可以概括地说，在编译时已知的数值可以作为非类型参数使用。

> 注意 在 C++ 中，有三种数据类型可以作为非类型参数使用，即示例中给出的 int 常量、指向全局函数的指针或引用，以及指向非局部（即静态或全局）对象的指针或引用。这是因为全局函数和全局对象的地址在编译时已知，因此指向它们的指针是允许的。相反，局部对象在运行时被加载到栈上时才获得地址，因此不允许指向它们的指针。

## 7.2.10 模板参数推导

前面已经提到，如果未指定，编译器可以推导参数的类型。模板参数推导具有以下优点：

- 1. 用户可以将模板函数用作普通函数。在示例中，对 GenericBubbleSort(Array4) 函数的调用类似于普通函数调用。因此，如果在库中提供了此类函数，用户可以在不知道该函数不是普通函数而是函数模板的情况下使用它们。
- 2. 每次程序执行时都会自动进行数据类型推导。如果程序后来被修改为接受并处理除之前提供之外的数据类型，例如，如果 Array4 现在改为操作类型 double，则函数调用无需更改。程序下次运行时，编译器会推导出数据类型为 double，并据此实例化函数的正确版本。

> 注意 如果可能，最好让编译器推导参数的类型。只有在存在歧义的情况下，用户才应提供显式参数。

### 推导过程

编译器根据函数调用中传递的参数的类型和值推导出通用参数的类型。参数推导过程比普通函数调用严格得多。如果类型不匹配，参数不会像普通函数中那样被提升。因此，如果 SumIt() 定义如下，则调用 SumIt(12, 12U) 将无法工作：

```
template <typename Type>
SumIt(Type, Type);
```

这是因为传递给 SumIt() 的两个参数不是同一类型；一个是 int，另一个是 unsigned。然而，模板的定义说明 SumIt() 必须有两个完全相同的类型参数，因为 Type 占位符在同一时间点不能有两个值。在这种情况下，编译器无法实例化具有唯一 Type 值的函数。

有趣的是，如果我们定义 SumIt(unsigned, unsigned)（不使用模板），则 SumIt(12, 12U) 将会工作，因为整数（12）会被编译器提升为 unsigned，然后调用其 unsigned 版本，这不是错误。

在某些情况下，编译时无法进行推导。在这些情况下，最好使用参数的显式指定。

![](img/0da15892b2796544fb447dc5727e9ab4_318_0.png)

- 1. 一个这样的例子就是前面给出的 SumIt() 函数。如前所述，SumIt(12, 12U) 将无法工作；相反，可以指定 SumIt <unsigned int> (12, 12U)。这里，Type 被假定为 unsigned int，值 12 将被转换为 unsigned int，然后继续进行处理。

- 2. 将同一函数扩展为返回 long，如果我们写 SumIt <unsigned int>，它将假定参数的类型为 unsigned int，但不会将返回类型假定为 long 类型。因此，我们需要将返回类型指定为 SumIt <long, unsigned int> (12, 12U)。在这种情况下，SumIt() 的定义将更改为

```
template <typename ReturnType, typename Type>
ReturnType SumIt(Type, Type)
```

## 7.2.11 模板函数和特化

可以定义单个模板函数并将其用于生成具有不同数据类型的多个函数。例如，我们已使用通用类型 Type 定义了 GenericBubbleSort()，并使用相同函数处理 int、char 和 employee 类型的数据。在本节中，我们将学习 C++ 如何实现此功能。

当定义模板函数时（例如给定示例中的 GenericBubbleSort() 函数），编译器会自动为实际使用的函数生成正确的代码。在这里，编译器为 int、char 和 employee 类型各创建了三个不同的 GenericBubbleSort() 版本。可以说，编译器自动重载了 GenericBubbleSort()。一个重要事实是，编译器仅为程序中使用的那些类型重载函数，而潜在的可能函数数量很大。

> 注意 以关键字 template 开头的通用函数称为模板函数。自动重载的函数称为模板函数的特化或实例化。生成特化的过程称为实例化。

编译器会自动生成特化。7.2.12 节解释了如果我们希望编译器为除一种情况外的所有情况生成特化会发生什么。

编译器仅为程序中使用的那些类型重载函数，而潜在的可能函数数量很大。

## 7.2.12 重载模板

如 7.2.11 节所述，模板函数在需要时由编译器自动重载。也可以为模板函数提供特定的重载。考虑员工的情况。我们现在有兴趣按部门编号然后按员工编号对他们进行排序。显然，相同的算法将不起作用。我们需要为 employee 类提供一个特殊算法。这在程序 7.7 中显示。

# 程序 7.7 重载模板

```
//OverloadingTemplates.cpp
#include <iostream>
#include <string>
using namespace std;
template <typename Type>
void GenericBubbleSort(Type TempGenericArray[], int Size);
```

```
class employee
{
    int EmpNo;
    string Name;
    string DeptName;
    string Designation;
public:
    employee(int TempNo = 0, string TempName = "", string TempDept = "", string TempDesi = "")
    {
        EmpNo = TempNo;
        Name = TempName;
        DeptName = TempDept;
        Designation = TempDesi;
    }

    bool operator <(employee & OtherEmployee)
    {
        if(EmpNo > OtherEmployee.EmpNo)
            return false;
        else
            return true;
    }

    friend ostream & operator <<(ostream & TempOut, employee & TempEmployee);
    template <> 
    friend void GenericBubbleSort(employee TempEmployee[], int Size);
};
ostream & operator <<(ostream & TempOut, employee & TempEmployee)
{
    TempOut << "Details of employee number" << TempEmployee.EmpNo << "\n";
    TempOut << "Name is" << TempEmployee.Name << "\n";
    TempOut << "Department is" << TempEmployee.DeptName << "\n";
    TempOut << "Designation is" << TempEmployee.Designation << "\n";
    return TempOut;
}

template <typename Type>
void GenericBubbleSort(Type TempGenericArray[], int Size)
{
    for(int i = 0; i < Size - 1; i++)
    {
        for(int j = i + 1; j < Size; j++)
        {
            if(TempGenericArray[i] < TempGenericArray[j])
            {
                Type TempGeneric = TempGenericArray[i];
                TempGenericArray[i] = TempGenericArray[j];
                TempGenericArray[j] = TempGeneric;
            }
        }
    }
}

template <>
void GenericBubbleSort(employee TempEmployee[], int Size)
{
    for(int i = 0; i < Size - 1; i++)
    {
        for(int j = i + 1; j < Size; j++)
```

```
{
    if(TempEmployee[i].DeptName < TempEmployee[j].DeptName)
    {
        employee TempEmp = TempEmployee[i];
        TempEmployee[i] = TempEmployee[j];
        TempEmployee[j] = TempEmp;
    }
    else
    if(TempEmployee[i].DeptName == TempEmployee[j].DeptName)
    {
        if(TempEmployee[i].EmpNo < TempEmployee[j].EmpNo)
        {
            employee TempEmp = TempEmployee[i];
            TempEmployee[i] = TempEmployee[j];
            TempEmployee[j] = TempEmp;
        }
    }
}
}
int main()
{
    employee UniEmployee[10] =
    {
        employee(1, "Lara", "Exam", "Professor"),
        employee(2, "Ponting", "Marksheet", "Clerk"),
        employee(3, "Laxman", "Accounts", "Head Clerk"),
        employee(4, "Flintoff", "Exam", "Clerk"),
        employee(5, "Murlidharan", "Accounts", "CAO"),
        employee(6, "Sarfaraz", "Exam", "Informer"),
        employee(7, "Dean Jones", "Exam", "Invigilator"),
        employee(8, "Madugalle", "Exam", "Examiner"),
        employee(9, "Ganguly", "Marksheet", "Repeater"),
        employee(10, "Nafees", "Accounts", "Clerk")
    };

    int Array2[] = {1,8,9,5,4,12,11,45,23,89,65,34,12,44,65,22};
    char Array3[] = "irngiremxc";

    GenericBubbleSort(Array2,16);
    for(int i = 0; i < 16; i++)
    {
        cout << " " << Array2[i] << ",";
    }
    cout <<"\n";

    GenericBubbleSort (Array3,10);
    for(int i = 0; i < 10; i++)
    {
        cout << " " << Array3[i] << ",";
    }

    GenericBubbleSort(UniEmployee, 10);
    for(int i = 0; i < 10; i++)
    {
        cout << " " << UniEmployee[i] << ",";
    }
}
```

