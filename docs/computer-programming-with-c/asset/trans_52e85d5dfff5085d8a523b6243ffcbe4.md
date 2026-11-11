
将使用对象 p1 调用函数 `add()`，并将对象 p2 作为参数传入。该语句执行 Point 对象 p1 与 p2 的加法，并将加法结果存储到对象 p3 中。因此，对象 p3 的 x 和 y 值将分别为 15 和 35。

最后，我们通过对 p3 调用 `output()` 函数，将结果打印到计算机屏幕上。

> **能否在单条语句中相加超过两个 Point 对象？**
> 
> 可以。由于每个 `add()` 函数都会返回一个 Point 对象，因此可以将对 `add()` 的函数调用级联起来。假设我们需要对 5 个 Point 对象 p1、p2、p3、p4、p5 执行加法，并将结果存储到对象 p6 中。通过如下所示级联对 `add()` 的函数调用，可以用单条语句完成整个加法：
> 
> `p6=p1.add(p2).add(p3).add(p4).add(p5);`
> 
> 函数调用将从左到右解析，因此第一次调用 `add()` 将返回一个临时 Point 对象，该对象给出 p1 与 p2 相加的结果。第二次调用 `add()` 函数时使用这个临时对象，并将 p3 作为参数传入。总之，表示前一次加法结果的对象被用来调用下一个 `add()` 函数；因此 p6 将包含所有 Point 对象 p1 到 p5 的加法结果。请记住，之所以能够级联对 `add()` 的函数调用，是因为 `add()` 返回 Point 类的对象。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_584_0.png)

## 11.11 对象数组

与其他任何数组一样，我们也可以在 C++ 中创建对象数组。下面给出创建类对象数组的语法：

```
ClassName ArrayName[size];
```

作为创建对象数组的示例，让我们考虑第 11.6 节中定义的 Employee 类，其私有成员为 id、name 和 salary，公有函数为 input() 和 output()。下面的 C++ 语句创建一个名为 e 的 Employee 对象数组，大小为 3。

```
Employee e[3];
```

注意，数组 e 的每个元素都将是 Employee 类的对象，因为整个数组的数据类型是 Employee。由于数组 e 的大小指定为 3，第一个 Employee 对象可以按 e[0] 访问，第二个 Employee 对象可以按 e[1] 访问，最后一个 Employee 对象可以按 e[2] 访问，如图 11.29 所示。

数组元素 e[0]、e[1] 和 e[2] 实际上都是 Employee 类的独立对象。数组的每个元素都包含成员 id、name 和 salary，如图 11.29 所示。这也意味着我们可以使用每个对象调用成员函数 input() 和 output()。例如，语句

```
e[0].input();
```

![](img/57c0d966bb33c67a5a188e6bf39e4e02_585_0.png)

将使用对象 `e[0]` 调用成员函数 `input()`，因此，input 函数中编写的 `cin` 语句将执行，并从用户处接收员工 `e[0]` 的 id、name 和 salary 作为输入。

类似地，语句

```
e[1].input();
```

以及

```
e[2].input();
```

将分别使用对象 `e[1]` 和 `e[2]` 调用成员函数 `input()`，以从用户处接收每个对象的成员值作为输入。假设用户按如下表格所示输入每个员工对象的 id、name 和 salary：

| 调用 `input()` 函数 | 用户输入的数据（`id, name, salary`） |
|---|---|
| `e[0].input();` | `(1,"John",1000)` |
| `e[1].input();` | `(2,"Jack",5000)` |
| `e[2].input();` | `(3,"Jill",3000)` |

这意味着数组 `e` 在计算机内存中的状态将如图 11.30 所示。

类似地，语句

```
e[0].output();
e[1].output();
e[2].output();
```

将调用 `output()` 函数并执行 `cout` 语句，从而打印各个相应 Employee 对象的成员值。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_586_0.png)

## 11.12 员工管理系统：再探

让我们开发一个 C++ 程序，将 n 名员工的详细信息存储到计算机内存中。由于在编译时 n 的值未知，我们将创建一个大小为 100 的数组 e，并假设员工的最大数量始终 ≤100。下面的语句将创建一个类型为 Employee、大小为 100 的数组 e：

