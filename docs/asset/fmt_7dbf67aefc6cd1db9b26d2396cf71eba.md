
`cout`<<`The second variable: `<<`y`<<`endl`;

`swap`(&`x`, &`y`);

`cout`<<`The first variable: `<<`x`<<`endl`;

`cout`<<`The second variable: `<<`y`<<`endl`;

`return` 0;

}

```

程序的输出如下：

| 程序的输出（如 4.7 所示） |
| :--- |
| The first variable: A |
| The second variable: B |
| The swap() function is called |
| The first argument: A |
| The second argument: B |
| ---------------------- |
| The first argument: B |
| The second argument: A |
| The swap() function is terminated |
| The first variable: B |
| The second variable: A |

## 将数组传递给函数

经常，需要将数组传递给函数。列表 4.8 中的程序说明了如何这样做。

一维数组通过两个参数传递给函数。它们是指向数组第一个元素的指针（数组名）以及确定数组元素数量的整数。

在下文程序中，我们创建了一个只有一个参数的 `mean` 函数，该参数是一个数值数组。函数返回数组元素的平均值。在程序的主函数中，我们调用 `mean` 函数计算两个数组的平均值。

> 列表 4.8. 将一维数组传递给函数

```cpp
#include <iostream>
using namespace std;
// 接收数组的函数；
double mean(double* m,int n) {
    // 用于存储和的局部变量：
    double s=0;
    for(int k=0;k<n;k++) {
        s+=m[k];
    }
    // 函数的返回值：
    return s/n;
}
```

```cpp
// 程序的主函数:
int main() {
    // 第一个数组:
    double A[]={1,3,8,-2,4};
    // 第二个数组:
    double B[]={4,6,2};
    // 调用函数:
    cout<<"数组 A 的平均值: " <<
    mean(A,5)<<endl;
    cout<<"数组 B 的平均值: " <<
    mean(B,3)<<endl;
    return 0;
}
```

程序的程序的输出如下：

| 程序的输出（在列表 4.8 中） |
| :--- |
| 数组 A 的平均值: 2.8 |
| 数组 B 的平均值: 4 |

我们描述了带有两个参数的 `mean()` 函数。类型为 `double*` 的第一个参数 `m` 是指向 `double` 类型值的指针。考虑到数组名是指向该数组第一个元素的指针，我们可以将参数 `m` 等同于数组名。这就是我们在函数中处理变量 `m` 的方式。函数的第二个整数参数 `n` 决定了数组的大小。

在函数内部，我们计算了数组元素的和，并将值存储在局部变量 `s` 中。`s/n`（元素之和除以元素个数得到平均值）是函数的返回值。

# 第 4 章 函数

在程序的主函数中，我们创建并初始化了两个数值数组。为了实现这一点，我们使用了语句 `double A[]={1,3,8,-2,4}` 和 `double B[]={4,6,2}`。

## 注意事项

在创建数组的语句中，我们没有指定数组的大小。每个数组的大小是根据初始化列表中的元素数量自动确定的。

我们将数组名及其大小传递给 `mean()` 函数：例如 `mean(A,5)` 或 `mean(B,3)`。

二维数组也可以以类似的方式传递给函数。列表 4.9 包含了我们描述 `show()` 函数的程序。该函数获取一个二维数组并在屏幕上打印数组的元素。

## 理论

静态二维数组的处理方式与一维数组相似（假设它是一个外部数组），其元素是一个一维数组（假设它们是内部数组）。外部数组的类型标识符必须包含内部数组的大小。因此，仅指定外部数组由内部数组组成是不够的。必须指定内部数组的大小。当我们把二维数组传递给函数时，传递了两个特征。这些特征是：二维数组名（带有第二个索引的大小，必须显式指定）以及一个决定第一个索引二维数组大小的整数（外部数组的大小）。

现在，让我们来看这个程序。

## 列表 4.9. 将二维数组传递给函数

```cpp
#include <iostream>
using namespace std;
// 第二个索引的数组大小;
const int n=3;
```

```cpp
// 接收二维数组
// 传递的函数:
void show(int M[][n], int p, int q) {
    for (int i=0;i<p;i++) {
        for (int j=0;j<n;j++) {
            cout<<M[i][j]<<" ";
        }
        cout<<endl;
    }
}
// 程序的主函数:
int main() {
    // 第一个数组:
    int A[2][n]={{1,2,3},{4,5,6}};
    // 第二个数组:
    int B[][n]=
    {{11,12,13},{14,15,16},{17,18,19},{20,21,22}};
    cout<<"第一个数组:\n";
    show(A,2);
    cout<<"第二个数组:\n";
    show(B,4);
    return 0;
}
```

程序的输出如下所示：

程序的输出（在列表 4.9 中）

```
第一个数组:
1 2 3
4 5 6
第二个数组:
11 12 13
14 15 16
17 18 19
20 21 22
```

为了确定二维数组第二个索引的大小，我们创建了一个全局常量 `n`。函数的第一个参数由表达式 `M[][n]` 描述，其中第二个索引的大小是显式指定的。因此，`show()` 函数适用于打印第二个索引大小为 `n` 的数组。在程序的主函数中，我们使用 `show()` 函数打印数组 `A` 和 `B`，这些数组是通过语句 `A[2][n]={{1,2,3},{4,5,6}}` 和 `B[][n]={{11,12,13},{14,15,16},{17,18,19},{20,21,22}}` 创建并初始化的。这些数组的第二个索引均为 `n`，但它们的第一个索引大小是不同的。此外，数组 `A` 的第一个索引大小是显式指定的，而数组 `B` 的大小（括号为空）是自动确定的。当我们调用 `show()` 时，数组名作为第一个参数传递，第二个参数是第一个索引的大小。

当我们想要将二维数组传递给函数时，一切都略有不同。

## 理论

二维数组是指针的一维数组。数组中的每个指针都包含另一个一维数组的第一个元素的地址。因此，将二维数组传递给函数与传递一维数组相同（这意味着传递两个参数：数组第一个元素的指针和数组的大小），再加上一个参数，该参数决定了内部数组的大小。在很多情况下，只传递三个参数就足够：一个指针和两个整数。

列表 4.10 包含了我们创建 `show()` 函数的程序。该函数打印二维数组的内容。为了实现数值的格式化输出，我们使用了 `printf()` 函数。这就是为什么我们在程序中包含了 `<cstdio>` 头文件而没有包含 `<iostream>` 头文件。

与上一个示例（见列表 4.9）相比，这里我们以不同的方式描述 `show()` 函数的参数。我们还会发现创建二维数组比创建静态数组困难。

## 列表 4.10. 将二维数组传递给函数

```cpp
#include <cstdio>
using namespace std;
// 接收二维数组
// 传递的函数:
void show(int** M, int p, int n) {
    for(int i=0;i<p;i++) {
        for(int j=0;j<n;j++) {
            printf("%4d",M[i][j]);
        }
    }
    printf("\n");
}
// 程序的主函数:
int main() {
    // 动态数组的大小
    // 以及循环控制变量:
    int a=3,b=5,i,j;
    // 创建指针数组:
    int** A=new int*[a];
    // 创建并填充内部数组:
    for(i=0;i<a;i++) {
      A[i]=new int[b];
      for(j=0;j<b;j++) {
        // 数组元素:
        A[i][j]=i*b+j+1;
      }
    }
    printf("数组的内容:\n");
    // 打印数组:
    show(A,a,b);
    // 删除内部数组:
    for(i=0;i<a;i++) {
      delete [] A[i];
    }
    // 删除指针数组:
    delete [] A;
    return 0;
}
```

我们从程序得到了以下输出

数组的输出（在列表 4.10 中）

数组的内容：

| 1 2 3 4 5 |
| 6 7 8 9 10 |
| 11 12 13 14 15 |

在向函数传递二维静态和动态数组时存在一些差异。传递动态数组时，没有必要指定第二个索引数组的大小。例如，上面示例中的 `show()` 函数适用于打印任何大小的二维动态数组。

## 向函数传递字符串

我们可以像传递任何其他一维数组一样向函数传递一维字符数组，不同之处在于我们不需要显式指定数组的大小。这是因为我们需要存储在数组中的字符串，而空字符决定了字符串的结束。

> 理论
> 向函数传递字符数组，只需传递指向数组第一个元素的指针（数组名）即可。

列表 4.11 包含一个参数为一维字符数组的程序。

```cpp
列表 4.11. 向函数传递字符数组
```

```cpp
#include <iostream>
using namespace std;
// 计算字符串长度的函数;
int getLength(char* str) {
int s=0;
for(int i=0;str[i];i++){
    s++;
}
return s;
}
// 计算字符串中空格数量的函数:
int getSpace(char* str(
```

## 第4章 函数

```cpp
int s=0;
for(int i=0;str[i];i++) {
    if(str[i] == ' ') {
        s++;
    }
}
return s;
}
// 该函数打印字符串及其
// 额外的特征：
void show(char* str) {
    cout<<"The string: "<<str<<endl;
    cout<<"Characters: "<<getLength(str)<<endl;
    cout<<"Spaces: "<<getSpace(str)<<endl;
    for (int k=1;k<=50;k++) {
        cout<<"-";
    }
    cout<<endl;
}
// 程序的主函数：
int main() {
    // 一个字符数组；
    char txt[100]="The C++ programming language";
    // 将字符数组传递给函数；
    show(txt);
    // 将字符串字量传递给函数：
    show((char*)"There are classes and objects in C++");
    return 0;
}
```

程序的输出如下：

## 第4章 函数

程序的输出（如列表 4.11所示所示

```
The string: The C++ programming language
Characters: 27
Spaces: 3

nThe string: There are classes and objects in C++
Characters: 36
Spaces: 6
```

我们在程序中创建了几个函数。我们使用这些函数来处理字符串（通过字符数组或字符串字面量实现）。特别是，我们描述了 `getLength()` 函数，它返回字符串中字符的数量。`getSpace()` 函数返回字符串中空格的数量。`show()` 函数打印传递给函数的字符串。`show()` 函数还打印了字符串的长度和字符串中的空格。这是通过调用 `getLength()` 和 `getSpace()` 函数实现的。这三个函数都将一个字符指针作为参数。该指针代表字符数组的。此外，我们也可以将字符串字面量传递给函数（因为字符串字面量是通过其指向字符串第一个字符的指针来处理的）。程序的主函数包含了对 `show()` 函数的调用。

## 细节

在 `show()` 函数的最后一次调用（使用字符串字面量）中，我们使用了显式类型转换 `char*`。这是因为字符串字面量是通过常量字符指针（类型为 `const char*`）传递的。C++ 禁止从 `const char*` 到 `char*` 的隐式类型转换，所以我们使用显式转换。

## 作为函数结果的指针

> 尽管如此，某些编译器（如 GCC）即使不使用显式转换也能编译程序。

函数的返回值可以是静态数组以外的任何类型。特别是，函数的返回值可以是指针。列表 4.12 包含一个程序，我们在其中创建了 `getMax()` 函数。我们将一个一维数值数组传递给函数，函数返回数组中最大元素的指针。考虑下面的代码。

- 列表 4.12. 函数返回指针

```cpp
#include <iostream>
using namespace std;
// 函数返回指针
int* getMax(int* nums, int n) {
    int i=0,k;
    // 寻找最大元素的索引：
    for(k=0;k<n;k++) {
        if (nums[k]>nums[i]) {
            i=k;
        }
    }
    // 函数的结果是一个指针：
    return nums+i;
}
// 函数打印数组：
void show(int* nums, int n) {
    for(int i=0;i<n;i++) {
        cout<<nums[i]<<" ";
    }
    cout<<endl;
}
// 程序的主函数：
int main() {
    // 数组的大小：
    const int size=10;
    // 创建数组：
    int numbers[size]={1,5,8,2,4,9,11,9,12,3};
    // 打印数组：
    show(numbers,size);
    // 将函数的结果
    // 存储指针：
    int* maxPnt=getMax(numbers,size);
    // 打印值：
    cout<<"The greatest value is: "<<*maxPnt<<endl;
    return 0;
}
```

```cpp
cout<<nums[i]<<" ";
}
cout<<endl;
}
// 程序的主函数：
int main() {
    // 数组的大小：
    const int size=10;
    // 创建数组：
    int numbers[size]={1,5,8,2,4,9,11,9,12,3};
    // 打印数组的内容：
    show(numbers,size);
    // 将函数的结果保存到 
    // 变量 maxNum 中：
    int maxNum=getMax(numbers,size);
    // 打印最大值：
    cout<<"The greatest value is "<<maxNum<<endl;
    // 将值赋值给变量：
    maxNum--=100;
    // 打印数组的内容：
    show(numbers,size);
    // 将函数的结果保存到
    // 引用 maxRef 中：
    int &maxRef=getMax(numbers,size);
    // 打印最大值：
    cout<<"The greatest value is "<<maxRef<<endl;
    // 将值赋值给引用：
    maxRef--=200;
    // 打印数组的内容：
    show(numbers,size);
    cout<<"The greatest value is "";
    // 计算新的最大值：
cout<<getMax(numbers,size)<<endl;
return 0;
}
```

# 第 4 章 函数 145

## 程序的输出（在列表 4.13 中）

1 5 8 2 4 9 11 9 12 3

The greatest value is 12

1 5 8 2 4 9 11 9 12 3

The greatest value is 12

1 5 8 2 4 9 11 9 -200 3

The greatest value is 11
