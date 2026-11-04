
## 示例 5.16. 数组作为成员字段。

```
using System;

namespace Chapter5 {
    class DynamicVariables {
        private short[] array = new short[10];

        public DynamicVariables (int n) {
            array = new short[n];
        }

        public void SetElement(short i) {
            array[i] = i;
        }

        public short ReadElement(short i) {
            return(array[i]);
        }

        static void Main() {
            DynamicVariables instance = new DynamicVariables(10);
            for (short i = 0; i < instance.array.Length; i++) {
                instance.SetElement(i);
                Console.Write("{0} ", instance.ReadElement(i));
            }
            Console.WriteLine();
        }
    }
}
```

## 重载成员函数

*重载* 发生在两个或多个用户定义函数使用单一定义进行引用时。然而，为了避免冲突，定义必须至少在传递的一个参数上有所不同。逻辑上，如果两个函数相似到足以使用相同的名称，并且如果它们的 arguments 相同，那么应该努力将这些函数统一起来。这里我列出了两个示例，一个演示如何实现两个相似但重载的函数，另一个演示如何避免不必要的重载（参见示例 5.17 和 5.18）。

### 示例 5.17 合并两个相似的重载函数。

```
/* This function just saves the account. */
public void SaveFiles(BankAccount acc) {
    StreamWriter SaveFile = new StreamWriter(@"C:\MyFile.txt");
    SaveFile.WriteLine(acc.pin_number);
    SaveFile.WriteLine(acc.account_number);
    SaveFile.WriteLine((acc.Savings));
    SaveFile.WriteLine((acc.Checking));
    SaveFile.WriteLine(acc.first_name);
    SaveFile.WriteLine(acc.last_name);
    SaveFile.Close();
}

// This function alters our account balances and then saves those
// values to a designated file
public void SaveFiles(BankAccount acc, short input1, short input2) {
    StreamWriter SaveFile = new StreamWriter(@"C:\MyFile.txt");
    SaveFile.WriteLine(acc.pin_number);
    SaveFile.WriteLine(acc.account_number);
    SaveFile.WriteLine((acc.Savings + input1));
    SaveFile.WriteLine((acc.Checking + input2));
    SaveFile.WriteLine(acc.first_name);
    SaveFile.WriteLine(acc.last_name);
    SaveFile.Close();
}
```

### 示例 5.18. 避免重载。

```
public void SaveFiles(BankAccount acc, short input1, short input2) {
    StreamWriter SaveFile = new StreamWriter(@"C:\MyFile.txt");
    SaveFile.WriteLine(acc.pin_number);
    SaveFile.WriteLine(acc.account_number);
    SaveFile.WriteLine((acc.Savings + input1));
    SaveFile.WriteLine((acc.Checking + input2));
    SaveFile.WriteLine(acc.first_name);
    SaveFile.WriteLine(acc.last_name);
    SaveFile.Close();
}
```

正如你所见，示例 5.18 中的函数本可以拆分为包含两个重载函数，但通过使用零输入的简单调整，我们的两个函数合并为一个。

## *私有和受保护的成员函数*

私有和受保护的成员函数（也称为谓词或实用函数）是专门用于该类内部引用的成员函数。这些函数可用于读取或显示数据，通常用于支持该类公共成员函数的操作。私有/受保护成员函数并非 intended for use by outside references，但通常不带任何特定标记编写。要将我们之前的程序转换为使用私有成员函数的程序，我们只需修改类的内部定义即可（参见示例 5.19 和 5.20）。

### 示例 5.19. 私有成员函数（方法）。

