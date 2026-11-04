
对成员的访问也在这些结构内部受到限制。一旦结构被列出，正确的声明和赋值包括声明结构的实例以及对该字段的赋值（参见示例 5.2 和 5.3。）

### 示例 5.2. 声明和赋值结构。

```
using System;

namespace Chapter5 {
    struct BankAccount {
        public string first_name;
        public string last_name;
        public long account_number;
        public decimal checking;
        public decimal savings;
        public short pin_number;

        public static void Main() {
            BankAccount account;
            Console.Write("Enter your pin number here (2001): ");
            account.pin_number = short.Parse(Console.ReadLine());

            if (account.pin_number == 2001) {
                account.account_number = 43297;
                account.first_name = "John";
                account.last_name = "Doe";
                account.checking = 0;
                account.savings = 112.53M;
                Console.WriteLine("Account Number: {0}",
                    account.account_number);
                Console.WriteLine("Identity: {0} {1}",
                    account.first_name, account.last_name);
                Console.WriteLine("Savings Account Balance: {0}",
                    account.savings);
                Console.WriteLine("Checking Account Balance: {0}",
                    account.checking);
            }
        }
    }
}
```

### 屏幕截图 5.1.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_336_0.png)

在插入点运算符时，使用可视化编译器的用户可能会遇到类似于屏幕截图 5.1 的弹出窗口。该窗口通常用作提醒，提示程序员某些字段可用。如果某项不存在，这可能表明它被错误编码，或者某个引用缺失或不完整。挂锁符号表示受保护或私有的成员/字段。

### 示例 5.3. 声明和赋值多个实例。

```
using System;

namespace Chapter5 {
    struct BankAccount {
        public string first_name;
        public string last_name;
        public long account_number;
        public decimal checking;
        public decimal savings;
        public short pin_number;
    }

    class Class1 {
        static void Main () {
            BankAccount account1, account2;

            account1.pin_number = 2001;
            account1.account_number = 43297;
            account1.first_name = "John";
            account1.last_name = "Doe";
            account1.savings = 0;
            account1.checking = 112.53M;
        }
    }
}
```

```
account2.pin_number = 2002;
account2.account_number = 78978;
account2.first_name = "Jane";
account2.last_name = "Happy";
account2.savings = 312.43M;
account2.checking = 2134.65M;

Console.Write("\nEnter your pin number here: ");
short input = short.Parse(Console.ReadLine());

if (input == account1.pin_number) {
    Console.WriteLine("Account Number: {0}",
        account1.account_number);
    Console.WriteLine("Identity: {0} {1}",
        account1.first_name, account1.last_name);
    Console.WriteLine("Savings Account Balance: {0}",
        account1.savings);
    Console.WriteLine("Checking Account Balance: {0}",
        account1.checking);
} else if (input == account2.pin_number) {
    Console.WriteLine("Account Number: {0}",
        account2.account_number);
    Console.WriteLine("Identity: {0} {1}",
        account2.first_name,
        account2.last_name);
    Console.WriteLine("Savings Account Balance: {0}",
        account2.savings);
    Console.WriteLine("Checking Account Balance: {0}",
        account2.checking);
}
}
}
```

## 多个结构

处理结构时另一个有用的技术是使用结构数组。当处理大量实例且这些实例共享一组共同的比较时，这很快就会成为必需。请注意结构名称如何被用作基本数据类型的位置，以及其格式如何模仿基本数组样式引用的格式。该数组也受大小限制，但它也固有地具有多维数组的一些功能（参见示例 5.4）。虽然允许结构数组，但内部结构数组不允许。这是因为结构按定义是基于值的，而数组依赖于基于引用的结构（在 C# 中定义为类）。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_338_0.png)

> 关键字 new 同时用作运算符和修饰符。作为运算符，它用于声明实例和创建对象。作为修饰符，它用于隐藏从基类继承的成员。new 运算符不能被重载或与 override 语句一起使用。

### 示例 5.4. 结构数组。

```
using System;

namespace Chapter5 {
    struct BankAccount {
        public string first_name;
        public string last_name;
        public long account_number;
        public decimal checking;
        public decimal savings;
        public short pin_number;
    }

    class Class1 {
        public static void Main() {
            BankAccount[] account = new BankAccount[3];

            account[0].pin_number = 2000;
            account[0].account_number = 78434;
            account[0].first_name = "Bad";
            account[0].last_name = "Dog";
            account[0].savings = 1000.15M;
            account[0].checking = 43.12M;
            account[1].pin_number = 2001;
            account[1].account_number = 43297;
            account[1].first_name = "John";
            account[1].last_name = "Doe";
            account[1].savings = 0;
```

```csharp
account[1].checking = 112.53M;
account[2].pin_number = 2002;
account[2].account_number = 78978;
account[2].first_name = "Jane";
account[2].last_name = "Happy";
account[2].savings = 2134.65M;
account[2].checking = 312.43M;

while (true) {
    Console.Write("Enter your pin number here: ");
    short input = short.Parse(Console.ReadLine());
    for (int index = 0; index < 3; index++) {
        if (input == account[index].pin_number) {
            Console.WriteLine("Account Number: {0}",
                account[index].account_number);
            Console.WriteLine("Identity: {0} {1}",
                account[index].first_name,
                account[index].last_name);
            Console.WriteLine("Savings Account Balance: {0}",
                account[index].savings);
            Console.WriteLine("Checking Account Balance: {0}",
                account[index].checking);
        }
    }
}
```

## 复杂结构

*复杂结构* 只是包含对其他结构引用的结构。这些次级结构与标准结构以基本相同的方式访问，只是增加了第二个点运算符和额外的成员名称。将一个结构包含在另一个结构中也称为 *组合和/或嵌套*。请注意，与 C++ 不同，对外层结构的引用不会固有地引用内部值，因此；这两个结构必须分别声明（参见示例 5.5）。

### 示例 5.5. 嵌套结构。

```csharp
using System;

namespace Chapter5 {
    struct BankAccount {
        public string first_name;

        public struct NestedStruct {
            public decimal swiss_account;
        }
    }

    class Class1 {
        static void Main() {
            BankAccount Account;
            BankAccount.NestedStruct HiddenAccount;

            Account.first_name = "MR.RICH";
            HiddenAccount.swiss_account = 5000000.00M;
        }
    }
}
```

## 结构作为函数参数：按值调用

除了能够将标准变量作为按值调用和按引用调用的值传递外，我们还可以使用这两种技术中的任何一种传递字段。在本节中，我们将应用其中更简单的一种，即按值调用过程，我们已经定义了这些值的自包含性质。请记住，按值调用用于传递数据，该数据可在引用方法内部进行更改，但最终不会影响源值（参见示例 5.6）。

### 示例 5.6. 使用结构的按值调用。

```csharp
using System;

namespace Chapter5 {
    class Class1 {
        struct BankAccount {
            public string first_name;
```
