

## 7.2 应用问题求解：飓风类别

飓风是伴有极强风力和暴雨的热带风暴。（在西北太平洋，它们被称为台风；在印度洋，则称为气旋。）这些热带风暴，或气旋，是通常在夏季和初秋形成的低压系统。巨大的旋转气团在卫星图像上清晰可见，由于这些风暴可能对人口稠密地区造成损害，因此会被仔细追踪。如果风暴中的风速在每小时 38 至 74 英里之间，则称为热带风暴；如果风速超过每小时 74 英里，则该风暴为热带气旋，即飓风。萨菲尔-辛普森等级根据风速定义了飓风强度的类别。在本节中，我们将更详细地定义萨菲尔-辛普森等级，然后开发一个程序，读取包含当前风暴及其峰值风速的数据文件。然后，根据风速，我们打印一份报告，其中包含足够强以被归类为飓风的风暴信息。

飓风强度的萨菲尔-辛普森等级用于根据风暴若袭击人口稠密地区可能造成的损害程度来分类飓风。以下是五个类别的主要特征：

- 1 类
  - 风速：74–95 英里/小时
  - 风暴潮：4–5 英尺
  - 对财产造成轻微损害

- 2 类
  - 风速：96–110 英里/小时
  - 风暴潮：6–8 英尺
  - 对财产造成中度损害

- 3 类
  - 风速：111–130 英里/小时
  - 风暴潮：9–12 英尺
  - 对财产造成严重损害

- 4 类
  - 风速：131–155 英里/小时
  - 风暴潮：13–18 英尺
  - 对财产造成极端损害

- 5 类
  - 风速：超过 155 英里/小时
  - 风暴潮：大于 18 英尺
  - 对财产造成灾难性损害

表 7.2 列出了 1950 年至 2002 年期间袭击美国的十二场最强飓风。（你会发现，使用互联网获取这些飓风的更多细节很有趣。）

| 飓风 | 年份 | 类别 |
|---|---|---|
| Hazel | 1954 | 4 |
| Audrey | 1957 | 4 |
| Donna | 1960 | 4 |
| Carla | 1961 | 4 |
| Camille | 1969 | 5 |
| Celia | 1970 | 3 |
| Frederic | 1979 | 3 |
| Allen | 1980 | 3 |
| Gloria | 1985 | 3 |
| Hugo | 1989 | 4 |
| Andrew | 1992 | 5 |
| Opal | 1995 | 3 |

每年都有超过 100 场具有成为飓风潜力的风暴。编写一个程序，读取包含当前风暴信息的数据文件，该信息包括识别编号和迄今在风暴中测得的最高风速（以英里每小时，或 mph 为单位）。程序应打印所有风速足够高、足以被归类为飓风的风暴列表。除了识别编号（整数）外，还应打印峰值风速和相应的飓风强度类别。此外，在风速最大的飓风的识别编号后打印一个星号。

### 1. 问题陈述

使用包含当前风暴信息的数据文件，确定哪些风暴是飓风。

### 2. 输入/输出描述

I/O 图显示数据文件作为输入，飓风信息作为输出。

![](img/0235a4ea835dc4575bd036e024a533b3_378_0.png)

### 3. 手算示例

假设数据文件包含以下五组数据：

| 识别编号 | 峰值风速 |
|---|---|
| 142 | 38 |
| 153 | 135 |
| 162 | 135 |
| 177 | 59 |
| 181 | 63 |

相应的输出将是以下报告：

### 符合飓风条件的风暴

| 识别编号 | 峰值风速 (mph) | 类别 |
|---|---|---|
| 153* | 135 | 4 |
| 177 | 76 | 1 |

请记住，星号标识风速最大的风暴。

### 4. 算法开发

