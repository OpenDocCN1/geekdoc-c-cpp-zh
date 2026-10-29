

## 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂版面中提取结构化信息。随着数字化办公的普及，文档格式日益多样化，传统的解析方式已难以满足需求。

本方法基于深度学习技术，结合版面分析与语义理解，实现了对标题、段落、表格、图片等元素的精准识别与定位。实验结果表明，该方法在多个公开数据集上均取得了优异的性能。

- 支持多种文档格式（PDF、Word、扫描件等）
- 高精度版面元素识别
- 输出结构化 Markdown 格式
- 提供坐标定位信息

下图展示了系统的整体架构，包括预处理模块、版面分析模块和内容提取模块。

![](img/202cface8244f523c2641baa2e00d7dd_488_0.png)

```
{
    elNum = idnum;
    currentFloor = cfloor;
    highestFloor = maxFloor;
}
void Elevator::request(int newfloor)
{
    if (newfloor < 1 || newfloor > highestFloor || newfloor == currentFloor)
        ; // do nothing
    else if (newfloor > currentFloor) // move elevator up
    {
        cout << "\nElevator " << elNum
             << " starting at floor " << currentFloor << endl;
        while (newfloor > currentFloor)
        {
            currentFloor++; // add one to current floor
            cout << " Going Up - now at floor " << currentFloor << endl;
        }
        cout << "Elevator " << elNum
             << " stopping at floor " << currentFloor << endl;
    }
    else // move elevator down
    {
        cout << "\nElevator " << elNum
             << " starting at floor " << currentFloor << endl;
        while (newfloor < currentFloor)
        {
            currentFloor--; // subtract one from current floor
            cout << " Going Down - now at floor " << currentFloor << endl;
        }
        cout << "Elevator "<< elNum
             << " Stopping at floor " << currentFloor << endl;
    }
    return;
}
```

```
int main()
{
    Elevator a;  // declare 1 object of type Elevator

    a.request(6);
    a.request(3);

    return 0;
}
```

## 信息点

## 封装

术语封装指的是将若干项打包成一个单一单元。例如，函数用于封装算法的细节。同样地，一个类将变量和方法一起封装在一个单一的包中。尽管“封装”有时被用来指代数据隐藏的过程，但这种用法在技术上并不准确。术语“信息隐藏”指的是封装并隐藏所有实现细节。

在 main() 函数中包含了三个类方法调用。第一个语句创建了一个名为 a 的 Elevator 类型对象。因为没有给出楼层，所以使用了构造函数的默认参数。这意味着电梯被指定为电梯编号 1，它从 1 层开始运行，并且只能上到 15 层。然后发出请求将电梯移动到 6 层，之后又发出请求移动到 3 层。程序 10.6 产生了以下输出：

```
Elevator 1 starting at floor 1
Going Up - now at floor 2
Going Up - now at floor 3
Going Up - now at floor 4
Going Up - now at floor 5
Going Up - now at floor 6
Elevator 1 stopping at floor 6
```

```
Elevator 1 starting at floor 6
Going Down - now at floor 5
Going Down - now at floor 4
Going Down - now at floor 3
Elevator 1 stopping at floor 3
```

在程序 10.6 中，注意 main() 函数提供的控制。这种顺序控制，使用对同一对象操作的两次调用并且使用不同的参数值，适合用于测试目的。然而，通过在 while 循环中加入对 request() 的调用并使用随机数函数 rand() 生成随机的楼层请求，可以实现电梯操作的连续模拟（参见练习 6）。

## 练习 10.4

- 1. （练习） 在你的计算机上输入并运行程序 10.5。
- 2. （修改） 修改程序 10.5 中的 main() 函数以创建一个长度为 9、宽度为 12 的第二个房间。让程序计算这个新房间的面积。

3. （修改） a. 修改程序 10.5 中的 main() 函数以创建四个房间：大厅、厨房、餐厅和客厅。这些房间的尺寸如下：
大厅：长度 = 12.40，宽度 = 3.5
厨房：长度 = 14，宽度 = 14
客厅：长度 = 12.4，宽度 = 20
餐厅：长度 = 14，宽度 = 10.5。

你的程序应显示每个房间的面积以及四个房间总面积之和。

4. （练习） 在你的计算机上输入并运行程序 10.6。

5. （修改） a. 修改程序 10.6 中的 main() 函数以投入第二部电梯服务，从 5 层开始，最大楼层为 20。让这第二部电梯移动到 1 层然后移动到 12 层。
b. 通过在其中添加一条消息来验证构造函数是否被调用，该消息在每次创建新对象时都会显示。运行你的程序以验证其操作。

6. （修改） 修改程序 10.6 中的 main() 函数以使用一个 while 循环，该循环调用 Elevator 的 request() 方法并传入 1 到 15 之间的随机数。如果随机数与电梯当前楼层相同，则生成另一个请求。while 循环应在完成五次有效请求并由电梯移动满足后终止。（提示：回顾第 6.8 节关于随机数的使用。）

7. （程序） 构造一个名为 Light 的类来模拟交通灯。该类的颜色属性应通过类的 change() 方法从绿灯变为黄灯再变为红灯然后再变回绿灯。当创建新的 Light 对象时，其初始颜色应为红灯。

8. （程序） a. 构造一个类定义来表示公司员工。每个员工由一个整数 ID 号、一个双精度工资率以及每周应工作最大小时数定义。该类应提供以下服务：为新员工输入数据的能力、更改新员工数据的能力以及显示新员工现有数据的能力。
b. 将为练习 8a 创建的类定义包含在一个工作的 C++ 程序中，该程序要求用户为三名员工输入数据然后显示输入的数据。
c. 修改为练习 8b 编写的程序以包含一个菜单，为用户提供以下选择：

- 1. 添加员工
- 2. 修改员工数据
- 3. 删除员工
- 4. 退出此菜单

根据用户的选择，程序应启动操作以实现该选择。

9. （程序） a. 构造一个类定义来表示食物类型。食物类型被归类为基本或加工。基本食物进一步被归类为乳制品、肉类、水果、蔬菜或谷物。该类应提供以下服务：为新食物输入数据的能力、更改新食物数据的能力以及显示新食物现有数据的能力。
b. 将为练习 9a 创建的类定义包含在一个工作的 C++ 程序中，该程序要求用户为四种食物项目输入数据然后显示输入的数据。
c. 修改为练习 9b 编写的程序以包含一个菜单，为用户提供以下选择：

- 1. 添加食物项目
- 2. 修改食物项目
- 3. 删除食物项目
- 4. 退出此菜单

根据用户的选择，程序应启动操作以实现该选择。

## 10.5 类作用域和持续期类别

正如你在第 6.4 节中学到的，标识符的作用域定义了标识符在程序中有效的部分。作用域有两类：局部和全局。此外，每个标识符都有一个持续期，它指的是为变量或方法保留存储位置的时间长度，该变量或方法由标识符命名（参见第 6.5 节）。

正如变量是声明它的方法的局部变量一样，类数据成员是局部于它们被声明的类。这意味着类数据成员仅在类内部已知，其中包括类方法。同样地，正如方法中的局部变量总是优先于同名全局变量一样，类数据成员优先于同名全局变量。此外，类方法名是局部于它们被声明的类，只能由为该类声明的对象使用。图 10.4 说明了以下声明的作用域规则：

```
double rate;  // global scope
// class declaration section
class Test
{
private:
    double amount, price, total;  // class scope
public:
    double extend(double, double); // class scope
};
```