```csharp
using System;
using System.IO;

namespace Chapter5 {
    class BankAccount {
        protected string first_name;
        protected string last_name;
        protected long account_number;
        protected decimal checking;
        protected decimal savings;
        protected short pin_number;

        private void ReadFile(ref BankAccount acc) {
            StreamReader file = new StreamReader(@"C:\MyFile.txt");
            acc.pin_number = short.Parse(file.ReadLine());
            acc.account_number = long.Parse(file.ReadLine());
            acc.savings = decimal.Parse(file.ReadLine());
            acc.checking = decimal.Parse(file.ReadLine());
            acc.first_name = file.ReadLine();
            acc.last_name = file.ReadLine();
            file.Close();
        }

        private void SaveFile(BankAccount acc, short input1,
            short input2) {
            StreamWriter file = new StreamWriter(@"C:\MyFile.txt");
            file.WriteLine(acc.pin_number);
            file.WriteLine(acc.account_number);
            file.WriteLine((acc.savings + input1));
            file.WriteLine((acc.checking + input2));
            file.WriteLine(acc.first_name);
            file.WriteLine(acc.last_name);
            file.Close();
        }

        public void CreateFile(ref BankAccount acc) {
            Console.WriteLine("Enter Your New Pin Number: ");
            acc.pin_number = short.Parse(Console.ReadLine());
            
            Random rnd = new Random();
            acc.account_number = rnd.Next(1, 100);
            
            Console.WriteLine("\nYour New Account Number is: {0}",
                acc.account_number);
            Console.WriteLine("\nEnter your first name: ");
            acc.first_name = Console.ReadLine();
            Console.WriteLine("\nEnter your last name: ");
            acc.last_name = Console.ReadLine();
            Console.WriteLine("\nEnter Your Savings Balance: ");
            acc.savings = decimal.Parse(Console.ReadLine());
            Console.WriteLine("\nEnter Your Checking Balance: ");
            acc.checking = decimal.Parse(Console.ReadLine());
            
            SaveFile(acc, 0, 0);
        }

        public void ViewFile(BankAccount acc) {
            Console.WriteLine("Pin Number: {0}", acc.pin_number);
            Console.WriteLine("Account Number: {0}", acc.account_number);
            Console.WriteLine("Name: {0} {1}", acc.first_name,
                acc.last_name);
            Console.WriteLine("Savings Balance: {0}", acc.savings);
            Console.WriteLine("Checking Balance: {0}", acc.checking);
        }

    }

    class Class1 {
        static void Main() {
            BankAccount account = new BankAccount();
            
            char input;
            while (true) {
                Console.WriteLine("Enter <C> to create new file or " +
                    "<V> to view account");
                input = char.Parse(Console.ReadLine());

                if(Char.ToUpper(input) == 'C') {
                    account.CreateFile(ref account);
                } else if (Char.ToUpper(input) == 'V') {
                    account.ViewFile(account);
                } else {
                    break;
                }
                account.ViewFile(account);
            }
        }
    }
}
```

### 示例 5.20. 受保护的成员函数（方法）。

```csharp
protected void ReadFiles(ref BankAccount acc) {
    StreamReader ReadFile = new StreamReader(@"C:\MyFile.txt");
    acc.pin_number = short.Parse(ReadFile.ReadLine());
    acc.account_number = long.Parse(ReadFile.ReadLine());
    acc.Savings = decimal.Parse(ReadFile.ReadLine());
    acc.Checking = decimal.Parse(ReadFile.ReadLine());
    acc.first_name = ReadFile.ReadLine();
    acc.last_name = ReadFile.ReadLine();
    ReadFile.Close();
}

protected void SaveFiles(BankAccount acc, short input1, short input2) {
    StreamWriter SaveFile = new StreamWriter(@"C:\MyFile.txt");
    SaveFile.WriteLine(acc.pin_number);
    SaveFile.WriteLine(acc.account_number);
    SaveFile.WriteLine((acc.Savings + input1));
    SaveFile.WriteLine((acc.Checking + input2));
    SaveFile.WriteLine(acc.first_name);
    SaveFile.WriteLine(acc.last_name);
    SaveFile.Close();
}
```

## 构造函数

构造函数是成员函数，会随着该类实例的声明而自动实现。每个新实例都会触发此执行，并且通常，
这些值会针对该实例的引用而具体化。构造函数与标准成员函数类似，是在这些类内部声明的，但构造函数不需要基本数据类型。构造函数使用与其声明类相同的定义进行定义，而其实际功能则表示为定义组合和连接的二进制作用域解析运算符的组合。由于构造函数不声明数据类型，因此它们也无法返回值（参见示例 5.21）。

> 每个声明的实例都会分配系统内存的一部分（通常称为堆）。在原生 C++ 中，定义该内存的恢复也很重要（通常由该类的析构函数引用——请参阅本章关于析构函数的部分）。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_365_0.png)

### 示例 5.21. 构造函数。

```csharp
using System;
using System.IO;

namespace Chapter5 {
    class BankAccount {
        public decimal InterestRate;
        public decimal LoanRate;

        // Default Constructor
        public BankAccount() {
            InterestRate = .03M; LoanRate = .13M;
        }
    }

    class Class1 {
        static void Main() {
            BankAccount account = new BankAccount();
        }
    }
}
```

1 虽然析构函数是原生 C++ 的重要组成部分，但在 C# 中其重要性已降低，其中对象析构的过程已成为编译器的主要关注点，通常在对象不再被引用时发生。
