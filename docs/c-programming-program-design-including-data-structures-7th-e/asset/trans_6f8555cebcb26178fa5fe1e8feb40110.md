
```cpp
for (int i = 0; i < length / 2; i++)        //Step 2
    if (str[i] != str[length - 1 - i])
        return false;

return true;
}
```

# 示例 6-7（有线电视公司）

第4章包含一个用于计算有线电视公司账单的程序。在该程序中，所有编程指令都集中在函数 main 中。这里，我们使用用户自定义函数重写同一个程序，进一步说明结构化程序设计。

由于有两类客户——住宅客户和商业客户，该程序包含两个独立的函数：一个用于计算住宅客户的账单，另一个用于计算商业客户的账单。两个函数都计算账单金额，然后将账单金额返回给函数 main。函数 main 打印应付金额。我们将计算住宅账单的函数称为 `residential`，将计算商业账单的函数称为 `business`。计算账单的公式与之前相同。

函数 `residential`：要计算住宅账单，你需要知道客户订阅的付费频道数量。根据付费频道数量，可以计算账单金额。计算账单金额后，函数使用 `return` 语句返回账单金额。以下四个步骤描述该函数：

- a. 提示用户输入付费频道数量。
- b. 读取付费频道数量。
- c. 计算应付金额。
- d. 返回应付金额。

该函数包含一条提示用户输入付费频道数量的语句（步骤 a）和一条读取付费频道数量的语句（步骤 b）。计算账单金额所需的其他项，例如基本服务连接费用和账单处理费，被定义为命名常量（在函数 main 的定义之前）。因此，为了计算账单金额，该函数不需要从函数 main 获取任何值。因此，该函数没有参数。

由前面的讨论可知，函数 `residential` 需要局部变量来存储付费频道数量和账单金额。该函数只需要这两个局部变量来计算账单金额：

```cpp
int noOfPChannels;   //number of premium channels
double bAmount;      //billing amount
```

现在可以将函数 residential 的定义写成如下形式：

```cpp
double residential()
{
    int noOfPChannels;   //number of premium channels
    double bAmount;      //billing amount

    cout << "Enter the number of premium "
         << "channels used: ";
    cin >> noOfPChannels;
    cout << endl;

    bAmount = RES_BILL_PROC_FEES +
              RES_BASIC_SERV_COST +
              noOfPChannels * RES_COST_PREM_CHANNEL;

    return bAmount;
}
```

函数 business：要计算商业账单，你需要知道客户订阅的基本服务连接数量和付费频道数量。然后，根据这些数量，可以计算账单金额。随后使用 `return` 语句返回账单金额。以下六个步骤描述该函数：

- a. 提示用户输入基本服务连接数量。
- b. 读取基本服务连接数量。
- c. 提示用户输入付费频道数量。
- d. 读取付费频道数量。
- e. 计算应付金额。
- f. 返回应付金额。

该函数包含提示用户输入基本服务连接数量和付费频道数量的语句（步骤 a 和 c）。该函数还包含输入基本服务连接数量和付费频道数量的语句（步骤 b 和 d）。计算账单金额所需的其他项，例如基本服务连接费用和账单处理费，被定义为命名常量（在函数 main 的定义之前）。因此，为了计算账单金额，该函数不需要从函数 main 获取任何值。因此，它没有参数。

由前述讨论可知，函数 business 需要变量来存储基本服务连接数量、付费频道数量以及账单金额。实际上，该函数只需要这三个局部变量来计算账单金额：

```cpp
int noOfBasicServiceConnections;
int noOfPChannels;   //number of premium channels
double bAmount;      //billing amount
```

现在可以将函数 `business` 的定义写成如下形式：

```cpp
double business()
{
    int noOfBasicServiceConnections;
    int noOfPChannels; //number of premium channels
    double bAmount;    //billing amount

    cout << "Enter the number of basic "
         << "service connections: ";
    cin >> noOfBasicServiceConnections;
    cout << endl;

    cout << "Enter the number of premium "
         << "channels used: ";
    cin >> noOfPChannels;
    cout << endl;

    if (noOfBasicServiceConnections <= 10)
        bAmount = BUS_BILL_PROC_FEES + BUS_BASIC_SERV_COST +
                  noOfPChannels * BUS_COST_PREM_CHANNEL;
    else
        bAmount = BUS_BILL_PROC_FEES + BUS_BASIC_SERV_COST +
                  (noOfBasicServiceConnections - 10) *
                  BUS_BASIC_CONN_COST +
                  noOfPChannels * BUS_COST_PREM_CHANNEL;

    return bAmount;
}
```

主程序的算法如下：

- 1. 要以带小数点和尾随零的固定小数格式输出浮点数，设置操纵符 fixed 和 showpoint。
- 2. 要将浮点数输出到两位小数，将精度设置为两位小数。
- 3. 提示用户输入账号。
- 4. 获取账号。
- 5. 提示用户输入客户类型。
- 6. 获取客户类型。
- 7.
    - a. 如果客户类型为 R 或 r，
        - i. 调用函数 `residential` 计算账单。
        - ii. 打印账单。
    - b. 如果客户类型为 B 或 b，
        - i. 调用函数 `business` 计算账单。
        - ii. 打印账单。
    - c. 如果客户类型不是 R、r、B 或 b，则为无效客户类型。

# 程序清单

```cpp
/************************************************************
// Author: D. S. Malik
//
// Program: Cable Company Billing
// This program calculates and prints a customer's bill for
// a local cable company. The program processes two types of
// customers: residential and business.
//************************************************************

#include <iostream>
#include <iomanip>
using namespace std;

                //Named constants - residential customers
const double RES_BILL_PROC_FEES = 4.50;
const double RES_BASIC_SERV_COST = 20.50;
const double RES_COST_PREM_CHANNEL = 7.50;

                //Named constants - business customers
const double BUS_BILL_PROC_FEES = 15.00;
const double BUS_BASIC_SERV_COST = 75.00;
const double BUS_BASIC_CONN_COST = 5.00;
const double BUS_COST_PREM_CHANNEL = 50.00;

double residential();   //Function prototype
double business();      //Function prototype

int main()
{
                //declare variables
    int accountNumber;
    char customerType;
    double amountDue;

    cout << fixed << showpoint;                         //Step 1
    cout << setprecision(2);                            //Step 2

    cout << "This program computes a cable bill."
         << endl;
    cout << "Enter account number: ";                   //Step 3
    cin >> accountNumber;                               //Step 4
    cout << endl;

    cout << "Enter customer type: R, r "
         << "(Residential), B, b (Business): ";         //Step 5
    cin >> customerType;                                //Step 6
    cout << endl;
```