我们首先开发分解大纲，因为它将解决方案划分为一系列顺序步骤。要打印飓风风暴的信息，我们不需要数组。我们可以在读取文件时直接完成，因为飓风状态仅取决于风速。然而，由于我们还需要使用星号来标识峰值风速的风暴，因此需要将所有信息存储在数组中。在确定最大值后，我们可以再次遍历数据，打印飓风信息，并为最大风速添加星号。

### 分解大纲

- 1. 将风暴数据读入数组，并确定最大风速。
- 2. 计算强度类别，并打印飓风风暴的信息，在最大值处添加星号。

我们将确定强度类别的步骤放入一个函数中。

### 伪代码细化

```
main: if file cannot be opened
    print error message
else
    read data into arrays, and determine max speed, npts
    set k to 0
    while k <= npts-1
        if mph[k] > 74
            if mph[k] = max speed
                print id[k], *, mph[k], category(mph[k])
            else
                print id[k], mph[k], category(mph[k])
                add 1 to k
category(mph) :
    category = 1;
    if mph >= 96
    category = 2
    if mph >= 111
    category = 3
    if mph >= 131
    category = 4
    if mph >= 155
    category = 5
```

```cpp
/*
**
** Program chapter7_6
**
** This program reads storm values from a data file
**
*/

#include<iostream> //Required for cin, cout, cerr.
#include<fstream> //Required for fin.
using namespace std;

//Function Prototypes.
double category(double speed);

int main()
{
 //Declare and initialize variables.
 //const int MAX_SIZE = 500;
 int k(0), npts, id[MAX_SIZE];
 double mph[MAX_SIZE], max(0);
 ifstream fin("storm1.txt");
 if(fin.fail())
 {
 cerr << "Could not open file storm1.txt" << endl;
 exit(1);
 }
 //Read data and determine maximum mph.
 fin >> id[k] >> mph[k];
 while(!fin.fail())
 {
 if (mph[k] > max)
 max = mph[k];
 }
 ++k;
 fin >> id[k] >> mph[k];
 //end while
 npts = k;

//Print hurricane report.
if(max > 74)
{
    cout << "Storms that Qualify as Hurricanes \n"
         << "Identification\t Peak Wind(mph)\t Category\n";
}
else
{
    cout << "No hurricanes in the file \n";
}
for(k=0; k<npts; ++k)
{
    if(mph[k] >= 74)
    {
        if(mph[k] == max)
        {
            cout << "\t" << id[k] << "*" << "\t\t" << mph[k] << "\t\t"
                 << category(mph[k]) << endl;
        }
        else
        {
            cout << "\t" << id[k] << "\t\t" << mph[k] << "\t\t"
                 << category(mph[k]) << endl;
        }
    }
} //end if k
//end for
fin.close();
return 0;
}

/*------------------------------------------------------------*/
/* This function determines the hurricane intensity           */
/* category.                                                  */
double category(double speed)
{
    //Declare variables.
    int intensity(1);

    //Determine Category.
    if(speed >= 155)
    {
        intensity = 5;
    }
    else if(speed >= 131)
    {
        intensity = 4;
    }
    else if(speed >= 111)
    {
        intensity = 3;
    }
    else if(speed >= 96)
    {
        intensity = 2;
    }
    return intensity;
}
/*-----------------------------------------------------*/
```

### 5. 测试

我们使用包含手算示例的文件开始测试，得到以下交互：

| 识别编号 | 峰值风速 (mph) | 类别 |
| :--- | :--- | :--- |
| 153* | 135 | 4 |
| 177 | 76 | 1 |

### 修改 7.2

这些问题与本节开发的用于打印飓风强度报告的程序有关。

- 1. 修改程序，使其仅打印风速最大的飓风的信息。
- 2. 修改程序，使其同时打印数据文件中的风暴数量。
- 3. 修改程序，使其同时打印数据文件中的飓风数量。
- 4. 修改程序，使其在报告末尾打印每个类别的飓风数量。
- 5. 修改程序，使其生成一个新数据文件，包含每个飓风的信息及其强度。