```
Employee e[100];
```

正如稍后在代码中所见，程序还会从用户处接收变量 n 的值作为输入，以确定要存储在计算机内存中的实际员工数量。回想第 11.11 节，数组 e 的每个元素 e[i] 实际上都是 Employee 类的对象，因此我们可以对每个对象 e[i] 调用函数 input()，从用户处接收 e[i] 的成员 id、name 和 salary 作为输入。类似地，我们可以对每个对象 e[i] 调用函数 output()，以打印 e[i] 的成员 id、name 和 salary。在程序中，我们使用了一个简单的 for 循环来遍历数组 e。由于数组中总共有 n 个对象，因此如代码所示，索引值 i 的范围将从 0 到 n−1。

在以下代码中，我们首先在 for 循环中通过对每个 Employee 对象调用 input() 函数，从用户处接收所有员工的数据作为输入，然后使用另一个 for 循环打印每个 Employee 对象的成员，如下所示。

```
#include <iostream.h>
class Employee
{
private:
        int id;
        char name[100];
        int salary;
public:
    void input()
    {
        cin>>id>>name>>salary;
        while(salary<0)
        {
            cout<<"Salary cannot be negative, please re-enter its value";
            cin>>salary;
        }
    }
    void output()
    {
        cout<<id<<"   "<<name<<" "<<salary<<endl;
    }
};
void main()
{
    Employee e[100];
    int i,n;
    cout<<"Enter the total number of employees"<<endl;
    cin>>n;
    for(i=0;i<=n-1;i++)
    {
        cout<<"Enter the details of Employee Number "<<i+1<<endl;
        e[i].input();
    }
    cout<<"Employee details are"<<endl;
    for(i=0;i<=n-1;i++)
    {
        e[i].output();
    }
}
```

### 输出：

```
Enter the total number of employees
2
Enter the details of Employee Number 1
1 John 2000
Enter the details of Employee Number 2
2 Jack 3000
Employee details are
1 John 2000
2 Jack 3000
```

## 11.13 友元函数

到目前为止，我们了解到类的私有成员只能在类内部访问。创建友元函数是这一说法的一个例外，因为友元函数始终位于类外部，但仍然可以访问该类的私有成员。

要创建友元函数，类必须使用关键字 `friend` 为该函数提供原型，如图 11.31 所示。这里，我们通过在类 Pqr 内为函数 `f1()` 提供原型，将函数 `f1()` 创建为类 Pqr 的友元。友元函数的完整函数定义始终位于类外部，因为友元函数不是类的成员。（如图 11.31 所示，函数 `f1()` 只是在类 Pqr 中进行了原型声明，但在类外部定义。）因此，友元函数绝不会像成员函数那样使用类的对象来调用。友元函数必须像任何其他非成员函数一样直接调用。

| 位置 | 内容 |
|---|---|
| **类内** | `class Pqr`<br>`{`<br>`private:`<br>`    int a;`<br>`    int b;`<br>`public:`<br><br>`friend void f1();`<br>`.....`<br>`};`<br>**函数 `f1()` 是类 Pqr 的友元函数。因此，我们使用关键字 `friend` 在类内为函数 `f1()` 提供原型。** |
| **类外** | `void f1()`<br>`{`<br>`Pqr o1;`<br>`o1.a=10;`<br>`o1.b=20;`<br>`........`<br>`}`<br>**友元函数 `f1()` 在类外定义。私有成员 a 和 b 可以在函数 `f1()` 中访问，因为 `f1()` 是类 Pqr 的友元。访问成员时使用如下表示法：** `<ObjectName>.VariableName` **这里 o1 是类 Pqr 的对象。** |

**图 11.31：** 使用友元函数访问类的成员

由于友元函数不是使用任何对象来调用的，因此不能从友元函数中直接访问成员变量。相反，应通过显式给出对象名，后跟成员访问运算符来访问对象的成员，以确定要访问其成员的确切对象。

```
<ObjectName>.VariableName
```

类似地，如果友元函数需要在其定义中调用任何成员函数，则必须显式指定对象名，使用该对象来调用成员函数
