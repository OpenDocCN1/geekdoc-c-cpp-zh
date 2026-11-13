

### 输出

输入 a,b 的值：2 7
捕获异常：1
输入 a,b 的值：7 4
a,b 的差：3

在程序 1.28 中，a、b、c 是整型变量。如果 a>=b，则 c 的值为 0，否则为 1。如果 c=0，则显示 a,b 的差。否则，捕获异常。

## 多个 catch 语句
try 块可以关联多个 catch 块；在这种情况下，它也可能有多个 throw 语句。

```
try
{
    //try block
}
catch(argument)
{
    catch block 1
}
catch(arguments)
{
    catch block 2
}
.
.
.
.
.
.
.
catch(arguments)
{
    catch block n
}
```

当抛出异常时，编译器会查找与抛出的异常类型匹配的 catch 块，然后执行该 catch 块。如果未找到匹配项，程序将终止。

如果异常类型与多个 catch 块参数匹配，则将执行第一个匹配的 catch。

## 程序 1.29

```
#include<iostream.h>
#include<conio.h>
void sum(int s)
{
 try
 {
 if(s==0)throw k;
 else
 if(s>0)
 throw 'p';
 else if(s<0)throw 0.3;
 }
 catch(char c)
 {
 cout<<"caught a positive value";
 }
 catch(int i)
 {
 cout<<"caught a null value";
 }
 catch(float f)
 {
 cout<<"caught a negative value";
 }
}
void main()
{
 cout<<"multiple catches:";
 sum(-5);
 sum(0);
 sum(10);
}
```

### 输出

多个捕获：
捕获了一个负值
捕获了一个零值
捕获了一个正值

在程序 1.29 中，函数 sum() 包含一个 try 块和若干个 catch 块。第一个 catch 块接收 char 类型对象，第二个 catch 块接收整型参数，第三个 catch 语句接收 float 类型参数。函数 sum() 分别传入正值、负值和零值进行调用，参数 s 接收这些值。当 s 接收到正值时，throw 语句抛出 char 类型异常。当 s 接收到整数时，抛出整型异常；同样，当 s 为负数时，抛出 float 类型异常。当 catch 块中的参数类型与 throw 语句的参数匹配时，将执行相应的 catch 块。

可以使用单个 catch 块捕获由不同类型的多个 throw 语句抛出的异常。以下形式的 catch 语句可捕获所有异常：

```
catch(...) {
 catch block;
}
```

## 程序 1.30

```
#include<iostream.h>
#include<conio.h>
void sum()
{
 try
 {
 if(s==0)throw k;
 else
 if(s>0)throw 'p';
 else if(s<0)throw 0.0;
 }
 catch(...) // catch all exception
 {
 cout<<"caught all exception";
 }
}
void main()
{
 sum(-5);
 sum(0);
 sum(10);
}
```

### 输出

```
Caught all exceptions
Caught all exceptions
Caught all exceptions
```

在程序 1.30 中，所有异常都由单个 catch 块捕获。catch(...) 捕获所有异常并对其进行处理。也可以从 catch 块抛出异常。这称为重新抛出异常。

throw：throw 语句不接受任何参数。重新抛出异常时，它不会被同一个 catch 语句捕获，而是传递给下一个 catch 语句。

## 程序 1.31

```
#include<iostream.h>
#include<conio.h>
void sum(int i, int j)
{
 cout<<"in function sum()";
 try
 {
 if(i==0)
 throw i;
 else
 cout<<"subtraction of i&j:"<<i-j;
 }
 catch(int)
 {
 cout<<"caught null values";
 throw;
 }
 cout<<"End of sum()";
}
void main()
{
 cout<<"in main() function";
 try
 {
 sum(10,6);
 sum(0,5);
 }
 catch(int)
 {
 cout<<"caught null value inside main()";
 }
 cout<<"End of main()";
}
```

### 输出

