
图 7.21 | 展示 C++ 标准库类模板 `vector`。（4 部分中的第 2 部分）。

## 7.10 C++ 标准库类模板 `vector` 简介

```cpp
if (integers1 == integers2) {
    cout << "integers1 and integers2 are equal" << endl;
}

// 使用方括号将位置 5 处的值作为右值
cout << "\nintegers1[5] is " << integers1[5];

// 使用方括号创建左值
cout << "\nassigning 100 to integers1[5]" << endl;
integers1[5] = 1000;
cout << "integers1: ";
outputVector(integers1);

// 尝试使用越界下标
try {
    cout << "\nAttempt to display integers1.at(15)" << endl;
    cout << integers1.at(15); // 错误：越界
} catch (out_of_range &e) {
    cerr << "An exception occurred: " << endl;
}

// 改变 vector的大小
cout << "\nCurrent integers3 size is: " << integers3.size() << endl;
integers3.push_back(1000); // 在 vector 末尾添加 1000
cout << "\nNew integers3 size is: " << integers3.size() << endl;
cout << "\nintegers3 now contains: " << endl;
outputVector(integers3);

// 输出 vector 内容
void outputVector(const vector<int>& items) {
    for (int &item : items) {
        cout << item << " ";
    }
    cout << endl;
}

// 输入Vector 内容
void inputVector(vector<int>& items) {
    for (int &item : items) {
        cin >> item;
    }
}
```

`vector` `integers1` 的大小为 7
`vector` after initialization: 0 0 0 0 0 0 0

`vector` `integers2` 的大小为 10
`vector` after initialization: 0 0 0 0 0 0 0

图 7.21 | 展示 C++ 标准库类模板 `vector`。（4 部分中的第 3 部分）。

17 个整数： 
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

输入后，`vectors` 包含：
`integers1`: 1 2 3 4 5 6 7
`integers2`: 8 9 10 11 12 13 14 15 16 17

求值：`integers1 != integers2`
`integers1` 和 `integers2` 不相等

`vector` `integers3` 的大小为 7
`vector` after initialization: 1 2 3 4 5 6 7

将 `integers2` 赋值给 `integers1`：
`integers1`: 8 9 10 11 12 13 14 15 16 17
`integers2`: 8 9 10 11 12 13 14 15 16 17

求值：`integers1 == integers2`
`integers1` 和 `integers2` 相等

`integers1[5]` 是 13
将 1000 赋值给 `integers1[5]`
`integers1`: 8 9 10 11 12 1000 14 15 16 17

尝试显示 `integers1.at(15)`
发生异常：Invalid `vector<T>` subscript

当前 `integers3` 大小: 7
New `integers3` size now contains: 1 2 3 4 5 6 7 1000

图 7.21 展示 C++ 标准库类模板 `vector`：（4 部分中的第 4 部分）

### 创建 `vector` 对象

第 13–14 行创建了两个存储 `int` 类型值的 `vector` 对象——`integers1` 包含七个元素，`integers2` 包含 10 个元素。默认情况下，每个 `vector` 对象的所有元素都设置为 0。像数组一样，`vector` 可以通过将 `<int>` 替换为相应的类型来定义以存储大多数数据类型。

注意，我们使用括号而不是大括号向每个 `vector` 的构造函数传递大小参数。在创建 `vector` 时，如果使用括号，则创建一个包含指定数量元素的 `vector`。

```cpp
vector<int> integers1(7);
vector<int> integers2(10);
```

如果使用大括号，则可以使用初始化列表来初始化 `vector`。

```cpp
vector<int> integers1{1, 2, 3, 4, 5, 6, 7};
vector<int> integers2{8, 9, 10, 11, 12, 13, 14, 15, 16, 17};
```

使用大括号时，`vector` 的元素将根据初始化列表中的值初始化。

```cpp
vector<int> integers3{1, 2, 3, 4, 5, 6, 7};
integers3.push_back(1000);
```
