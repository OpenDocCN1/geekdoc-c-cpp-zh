
这里是程序执行的结果：

## 程序的输出（在列表 8.11 中）

Three -> 3

Ten -> 10

在程序中，我们创建了枚举 `Number`，其值被常量 `one`（值为 1）、`two`（值为 2）、`three`（值为 3）、`five`（值为 5）、`ten`（值为 10）限制。我们还创建了 `Number` 类型变量 `num` 并给变量赋值（语句 `num=Number::three` 和 `num=Number::ten`）。当我们打印变量 `num` 的值时，我们使用了显式转换（指令 `(int) num`，因为在这种情况下不涉及隐式转换）。

## 异常处理

我们已经使用过异常处理。现在，我们将考虑该机制的其他方面。

让我们考虑列表 8.12 中的程序。在那里我们创建了一个数组（基于 `vector` 类）并用斐波那契数填充它。数组的大小由用户输入。用户可能会输入错误的数组大小（一个负数）。

# 第 8 章 不同的程序

## 列表 8.12. 异常处理

```cpp
#include <iostream>
#include <vector>
using namespace std;
int main(){
    // 存储数组大小的变量：
    int n;
    cout<<"The Fibonacci numbers\n";
    cout<<"Enter the size of the array: ";
    cin>>n;
    try{
        // 创建数组：
        vector<int> fibs(n,1);
        // 打印前两个元素：
        cout<<fibs[0]<<" "<<fibs[1];
        // 填充数组并打印元素：
        for(int k=2;k<n; k++) {
            fibs[k]=fibs[k-1]+fibs[k-2];
            cout<<" "<<fibs[k];
        }
    }
    // 捕获异常：
    catch(...){
        cout<<"An error has occurred.";
    }
    cout<<"\nThe program is terminated\n";
    return 0;
}
```

程序的输出可能是（如果用户输入正确的数组大小）：

程序的输出（在列表 8.12 中）

The Fibonacci numbers

Enter the size of the array: 10

1 1 2 3 5 8 13 21 34 55

The program is terminated

也可能是（如果用户输入负数）：

程序的输出（在列表 8.12 中）

The Fibonacci numbers

Enter the size of the array: -3

An error has occurred.

The program is terminated

在程序中，我们使用容器类 `vector` 创建数组

## 使用多线程

在下一个程序中，我们运行多个线程。

> 理论：线程是程序的不同部分，它们同时执行。通用方案如下。在主线程（与 `main()` 函数标识）中，我们可以运行子线程。要在子线程中执行的代码实现为一个函数。我们在主线程中以特殊模式调用该函数。为了实现多线程方法，必须包含 `<thread>` 头文件。为了运行子线程，我们在主线程中创建一个 `thread` 对象。为了连接线程和函数，我们将函数名称传递给构造函数。

所有这些线程都会同时打印消息。现在让我们考虑这个程序。

## 列表 8.13. 使用多线程

```cpp
#include <iostream>
#include <string>
#include <thread>
#include <chrono>
#include <mutex>
using namespace std;
mutex m;
// 创建线程的函数：
void mythread(string name, int time, int steps) {
    for(int k=1; k<=steps; k++) {
        // 语句执行期间的时间延迟：
        this_thread::sleep_for(chrono::seconds(time));
        // 锁定资源（控制台）：
        m.lock();
        // 在控制台打印消息：
        cout << "The thread " << name << ": message " << k << endl;
        // 解锁资源（控制台）；
        m.unlock();
    }
}

// 程序的主函数：
int main() {
    // 线程中的循环次数：
    int n=5;
    cout << "Running the threads...\n";
    // 第一个子线程：
    thread A(mythread, "Alpha", 4, n);
```

# 第 8 章

```cpp
// 第二个子线程：
thread B(mythread, "Bravo", 3, n);
// 在主线程中调用函数：
mythread("Main", 2, n);
// 等待第一个线程终止：
if(A.joinable()) {
  A.join();
}
// 等待第二个线程终止：
if(B.joinable()) {
  B.join();
}
cout << "The program is terminated\n";
return 0;
```

程序的可能输出在此处：

> 程序的输出（见列表 8.13）

```
Running the threads...
The thread Main:    message 1
The thread Bravo:   message 1
The thread Alpha:  message 1
The thread Main:    message 2
The thread Bravo:   message 2
The thread Main:    message 3
The thread Alpha:  message 2
The thread Main:    message 4
The thread Bravo:   message 3
The thread Main:    message 5
The thread Alpha:  message 3
The thread Bravo:   message 4
```