```
In main() function
In function sum()
Subtraction of i&j:4
End of sum().
In function sum()
Caught null values
Caught null value inside main()
End of main()
```

在程序 1.31 中，当用零值调用函数 sum() 时，其内部的 catch 块捕获异常，与该 catch 块关联的 throw 语句重新抛出异常，并由同一个 catch 块捕获。main 函数内部的 catch 块处理重新抛出的异常。

## 摘要

- 类是成员变量和成员函数的集合。
- 对象是类的实例。它既保存数据，也保存操作数据的方法。
- 流是 I/O 设备的逻辑实体。流可以生成或消耗信息，并直接与 I/O 子系统相关联。类 ios 是 I/O 流的基类。
- 访问说明符为类成员从类外部访问提供访问权限。类的私有成员可以通过同一类的公有成员访问。声明为公有的成员变量和函数可以被类外部的成员访问。访问说明符 protected 的作用类似于关键字 private，在继承中非常有用。
- 作用域决定标识符的生存期和可见性。局部作用域、函数作用域、文件作用域、类作用域和原型作用域是不同类型的作用域。
- 类的所有对象共享静态成员的单一副本。每个静态变量必须初始化为零。
- 静态函数只能访问静态成员变量和函数，其作用域在类内是全局的。
- 内联函数在被访问时会复制函数定义。
- 友元函数允许访问类的私有成员。
- 函数重载定义多个同名但操作不同的函数。
- this 指针指向当前调用对象。
- new 运算符动态分配内存，delete 运算符在运行时释放内存。
- 异常是运行时错误。try、catch 和 throw 用于处理异常。
- 重新抛出异常是指从 catch 块抛出异常。

## 练习

### 填空

- 1. 对象是类的______。
- 2. 默认情况下，类的所有成员都是______。
- 3. 静态成员通过使用______来调用。
- 4. new 运算符与 malloc() 函数的区别是______。
- 5. 异常是______，发生在______。
- 6. 异常处理涉及______个关键字。

### 选择题

- 1. iostream 文件包含______。
  - a. 标准输入/输出库的声明
  - b. 程序输入和输出的流
  - c. (a) 和 (b) 都是。
  - d. 以上都不是

- 2. 以下哪项是正确的？
  - a. cout 表示标准输出流
  - b. cout 不是 iostream 的成员
  - c. cout 的默认控制台是键盘
  - d. 以上都不是

- 3. 静态成员可以使用_____运算符访问。
  - a. .(点)
  - b. -> (指针)
  - c. new
  - d. a 和 b 都是

- 4. 当成员变量声明为 static 时
  - a. 每个对象都会有一个单独的副本
  - b. 所有对象将共享成员变量的同一副本
  - c. 它们可以被对象访问
  - d. 以上都不是

- 5. 以下哪个关键字用于处理异常________。
  - a. try
  - b. throw
  - c. catch
  - d. 重新抛出

- 6. 在函数重载中，函数通过_______来区分。
  - a. 参数个数
  - b. 参数类型
  - c. 返回类型
  - d. a 和 b 都是

- 7. 静态函数直接通过使用_______来调用。
  - a. 对象
  - b. 成员函数
  - c. 类名
  - d. 作用域访问运算符 (::)

### 简答题

- 1. 定义类和对象。
- 2. 说明对象和变量的区别。
- 3. 说明访问说明符的用法。
- 4. 什么是作用域？定义各种类型的作用域。
- 5. 什么是静态成员和函数？
- 6. 说明重载函数的特性。
- 7. 定义友元类。
- 8. 讨论内联函数和友元函数。
- 9. 解释 this 指针。

### 论述题

- 1. 详细讨论 I/O 流。
- 2. 解释向方法传递参数的不同方式。
- 3. 详细说明动态内存分配。
- 4. 什么是异常？讨论处理异常的方式。
- 5. 用合适的例子解释函数重载的概念。

