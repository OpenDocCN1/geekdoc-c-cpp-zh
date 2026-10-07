
```cpp
int a[5] = {1, 2, 3, 4, 5};
for (int i = 0; i < 5; i++) {
    cout << a[i] << endl;
}
```

# 第 7 章 一维数组

```cpp
// 检查打开成功并读取数据到数组。
if(!sensor3.fail()) {
    for (int k=0; k<10; ++k) {
        sensor3 >> time[k] >> motion[k];
        cout << time[k] << '\t' << motion[k] << endl;
    }
} else {
    cout << "  Could not open file sensor3.dat..goodbye." << endl;
}
return 0;
```

如果数据 `sensor3.dat` 包含以下数据集：

```
0.0 1
0.1 1
0.2 2.5
0.3 1.7
0.4 2
0.5 2.5
0.6 3.5
0.7 1.5
0.8 1.5
0.9 1
```

那么数组 `time` 和 `motion` 将包含以下值：

| double time | double motion |
| :--- | :--- |
| 0.0 | 1.0 |
| 0.1 | 1.0 |
| 0.2 | 2.5 |
| 0.3 | 1.7 |
| 0.4 | 2.0 |
| 0.5 | 2.5 |
| 0.6 | 3.5 |
| 0.7 | 1.5 |
| 0.8 | 1.5 |
| 0.9 | 1.0 |

程序 `chapter7_2` 的输出如下：

```
0 1
0.1 1
0.2 2.5
0.3 1.7
0.4 2
0.5 2.5
```

显示以下每组语句中定义的数组的内容。

- 1. `int x[10]={-5, 4, 3};`
- 2. `char letters[] = {'a', 'b', 'c'};`
- 3. `double z[4];`

```
z[1] = -5.5;
z[2] = z[3] = fabs(z[1]);
```

- 4. `double time[9];`

```
for (int k=0; k<=8; k++)
{
  time[k] = (k-4)*0.1;
}
```

- 5. 显示以下程序生成的输出：

```cpp
#include<iostream>
using namespace std;
int main() {
  int arr[5], i, k;
  for(i=0; i<5; ++i) {
    for(k=1; k<3; ++k) {
      arr[i] += k*i;
    }
    cout << "arr[" << i << "] " << arr[i] << endl;
  }
  return 0;
}
```

## 计算与输出

对数组元素的计算方式与简单对象的计算方式一样，但必须使用偏移量 `offset` 来指定单个数组元素。为了说明这一点，下一个程序使用 `for` 循环从数据文件中读取指定数量的浮点值，并将值赋值给数组 `y`。`y` 的声明大小为 100，因此程序将允许将最多 100 个值赋值给 `y`，以避免超出数组边界。程序确定数据的平均值并将其存储在 `yAve` 中。然后统计并打印数组中大于平均值的数量。

## 第 7 章 一维数组

```
/*
* 程序 chapter7_
* 此程序从数据文件中读取最多 100 个值，
* 并确定大于平均值的数量。
*/
```

```cpp
#include<iostream> // 需要 cin, cout, cerr
#include<fstream> // 需要 istream
#include<string> // 需要 string
using namespace std;

int main()
{
    // 定义数组大小常量
    const int N = 100;

    // 声明并初始化对象
    string filename;
    int count=0, numberOfValues;
    double y[N], yAve, sum=0;
    ifstream lab;

    // 提示输入文件名
    cout << "Enter name of input file: ";
    cin >> filename;

    // 打开数据文件并将数据读入数组
    lab.open(filename.c_str());
    if (lab.fail())
    {
        cerr << "Error opening file\n";
        exit(1);
    }

    // 文件已打开
    // 读取数据数量
    lab >> numberOfValues;
    // 不要超出数组边界
    if (numberOfValues > N)
    {
        cerr << "Number of data values "
             << "exceeds maximum array size of " << N
             << " values will be read." << endl;
        numberOfValues = N;
    }
    int k;
    for (k=0; k<numberOfValues; ++k)
    {
        lab >> y[k];
        sum += y[k];
    }

    // 计算平均值并统计大于平均值的数量
    yAve = sum/numberOfValues;
    for (int k=0; k<numberOfValues; ++k)
    {
        if (y[k] > yAve)
            count++;
    }

    // 打印数量
    cout << count << " values greater than the average" << endl;

    // 关闭文件并退出程序
    lab.close();
    return 0;
}
```

如果程序的目的是确定数据文件中值的平均值，则不需要数组。循环可以将每个值读入同一个对象并累加到和中。然而，由于我们需要将每个值与平均值进行比较以统计大于平均值的数量，我们选择使用数组来存储这些值以便再次访问。

使用偏移量访问并打印数组值。例如，以下语句打印了数组的第一个和最后一个值：

```cpp
cout << "first and last array values: " << endl;
cout << y[0] << " " << y[numberOfValues-1] << endl;
```

以下循环打印 `y` 的所有 100 个值，每行一个：

```cpp
cout << "y values: " << endl;
for (int k=0; k<N; ++k)
{
    cout << y[k] << endl;
}
```

注意数组的值必须逐个打印，因为 C++ 不支持数组的聚合输出。在打印这样的大数组时，我们可能希望在同一行打印多个值。以下语句使用模运算在每组五个值之前跳到新行：

```cpp
cout << "y values: " << endl;
for (int k=0; k<numberOfValues; ++k)
{
    if (k%5 == 0)
        cout << y[k] << endl;
    else
        cout << y[k] << " ";
}
cout << endl;
```

## 第 7 章 一维数组