| The thread Bravo: message 5 |

| The thread Alpha: message 4 |

| The thread Alpha: message 5 |

| The program is terminated |

接下来，我们将分析这个程序并解释它的一些关键部分。首先，让我们考虑程序的总体结构。

除了 `main()` 函数外，我们描述了带有三个参数的 `mythread()` 函数。我们在 `main` 函数中调用了三次 `mythread()`。也就是说，我们在两个子线程中运行该函数，并在主线程中运行它。

当我们调用函数 `mythread()` 时，它会执行一个循环语句。在每次迭代中，函数都会在屏幕上打印一条消息。消息包含了 `mythread()` 函数的第一个字符串参数和消息编号。函数的第三个参数决定了打印消息的总数。函数在消息之间产生时间延迟。`mythread()` 的第二个参数提供了延迟的时间间隔（以秒为单位）。这就是该函数的功能。稍后我们将研究它的代码。现在我们要分析主函数 `main()`。

在 `main` 函数中，我们使用了值为 5 的变量 `n`。它决定了每个线程在屏幕上打印的消息数量。语句 `thread A(mythread, "Alpha", 4, n)` 运行第一个子线程。也就是说，它创建了 `thread` 类的对象 `A`。我们可以将此对象识别为第一个子线程，并通过对象 `A` 来操作线程。我们在创建对象 `A` 时传递给构造函数的参数意味着该子线程将带有参数 "Alpha"、4 和 `n` 运行函数 `mythread()`。因此，该线程将打印 `n` 条带有字符串 "Alpha" 的消息，且消息之间的时间延迟为 4 秒。

在创建第一个子线程后，语句 `thread B(mythread, "Bravo", 3, n)` 运行另一个子线程。我们可以通过对象 `B` 访问该线程。该线程带有参数 "Bravo"、3 和 `n` 运行函数 `mythread()`。这意味着该线程将打印 `n` 条带有字符串 "Bravo" 的消息，且消息之间时间延迟为 3 秒。在主线程中，语句 `mythread("Main", 2, n)` 运行函数 `mythread()`。因此，主线程将打印 `n` 条带有字符串 "Main" 的消息，且消息之间的时间延迟为 2 秒。结果是，随着主线程执行，有两个子线程正在执行。换句话说，我们有三个并行线程，它们执行所需的时间不同。我们希望主线程等待子线程终止。为了实现这一点，我们使用了语句 `A.join()` 和 `B.join()`。这意味着在执行下一条语句之前，必须等待第一个和第二个线程终止。在调用线程对象的 `join()` 方法之前，我们必须检查该线程是否仍在运行。为了进行此测试，我们使用线程对象调用的 `joinable()` 方法。子线程终止后，语句 `cout << "The program is terminated\n"` 在主线程中打印一条消息。

现在让我们分析 `mythread()` 函数的代码。它简单且短小，但包含一些新语句和未知的语法结构。特别是，我们在那里使用了语句 `this_thread::sleep_for(chrono::seconds(time))`。它会根据函数参数 `time` 定义的时间（秒为单位）阻塞其他语句的执行。为了使用此语句，我们在程序中包含了 `<chrono>` 头文件。

在语句中，为了产生时间延迟，我们调用了在 `this_thread` 命名空间中描述的 `sleep_for()` 函数。我们通过作用域解析运算符 `::` 将命名空间放在函数之前。

`seconds()` 函数返回一个确定延迟间隔的对象。将其传递给 `sleep_for()` 函数。`seconds()` 函数来自 `chrono` 命名空间。`chrono` 命名空间在包含 `<chrono>` 头文件后即可访问。

```cpp
// 使用不动点迭代法求解方程的
// 函数：
double findRoot(double (*f)(double), double x0, int n) {
    // 方程根的初始近似值：
    double x=x0;
    // 进行迭代：
    for(int k=1; k<=n; k++) {
        x=f(x);
    }
    // 函数的返回值：
    return x;
}

// 这些函数决定了方程：
double f(double x) {
    return 0.5*cos(x);
}
double g(double x) {
    return exp(-x);
}
double h(double x) {
    return (x*x+6)/5;
}
// 用于求解方程
// 并测试根的函数：
void test(double (*f)(double), double x0, string eq) {
    // 迭代次数：
    int n=100;
    // 用于保存方程根的变量：
    double z;
    cout << "The root of the equation " << eq << ":\t";
    // 找到方程的根：
    z=findRoot(f,x0,n);
    // 输出结果：
    cout<<z<<endl;
    cout<<"Testing the root:\t"; // 测试根：
    cout<<z << " = " << f(z)<<endl;
    for (int k=1; k<=50; k++) {
        cout<<"-";
    }
    cout<<endl;
}

// 程序的主函数：
int main() {
    // 求解方程：
    test(f,0,"x=0.5cos(x)");
    test(g,0,"x=exp(-x)");
    test(h,1,"x=(x*x+6)/5");
    return 0;
}
```

