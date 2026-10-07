

# 输入、输出模板

如果文件已存在，输出将追加到文件末尾（而不是覆盖）。
`simpleOut` 程序产生的结果如下：

```
$ g++ -Wall simpleOut.cpp -o simpleOut
$ simpleOut out.txt 3 4
$ cat out.txt
1 2 3 4
2 4 6 8
3 6 9 12
```

文件结束
为了有效处理具有实际意义的问题，应该构造一个输出类。该类的对象可以用于将数据写入指定的文件。可能会创建的方法或对象构造的方法取决于数组的数据类型。这将需要不同的方法来处理整数和浮点数据，但由于如果我们能创建一个泛型数据类型，允许从（例如）任何基本类型构造的数组仅通过单个方法即可写入文件，那么这些工作就可以很方便地完成。这可以通过类模板来实现，并且我们将开发该解决方案。

创建模板类的语法如下：

```cpp
template<class T> class className{
    成员声明和方法原型
};
```

在这里，T 代表调用程序必须指定的排序“卡牌字字”。在模板类的通用语境下，T 可以可以是任何数据类型，包括已创建的类型。出于统计目的，T 大多数是基本类型之一，如 `char`、`int`、`float` 等，在整个章节中从这个角度来看也没有害。
方法的声明以及公共和私有类模板的与非模板情况完全相同。要在类声明之外指定方法定义：

```cpp
template<class T> returnType className<T>::methodName(arguments){
    方法体
};
```

这里有一个陷阱；方法定义必须与类声明位于同一个文件中。之前，类声明在头文件和 `.cpp` 文件中与方法定义是物理分离的。`.cpp` 文件被编译成对象文件，最后链接在一起以生成可执行文件。这种方法对于模板存在的问题在于，泛型 `T` 被用作实际数据类型的占位符，该类型将替换为 T 以产生一个特定对象。在没有指定实际数据类型的情况下，类没有办法为对象文件的创建分配存储。这只有当编译器对 T 做出特定选择时才会进行，此时编译器本质上会同时处理源码（即 `.cpp` 文件）和类的定义（位于头文件中），并用“值”替换 T。然而，如果 `.cpp` 文件是单独编译的，编译器就没有它，它会假设所有具有 T 所需“值”的方法都存在于预编译的对象文件中。将代码组合的任务就落到了链接器，链接器会查找对象文件以寻找使用 T 指定值（或多个值）的方法定义，而没有

> † 标准 `std::ios_base::app` 的值是 C++ `ios_base` 类的 `static const` 成员，提供了所有其他类使用的常量和函数。

`simpleTemp` 类背后的基本思想很容易推广到构造某些有用的东西。特别是，列表 3.20 提供了一个可以用于文件输出的模板类。

列表 3.20 fileOut.h

```cpp
//fileOut.cpp
#include <iostream>
#include <fstream>
#include <cstdlib>

template<class T = double> class fileOut{
char* fName;
bool App;

public:
    fileOut(char* fileName, bool app = 0);
    ~fileOut() {};

    void write(int nrows, int ncols, const T* const* pData) const;
};

//方法定义
template<class T> fileOut<T>::fileOut(char* fileName, bool app){
fName = fileName;
App = app;
}

template<class T> void fileOut<T>::write(int nrows, int ncols, const T* const* pData) const {

    if(App == 0) {
        std::ofstream outFile;
        outFile.exceptions(std::ofstream::failbit |
        std::ofstream::badbit);
        try{
            outFile.open(fName);
        } catch(std::ofstream::failure e) {
            std::cout << "Error opening output file: " << e.what()
            << std::endl;
        }
        for(int i = 0; i < nrows; i++) {
            for(int j = 0; j < ncols; j++) {
                outFile << " " << pData[i][j] << " ";
            }
            outFile << std::endl;
        }
        outFile.close();
    } else {
        std::ofstream outFile(fName, std::ios::app);
        if(!outFile.is_open()){
            std::cout << "Error opening output file!" << std::endl;
        }
        for(int i = 0; i < nrows; i++) {
            for(int j = 0; j < ncols; j++) {
                outFile << " " << pData[i][j] << " ";
            }
        }
        outFile.close();
    }
```

该类有两个成员：输出文件 `fileName` 和一个指示输出是否追加到 `fileName` 的布尔变量 `App`。在类中 `App` 使用了 `false` 作为默认值。构造函数方法是 `write`，它将数组指针的行和列维度作为参数。注意使用了第 3.8 节中的 `T* const`，这确保了方法不会修改 `pData` 的数据。`write` 方法根据 `App` 的值以创建/覆盖或追加模式打开一个输出文件。在任何情况下，都会进行检查以确保目标文件已打开。对于 `App = 0` 的第一种情况，使用第 3.8 节中的 `try/catch` 进行检查。`App = 1` 的实例通过流成员处理，如果在连接到指定的输出时遇到问题，则该成员求值为为 `false`。现在让我们探索列表 3.20 中使用异常的一些细节。这里的标志位指示提供流状态信息的输入和输出对象。这些是名为 `ebit` 的变量（注：原文此处可能有误，指标志位变量）。

`simpleTemp` 类背后的基本思想很容易推广到构造某些有用的东西。特别是，列表 3.20 提供了一个可以用于文件输出的模板类。

该类有两个成员：输出文件 `fileName` 和一个布尔变量 `App`，指示输出是否追加到 `fileName`。在类中 `App` 使用了 `false` 作为默认值。构造函数方法是 `write`，它将数组指针的行和列维度作为参数。注意使用了第 3.8 节中的 `T* const`，这确保了方法不会修改 `pData` 的数据。`write` 方法根据 `App` 的值以创建/覆盖或追加模式打开一个输出文件。在任何情况下，都会进行检查以确保目标文件已打开。对于 `App = 0` 的第一种情况，使用第 3.8 节中的 `try/catch` 进行检查。`App = 1` 的实例通过流成员处理，如果在连接到指定的输出时遇到问题，则该成员求值为 `false`。现在让我们探索列表 3.20 中使用异常的一些细节。这里的标志位指示提供流状态信息的输入和输出对象。

*(注：由于提供的原文后半部分存在大量重复和逻辑乱码，译文已根据要求翻译并清理了重复的逻辑内容。)*

