

*函数调用栈*（有时也称为*程序执行栈*）——在“幕后”工作——支持函数调用/返回机制。它还支持每个被调用函数的自动变量的创建、维护和销毁。正如我们在图 6.13–6.15 中看到的，这种后进先出行为正是函数在返回调用它的函数时所做的。

随着每个函数的被调用，它可能会依次调用其他函数，而这些函数又可能会依次调用其他函数——所有这些都在任何函数返回之前。每个函数最终必须将控制权返回给调用它的函数。因此，我们必须以某种方式跟踪每个函数需要返回给其调用者的返回地址。函数调用栈是处理此信息的完美数据结构。每次调用函数时，都会将一个条目压入栈中。该条目称为*栈帧*或*激活记录*，包含被调用函数需要返回给调用函数的返回地址。当被调用函数返回时，该函数调用的栈帧会被弹出，并且控制权转移到弹出的栈帧中的返回地址。

调用栈的美妙之处在于，每个被调用函数总能在调用栈顶部找到返回给其调用者所需的信息。而且，如果一个函数调用了另一个函数，只需简单地将新函数调用的栈帧压入调用栈。因此，新被调用函数返回给其调用者所需的返回地址现在位于栈顶。

栈帧还有另一个重要的职责。大多数函数都有自动变量——参数以及函数声明的任何局部变量。自动变量需要在函数执行期间存在。如果函数调用了其他函数，它们需要保持活动状态。但当被调用函数返回给其调用者时，被调用函数的自动变量需要“消失”。被调用函数的栈帧是存储函数自动变量的完美位置。只要被调用函数处于活动状态，该栈帧就存在。当该函数返回并且不再需要其局部自动变量时，其栈帧会从栈中弹出，并且那些局部自动变量对程序来说不再为人所知。

当然，计算机中的内存是有限的，因此只能使用一定量的内存来存储函数调用栈上的激活记录。如果发生的函数调用多于其激活记录能够存储在函数调用栈上的数量，就会发生称为*栈溢出*的错误。

## *函数调用栈的实际操作*

因此，正如我们所见，调用栈和激活记录支持函数调用/返回机制以及自动变量的创建和销毁。现在让我们考虑调用栈如何支持由 main 调用的 square 函数的操作（图 6.12 的第 11–17 行）。首先操作系统调用 main——这会将一个激活记录压入栈中（图 6.13 所示）。该激活记录告诉 main 如何返回到

```
1  // Fig. 6.12: fig06_12.cpp
2  // square function used to demonstrate the function
3  // call stack and activation records.
4  #include <iostream>
```

Fig. 6.12 | square function used to demonstrate the function call stack and activation records. (Part 1 of 2.)

```
using std::cin;
using std::cout;
using std::endl;

int square( int ); // prototype for function square

int main()
{
    int a = 10; // value to square (local automatic variable in main)
    cout << a << " squared: " << square( a ) << endl; // display a squared
    return 0; // indicate successful termination
} // end main

// returns the square of an integer
int square( int x ) // x is a local variable
{
    return x * x; // calculate square and return result
} // end function square
```

10 squared: 100

Fig. 6.12 | square function used to demonstrate the function call stack and activation records. (Part 2 of 2.)

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_237_0.png)

Fig. 6.13 | Function call stack after the operating system invokes main.

操作系统（即转移到返回地址 R1）并包含 main 的自动变量的空间（即 a，初始化为 10）。

函数 main——在返回操作系统之前——现在在图 6.12 的第 15 行调用函数 square。这会导致 square 的栈帧（第 20–23 行）被压入函数调用栈（图 6.14）。该栈帧包含 square 需要返回给 main 的返回地址（即 R2）以及 square 自动变量（即 x）的内存。

在 square 计算其参数的平方后，函数需要返回给 main——并且不再需要其自动变量 x 的内存。因此栈被弹出——给 square main 中的返回位置（即 R2）并丢失 square 的自动变量。图 6.15 显示了在 square 的激活记录被弹出后函数调用栈。

函数 main 现在显示调用 square 的结果（第 15 行），然后执行 return 语句（第 16 行）。这会导致 main 的激活记录从栈中弹出。这给 main 它需要返回到操作系统的地址（即图 6.13 中的 R1）并导致 main 的自动变量（即 a）的内存变得不可用。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_238_0.png)

Fig. 6.14 | Function call stack after main invokes function square to perform the calculation.

Fig. 6.15 | Function call stack after function square returns to main.

## 6.12 空参数列表的函数

在 C++ 中，空参数列表是通过在括号中写入 void 或什么都不写来指定的。原型

```
void print();
```

指定函数 print 不接受参数且不返回值。图 6.16 演示了声明和使用空参数列表函数的两种方法。

```
1  // Fig. 6.16: fig06_16.cpp
2  // Functions that take no arguments.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  void function1(); // function that takes no arguments
8  void function2( void ); // function that takes no arguments
```

Fig. 6.16 | Functions that take no arguments. (Part 1 of 2.)

```
9
10 int main()
11 {
12     function1(); // call function1 with no arguments
13     function2(); // call function2 with no arguments
14     return 0; // indicates successful termination
15 } // end main
16
17 // function1 uses an empty parameter list to specify that
18 // the function receives no arguments
19 void function1()
20 {
21     cout << "function1 takes no arguments" << endl;
22 } // end function1
23
24 // function2 uses a void parameter list to specify that
25 // the function receives no arguments
26 void function2( void )
27 {
28     cout << "function2 also takes no arguments" << endl;
29 } // end function2
```

```
function1 takes no arguments
function2 also takes no arguments
```

Fig. 6.16 | Functions that take no arguments. (Part 2 of 2.)

### Portability Tip 6.2

> C++ 中空函数参数列表的含义与 C 中截然不同。在 C 中，它意味着所有参数检查都被禁用（即函数调用可以传递任何参数）。在 C++ 中，它意味着函数明确不接受参数。因此，使用此功能的 C 程序在用 C++ 编译时可能会导致编译错误。

### Common Programming Error 6.13

> 除非为每个函数提供函数原型或每个函数在被调用前已定义，否则 C++ 程序不会编译。

## 6.13 内联函数

从软件工程的角度来看，将程序实现为一组函数是好的，但函数调用涉及执行时开销。C++ 提供了内联函数来帮助减少函数调用开销——尤其是对于小型函数。在函数定义中将限定符 inline 放在函数的返回类型之前，“建议”编译器在适当时在原地生成函数代码的副本以避免函数调用。权衡是程序中插入了函数的多个代码副本（通常使程序变大），而不是每次调用函数时都传递控制权到函数的单个副本。编译器可以忽略 inline 限定符，并且通常对除最小函数之外的所有函数都这样做。

