

## 3.2.4 搜索

按索引访问数组中的每一个元素（称为*遍历*）对于大型数组来说效率不高，因此我们应该使用一种算法来查找我们想要的元素。以下便是这些搜索方法。

### 线性搜索

在线性搜索中，我们通过遍历数组并检查搜索元素是否与数组元素匹配，来顺序查找所需的元素。

#### 线性搜索算法

1. 开始。
2. 如果未给定数组，则从用户处获取大小和元素输入。
3. 从用户处输入搜索元素。
4. 初始化 for 循环，从 i=0 到索引 size-1。
5. 使用嵌套 if 循环判断搜索元素是否等于 array[i]。
6. 如果结果为真，则找到匹配项；跳出循环。
7. 如果结果为假，则执行代码的 else 部分。
8. 停止。

#### 代码：线性搜索示例

```cpp
#include<iostream>
using namespace std;
int main()
{
    int size,e,flag=0;
    cout<<"\nGive the size of the array "<<endl;
    cin>>size;
    int array[size];
    cout<<"Enter the elements of the array "<<endl;
    for(int i=0;i<size;i++)
    {
        cin>>array[i];
    }
    cout<<"What do you wish to search for"<<endl;
    cin>>e;
    for(int i=0;i<size;i++)//traverse array
    {
        if(array[i]==e)//check with element to match
        {
            flag=i;
            break;
        }
    }
    if(flag)
        cout<<"Element "<<e<<" is at index "<<flag;
    else
        cout<<"Element "<<e<<" is not present\n";
    return 0;
}
```

#### 输出

```
Give the size of the array
4
Enter the elements of the array
11
23
66
77
What do you wish to search for
88
Element 88 is not present
```

你还可以通过设置一个初始为 false 的标志，并在 if 语句内将 i 的值赋给它，来轻松找到搜索元素所在的索引。

### 二分搜索

在该搜索算法中，我们获得一个按从小到大顺序排列的有序数组。然后，通过找到中点将工作分成两半，并基于中点继续寻找下一半。程序检查搜索元素是大于还是小于中间元素，并重复此过程，直到数组为空并找到匹配的元素。

#### 二分搜索算法

1. 开始。
2. 如果未给定数组，则从用户处获取大小和元素输入。
3. 从用户处输入搜索元素。
4. 调用二分搜索函数，并传入数组、`firstindex`、`lastindex` 和搜索元素。
5. 执行嵌套 if 循环，判断搜索元素是等于 `array[mid]`、小于 `array[mid]` 还是大于 `array[mid]`。
6. 如果结果为真，则找到匹配项，返回 mid。
7. 如果结果为假，则返回 0 并退出循环。
8. 停止。

#### 代码：二分搜索示例

```cpp
#include<iostream>
using namespace std;
int binarySearch(int array[], int a, int b, int s) {
    if (a <= b) {
        int mid = (a + b)/2;
        if (array[mid] == s)
            return mid;
        if (array[mid] > s)
            return binarySearch(array, a, mid-1, s);
        if (array[mid] < s)
            return binarySearch(array, mid+1, b, s);
    }
    return 0;
}
int main(void) {
    int array[] = {23,67,45,11,33,44,55};
    int size = sizeof(array)/sizeof(array[0]);
    int s;
    cout << "Enter the element to search: \n";
    cin >> s;
    int flag = binarySearch(array, 0, size-1, s);
    if(flag){
        cout << s << " found at index " << flag << "\n";
    }else{
        cout << s << " is not in the array sorry!";
    }
    return 0;
}
```

#### 输出

```
Enter the element to search:
55
55 found at index 6
```

## 3.3 多维数组

我们之前已经了解了 1D 数组及其操作，现在让我们继续学习 2D 和 3D 数组。这类数组具有行和列，你可以通过以下语句来表示它们：

2D 数组：datatype array_name[rows][columns];

3D 数组：int three_d[array_no][rows][columns];

### 代码：演示 2D 和 3D 数组的示例