# 第9章 数学问题

这里是程序的输出：

程序的输出（见列表 9.1）

方程 x=0.5cos(x) 的根: 0.450184

测试根: 0.450184 = 0.450184

方程 x=exp(-x) 的根: 0.567143

测试根: 0.567143 = 0.567143

方程 x=(x*x+6)/5 的根: 2

测试根: 2 = 2

为了求解方程，我们在程序中描述了 `findRoot()` 函数。该函数的第一个参数是一个指向确定要解方程的函数指针。该函数必须有一个类型为 `double` 的参数，并且必须返回 `double` 类型。`findRoot()` 函数的第二个参数决定了方程根的初始近似值。第三个参数定义了计算根时执行的迭代次数。

我们在程序中解了三个方程。这些方程由函数 `f()`、`g()` 和 `h()` 。我们将这些函数名作为第一个参数传递给函数 `findRoot()`。`findRoot()` 函数本身在 `test()` 函数中被调用。

找到方程的根后，我们会测试它的正确性。为此，我们打印计算出的根 `x`，然后打印在根点确定方程的函数值 `q(x)`。理想情况下，这些值应该是相等的。

> 注意：

> 这里我们不考虑可以使用不动点迭代法求解方程的条件。

## 二分法

二分法用于求解形式为 $f(x) = 0$ 的代数方程。如果已知根局限于某个区间 $a \le x \le b$ 内，且函数 $f(x)$ 在区间边界处的符号不同（这意味着 $f(a)f(b) < 0$），我们就可以应用该方法。

算法如下：我们在区间的中心点 $x = (a+b)/2$ 处计算函数 $f(x)$。然后找到函数值与中心点符号边界。将边界移动到区间的中心。结果是搜索根的区间缩短了一倍，且函数 $f(x)$ 在新区间边界处的符号不同。因此，我们的情况与最初几乎相同，但根的定位区间缩短了一倍。

列表 9.2 包含了通过二分法求解方程的程序。

## 列表 9.2. 二分法

```cpp
#include <iostream>
#include <cmath>
#include <string>
using namespace std;
// 使用二分法
// 求解方程的函数：
double findRoot(double (*f)(double),double a,
double b, double dx) {
    // 用于保存根的变量：
    double x=(a+b)/2;
    // 计算根：
    while((b-a)/2>dx) {
        // 如果根在左边界：
        if (f(a)==0) {
            return a;
        }
        // 如果根在右边界：
        if (f(b)==0) {
            return b;
        }
        // 如果：
        if (f(a)*f(x)<0) {
            // 将边界移动到区间的中心：
            a=x;
        } else {
            b=x;
        }
        // 计算新的点：
        x=(a+b)/2;
    }
// 决定方程的函数：
double f(double x) {
  return 0.5*cos(x);
}
double g(double x) {
  return exp(-x);
}
double h(double x) {
  return (x*x+6)/5;
}
// 求解方程
// 并测试根的函数：
void test(double (*f)(double), double x0, string eq) {
  // 捕获异常：
  try {
    // 用于保存根的变量：
    double z;
    cout << "The root of the equation " << eq << ":\t";
    // 找到方程的根：
    z=findRoot(f,x0,n); 
    // 输出结果：
    cout<<z<<endl;
    cout<<"Testing the root:\t"; // 测试根：
    cout<<z << " = " << f(z)<<endl;
  } catch (const char* e) {
    // 输出错误：
    cout<<e<<endl;
  }
}

// 程序的主函数：
int main() {
    // 求解方程：
    test(f,0,"x=0.5cos(x)");
    test(g,0,"x=exp(-x)");
    test(h,1,"x=(x*x+6)/5");
    return 0;
}
```

*(注：由于原文代码中 `findfindRoot` 处存在 `n` 未定义及部分逻辑截断，此处翻译时保持了逻辑结构，仅对注释进行翻译)*

*(纠正：用户提供的原文文本中代码块存在不完整的情况（如 `test` 函数中 `n` 未定义），但作为翻译，我应严格遵循原文代码结构，仅翻译注释。)*
