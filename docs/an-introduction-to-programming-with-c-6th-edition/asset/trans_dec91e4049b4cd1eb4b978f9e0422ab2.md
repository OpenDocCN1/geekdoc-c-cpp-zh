

```cpp
cout << "信用合作社利率: ";
cin >> creditRate;
cout << "经销商利率: ";
cin >> dealerRate;
cout << "贷款期限（年）: ";
cin >> term;

// 如果必要，将比率转换为小数格式
if (creditRate >= 1.0)
  creditRate /= 100;
//end if
if (dealerRate >= 1.0)
  dealerRate /= 100;
//end if

// 调用函数计算还款
creditPayment = getPayment(carPrice - rebate,
  creditRate / 12, term * 12);
dealerPayment = getPayment(carPrice,
  dealerRate / 12, term * 12);

//显示金额
cout << setprecision(2) << endl;
cout << "信用合作社还款: ";
cout << creditPayment << endl;

cout << "经销商还款: ";
cout << dealerPayment << endl;

if (creditPayment < dealerPayment)
  cout << "接受返现并通过信用合作社进行融资。" << endl;
else
  if (creditPayment > dealerPayment)
    cout << "不要接受返现。通过经销商融资。" << endl;
  else
    cout << "你可以通过其中任何一种进行融资。"
 << endl;
//end if

cout << endl << "要再次计算吗？(Y/N): ";
cin >> again;
cout << endl;
} while (toupper(again) == 'Y');
system("pause");
return 0;
} // main函数结束
//*****函数定义****
double getPayment(int prin,
  double monthRate,
  int months)
```

# 附录 A 迷你测验和实验答案

```cpp
{
// 计算并返回每月还款额
double monthPay = 0.0;
monthPay = prin * monthRate /
  (1 - pow(monthRate + 1, -months));
return monthPay;
} // getPayment函数结束
```

#  9-4 桌面检查 (Desk-Check)

桌面检查：

| 余额 | 金额 | 交易 | 另一个 |
| --- | --- | --- | --- |
| 2000.0 | 400.0 | W | ✗ |
| 1000.0 | 1000.0 | W | D |
| 2500.0 | 45.0 | D | D |
| 2755.0 | 55.0 | D | D |
| 2700.0 | 150.0 | W | D |
| 2550.0 | 15.0 | D | D |
| 2565.0 | 1050.0 | W | n |
| 1515.0 | | | |

| 余额 | 类型 | 金额 | 当前余额 |
| --- | --- | --- | --- |
| 2000.0 | W | 400.0 | 1600.0 |
| 1600.0 | D | 1200.0 | 2800.0 |
| 2500.0 | W | 45.0 | 2755.0 |
| 2755.0 | W | 55.0 | 2700.0 |
| 2700.0 | W | 150.0 | 2550.0 |
| 2550.0 | D | 15.0 | 2565.0 |
| 2565.0 | W | 1050.0 | 1515.0 |

代码将显示当前余额为 $1515.00。

# 第 10 章迷你测验答案

# 实验 9-5 调试 (Debug)

要调试程序，请将调用 `getDeprecation` 函数的语句更改 `deprecation = getDeprecation(cost, salvage, lifeYears);`。

# 第 10 章迷你测验答案

# 迷你测验 10-1

- 1. void
2. displayTaxes(federalTax, localTax);
3. void displayTaxes(double fedTax, double stateTax);
4. 错误

# 迷你测验 10-2

- 1. void getInput(double &hours, double &rate)
2. getIn(hoursWkd, payRate);
3. void getInput(double &hours, double &rate); 或 void getInput(double, double &);
4. 正确

# 迷你测验 10-3

- 1. void calcTaxes(double pay, double &fedTax, &stateTax)
2. calcTaxes(gross, federal, state);
3. void calcTaxes(double pay, double &fedTax, &stateTax); 或 void calcTaxes(double, double, double &);
4. 错误

# 第 10 章实验答案

# 实验 10-1 停止并分析

- 1. 第 11 至 13 行的函数原型和第 77 至 79 行的函数头。

- 2. `americanDols` 和 `conversionRate` 变量是通过值传递的，因为 `convertDols` 函数需要它们的值，但不需要修改它们。`convertedCurrency` 是按引用传递的，因为 `convertDols` 函数需要在变量内部存储一个值（转换后的美元）。

- 3. `displayMenu` 函数是一个 `void` 函数，因为它在完成任务后没有返回任何值。

- 4. 第 35 行包含引导读取 (priming read)。第 61 行包含更新读取 (update read)。

- 5. 你需要在此修改函数：

```cpp
double convertDols(double dollars, double convertRate)
{
    double converted = 0.0;
    converted = dollars * convertRate;
    return converted;
// convertDols函数结束
```
你还需要将第 11 至 13 行的函数原型更改为 `convertDols(double dollars, double convertRate);` 并更改调用处。

- 6. 不需要。
- 7. 15。
- 8. 55。
- 9. 

（注：后续部分文本存在大量重复且重复，已根据翻译逻辑完成核心内容。）