```cpp
#include<iostream>
using namespace std;

int main()
{
    int array[2][3] = {{5,1,4}, {2,3,7}};
    cout<<"\n2D Array:\n";
    for (int i = 0; i < 2; ++i) {
        for (int j = 0; j < 3; ++j) {
            cout << array[i][j]<<" ";
        }
        cout<<"\n";
    }

    int x[2][3][3] = { { { 7, 1,5 }, { 26, 3,88 }, { 45, 5,78 } },
        { { 66, 77,33}, { 84, 9,32 }, { 10, 11,12 } } };
    cout<<"\n3D Array:\n";
    for (int m = 0; m < 2; ++m) {
        for (int n = 0; n < 3; ++n) {
            for (int q = 0; q < 3; ++q) {
                cout<< x[m][n][q]<<" ";
            }
        }
    }
}
```

## 3.4 字符串

```cpp
int main() {
    string str1;
    cout << "Enter your name: ";
    cin >> str1;
    cout << "Name: " << str1;
    return 0;
}
```

#### 输出

```
Enter your name:
Carlos Sainz
Name: Carlos
```

## 3.5 字符串函数

C++ 字符串类提供了大量用于处理字符串的函数，如下表所示。

**表 3.1** 字符串函数的语法与功能

| 函数语法 | 功能 |
|---|---|
| `strcat(char_arr1, char_arr2);` | 连接两个字符数组 |
| `string1.append(string2);` | 将一个字符串追加到另一个字符串的末尾 |
| `int length();` | 查找给定字符串的长度 |
| `void swap(string& string1);` | 交换两个字符串 |
| `int compare(const string& string1);` | 检查两个字符串是否相等 |
| `int size()` | 查找字符串的字节大小。 |
| `int find(string& string1, int pos, int size)` | 在给定位置查找字符串 |
| `int copy(string& string1)` | 将一个字符串的内容复制到另一个字符串 |
| `int capacity()` | 返回已分配的内存空间大小 |
| `getline()` | 读取输入字符串，直到遇到 `\n` 字符 |
| `resize()` | 增加或减少字符串的大小 |
| `end()` | 标识字符串的末尾 |
| `rend()` | 反转字符串的末尾 |
| `char& at(int pos)` | 查找指定位置的字符 |
| `string& append(const string& string1)` | 将一个字符串追加到另一个字符串 |

## 小结

- 数组是 C++ 中的一种数据类型，用于在相同名称下存储同类数据，并通过索引进行访问。
- 所有数组元素都存储在连续的内存位置中。
- 索引 0 处的元素也可以说是数组名的指针，数组的下标范围一直到 n-1。
- 数组仅通过其名称传递给函数。
- 枚举（Enum）是用户自定义的数据类型。
- 按索引逐个访问每个元素称为遍历数组。
- 可以使用线性算法或二分算法搜索数组中的元素。
- 数组的数组称为多维数组。
- C++ 中的字符串是一种数据类型，表示一组字符，这些字符以字节集合的形式存储在连续的内存位置中。
- 我们讨论了诸如 concat、compare、length 和 size 等字符串函数。

## 练习

### 理论题

1. 讨论 C++ 中数组的概念。
2. 如何声明一个数组？
3. 数组有哪些优点和缺点？
4. 解释 2D 和 3D 数组是如何工作的。
5. 比较数组的线性搜索算法和二分搜索算法。
6. 关于数组，维度和下标分别是什么意思？
7. C++ 中的字符串是什么？
8. 比较字符串和字符数组。
9. 结合示例讨论 C++ 中对字符串进行的各种操作。

### 多项选择题

1. 数组元素总是存储在 __________ 内存位置中。
   - a. 连续的
   - b. 随机的
   - c. 连续的和随机的
   - d. 以上都不是

2. 字符串是一种 __________。
   - a. C++ 中的数据类型
   - b. 以空字符结尾的字符数组
   - c. 以空字符开头的字符数组
   - d. 以 0 结尾的整数数组

3. 选择关于字符串对象的正确陈述。
   - a. 它们以空字符“\0”结尾。
   - b. 它们具有有限的、确定的大小。
   - c. 它们是动态的。
   - d. 以上都不是

4. 以下哪一项或哪几项用于查找字符串的长度？
   - a. length()
   - b. size()
   - c. max_size()
   - d. size() 和 length() 都可以

5. 以下哪项是声明数组的正确方式？
   - a. int array;
   - b. int array[size];
   - c. array{ele};
   - d. array{ele,ele} array[size];

