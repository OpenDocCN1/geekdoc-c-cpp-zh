

# 源码 4.3：Import 类与示例实现

```cpp
// Import.h
#pragma once

#include "Utils.h"

#include <string>
using std::string;

class Import {
public:
    Import() {}
    virtual ~Import() {}

    // 成员函数声明
    vector<vector<double>> GetData(const string& fileName); // GetData()
private:
    // 成员变量声明
    Utils m_utils; // Utils类的实例
};

// Import.cpp
#include "Import.h"

#include <fstream>
#include <sstream>
#include <iostream>
using std::cout;
using std::ifstream;
using std::stringstream;

// 成员函数定义
vector<vector<double>> Import::GetData(const string& fileName)
{
    int ROW = 0, COLS = 0; // 初始化行和列
    string line, tmp;
    stringstream ss; // 创建一个 stringstream 对象

    ifstream file(fileName); // 将文件添加到 fstream

    getline(file, line); // 移除文件头
    ss.clear(); // 清除 stringstream

    ss << line;
    while (ss >> tmp) {
        COLS++; // 确定文件的列数 (COLS)
    }
    vector<vector<double>> data; // 声明一个 double 的二维 vector
    vector<double> v(COLS); // 声明一个 double 的一维 vector

    if(file.is_open()) {
        while (file.good()) {
            {
                data.push_back(v); // 向 data 中添加新行
                for (int COL=0; COL<COLS; COL++) {
                    file >> data[ROW][COL]; // 用元素填充行
                }
            }
            ROW++; // 跟踪当前的 ROW 并递增
        }
        data.pop_back(); // 移除数据末尾的空值
        std::cout << "\nFile: " << fileName << " \n";
        std::cout << " 导入了 " << data.size() * (COLS - 1) << " \n 个数值!\n";
        file.close(); // 关闭文件
    } else {
        m_utils.ErrorChk("无法加载文件");
    }

    return data;
}

// main.cpp
#include "Import.h"
#include <windows.h>
#include <iostream>
using std::cout;
using std::cin;

int main()
{
  SetConsoleTitle(L"Console Output");

  vector<vector<double>> data; // 为数值声明一个二维 vector
  Import ctai; // 创建 Import 类的实例

  // 调用 Import 类的 GetData 成员函数
  data = ctai.GetData("./data/cta_index.dat");

  vector<string> v; // 为基金名称声明一个一维 vector
  v.push_back("CTA");

  cout << "\n打印前18行:\n";
  Utils::PrintFile(data, v, 18); // 打印前18行

  cin.get();
  return 0;
}
```

![](img/2d1ac831a270bb08f8bec2205913dc_137_0.png)

注意在 C++ 中处理文件有许多方法，但这种方法提供了一个易于使用的标准方法，并且对于我们的需求。在 import.h 中我们实例化了 Utils 类变量 m_utils。这允许我们使用点符号访问 Utils 类的 `ErrorChk()` 方法。然而，我们必须在 Import 类头文件中包含 Utils 类文件 (Utils.h) 以实现访问。

![](img/2d1ac831a270bb08f8bec2205913dc_138_0.png)

图 4.2 CTA指数月收益柱状图

# 4.4 基础图表

## 4.4.1 价值指数 (Value Added Index)

从表格格式的基金收益序列中提取任何信息几乎是不可能的。考虑 CTA 指数的假设月收益；总计的正负收益。如图4.2所示，数据的简单柱状图可以直观展示 CTA 指数在此期间的表现，并识别高低点。

价值指数 (VAI) 是一项统计数据，显示特定报告频率（例如每日、每月）的基金收益表现。VAI 可以根据报告频率按每日或每月计算。VAI 由公式给出：
$VAI_{t+1} = VAI_t(1 + r_t)$

CTA 指数月收益的每月 VAI (VAI) 如图4.3所示。读取 CTA 指数1000 元投资的最终值可以得到 VAI；然而，它并没有告诉我们基金也报告每日和每周收益，但每月是最常见的。基金可能提供净资产价值 (NAV) 序列，在这种情况下，它们可以转换为时间 $t_1$ 和 $t_2$ 之间的收益 $r_{t_1,t_2} = \frac{NAV_{t_2}}{NAV_{t_1}} - 1$。

![](img/2d1ac831a270bb08f8bec2205913dc_139_0.png)

图 4.3 指数成立以来的 VAI 图。源码4.4 展示了 Stats类的 VAI 成员函数和方法实现。

# 源码 4.4：VAI 成员函数与方法实现

```cpp
// Stats.h
#pragma once

#include "Utils.h"

class Stats {
public:
    Stats() {}
    virtual ~Stats() {}

    // 成员函数声明
    double VAI(const vector<vector<double>>& v); // VAI()
private:
    // 成员变量声明
    Utils m_utils; // Utils类的实例
};

// 成员函数定义
// VAI()
double Stats::VAI(const vector<vector<double>>& v)
{
    unsigned int n = v.size(); // 声明无符号整数
    double vai; // 定义 VAI 的 double 类型

    vai = 1000.0; // 初始化为1000

    // 使用公式 (3.1) 计算 VAI
    for(unsigned int i=0; i<n; i++)
    { 
        vai *= (1 + v[i][v[0].size()-1);
    }
    return vai;
}

// main.cpp
#include "Import.h"
#include "Stats.h"
#include <windows.h>
#include <iostream>
using std::cout;
using std::cin;

int main()
{
    SetConsoleTitle(L"Console Output");

    vector<vector<double>> data; // 为数值声明一个二维 vector
    Import ctai; // 创建 Import 类的实例

    // 调用 Import 类的 GetData() 成员函数
    data = ctai.GetData("./data/cta_index.dat");

    Stats stats; // 创建 Stats 类的实例
    double vai; // 为 VAI 值声明一个 double 类型

    // 调用 Stats 类的 VAI() 方法函数
    vai = stats.VAI(data);

    // 输出结果
    cout << "\nVAI($)" << vai << "\n";

    cin.get();
    return 0;
}
```

![](img/2d1ac831a270bb08f8bec2205913dc_141_0.png)

在 for 循环中使用 `v[0].size()-1` 允许我们访问列，并且我们减了一，因为第一列只是表头。