与此处所示类似的语句可以将数组值写入数据文件。例如，以下语句将使用同一个流在数据文件的一行打印 `y[k]` 的值：

```cpp
sensor << y[k] << endl;
```

由于包含了 `endl` 操符符写入文件的下一个值将位于新行。

![](img/4456642232ef4a1bd7dfe37e0176d335_0.png)

- 1. 不使用数组重写程序 `chapter7_3`。提示：计算平均值，然后关闭并重新打开输入文件，统计大于平均值的数量。第二次读取文件之前需要清除错误位 `ebit` 吗？
- 2. 考虑以下程序：

```cpp
#include<iostream>
using namespace std;
int main() {
    char greeting[] = "HelloWorld";
    int numbers[] = {1,2,3,4,5};
    cout << greeting << endl;
    cout << numbers << endl;
    return 0;
}
```

编译并运行此程序。解释输出。

数组的最大尺寸即可以赋值给数组的元素数量在类型声明语句中确定，并可以在程序后续引用以避免超出数组边界。如果更改了最大尺寸，程序中可能有多个地方需要修改。如果使用符号常量来指定数组的声明大小，更改数组的大小就会变得简单。要更改最大尺寸，只需更改符号常量的值。这种风格切换在多个程序员在同一个软件项目的编程环境中尤为重要。许多后续程序说明了使用符号常量来定义数组的最大尺寸。

表 7.1 给出了偏移量括号的更新优先级顺序。括号和下标在其他运算符之前结合。如果括号和下标在同一个语句中，它们从左到右结合；如果嵌套，则先求值内层。

### 表 7.1 运算符优先级

| 优先级 | 操作 | 结合性 |
| :--- | :--- | :--- |
| 1 | () [] | 内层优先 |
| 2 | ++ -- ! (type) | 从右向左（单目） |
| 3 | * / % | 从左到右 |
| 4 | + - | 从左到右 |
| 5 | <= >= | 从左到右 |
| 6 | == != | 从左到右 |
| 7 | && | 从左到右 |
| 8 | || | 从左到右 |
| 9 | ?: | 从右向左 |
| 10 | = += %= | 从左到右 |
| 11 | \| | 从左到右 |

### 练习！

假设数组 `s` 已通过以下语句定义：
`int s[]={3, 8, 15, 21, 30, 41};`

通过手动确定以下每组语句的输出：

- 1. `for (int k=0; k<=5; k++)`
  {
    `cout << s[k] << ' ' << s[k+1] << endl;`
  }
- 2. `for (int k=0; k<=5; k++)`
  {
    `if (s[k]%2 == 0)`
     `cout << s[k] << ' ';`
  }
  `cout << endl;`

## 函数参数

当将数组信息传递给函数时，通常使用两个参数；一个参数指定特定数组，另一个参数指定数组中使用的元素数量。通过指定数组中使用的元素数量，函数变得更加灵活。例如，如果函数指定了一个整数数组，那么该函数就可以用于任何整数数组；指定数组元素的数量确保了我们使用了正确的大小。此外，数组中使用的元素数量可能会随时间变化而变化。例如，数组可能会从数据文件中读取元素；此时，元素的数量取决于运行程序时使用的特定数据文件。然而，在所有这些示例中，数组必须声明为一个最大尺寸，而实际使用的元素数量可以小于或等于该最大值。

考虑下面提供的 `chapter7_4`，它从数据文件中读取数组，并引用一个函数来确定数组中的最大值。对象 `npts` 用于计数从数据文件中读取并存储在数组中的实际值数量；`npts` 的值可以小于或等于定义的数组大小 `100`。我们必须小心，不要给数组分配超过 100 个值，并且必须准确计数分配给数组的实际值数量。该函数有两个形式参数：数组名和数组中的实际点数，如原型所示。`chapter7_4` 的流程图见图 7.1 ![](img/44564223e4f18bd7dfe3176d337_0.png)

图 7.1

### 7.1 节数组

```cpp
/*
 * Program7_4
 * 此程序从数据文件中读取数值，
 * 并调用函数来确定最大值。
 */
#include<iostream> // 用于 cin, cerr。
#include<fstream> // 用于 ifstream。
#include<string> // 用于 string。
using namespace std;

// 定义函数原型
double maxval(const double x[], int n);
int main()
{
    // 声明对象
    const int N = 100;
    int npts=0;
    double y[N], temp;
    string filename;
    ifstream lab;
    // 提示文件名并打开数据文件
    cout << "Enter the name of data file:";
    cin >> filename;
    lab.open(filename.c_str());
    if(lab.fail())
    {
        cerr << "Error opening file\n";
        exit(1);
    }
    // 从文件中读取一个数值
    lab >> temp;
    // 只要数组还有空间且未遇到文件末尾，
    // 将值赋值给数组并读取下一个数值。
    while (npts < N && !lab.eof())
    {
        y[npts] = temp; // 将值赋值数组
        npts++; // npts 自增
        lab >> temp; // 读取下一个值
    }
    // Find并打印最大值
    cout << "Maximum value: " << maxval(y,npts) << endl;
    // 关闭文件并退出
    lab.close();
    return 0;
}
```

## 第 7 章 一维数组

```cpp
/*
 * 此函数返回含有 n 个元素的数组
 * 最大值。
 */
double maxval(const double x[], int n) {
    // 声明局部对象
    double maxVal;
    // 确定数组中的最大值
    maxVal = x[0];
    for (int k=1; k<n; ++k) {
        if (x[k] > maxVal)
            maxVal = x[k];
    }
    // 返回最大值
    return maxVal;
}
```
