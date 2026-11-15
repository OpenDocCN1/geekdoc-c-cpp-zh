

| Validate() | 内存快照 | Pixel p1 | 值 | 类型 |
| :--- | :--- | :--- | :--- | :--- |
| 步骤 1: if (red > MAXVAL) overflowFlag = overflowFlag | RMASK; | Pixel p1 | 278 | 无符号 red |
| | | | 298 | 无符号 green |
| | | | 150 | 无符号 blue |
| | | | 4 | 无符号短整型 overflowFlag |
| 步骤 2: if (green > MAXVAL) overflowFlag = overflowFlag | GMASK; | Pixel p1 | 278 | 无符号 red |
| | | | 298 | 无符号 green |
| | | | 150 | 无符号 blue |
| | | | 6 | 无符号短整型 overflowFlag |
| 步骤 3: if (blue > MAXVAL) overflowFlag = overflowFlag | BMASK; | | | |

在步骤 1 中，对操作数 overflowFlag (00000000) 和 RMASK (00000100) 执行按位或运算时，结果为 4，如下所示：

```
00000000  overflowFlag
00000100  RMASK
----------
00000100  result of bitwise or
```

该操作的结果被赋给 overflowFlag，从而替换之前的值。在步骤 2 中，对操作数 overflowFlag (00000100) 和 GMASK (00000010) 执行按位或运算时，结果为 6，如下所示：

```
00000100  overflowFlag
00000010  GMASK
----------
00000110  result of bitwise or
```

overflowFlag 的结果值表明数据成员 red 发生溢出，数据成员 green 发生溢出，而数据成员 blue 未发生溢出。因此，语句 pixel1.overflow() 将返回布尔值 true，如下所示：

```
00000110  overflowFlag
00000111  CHECK
----------
00000110  result of bitwise and
```

我们现在将编写一个小型驱动程序来测试 Pixel 类的新方法。

```
/*---------------------------------------*/
/* Program chapter10_2 */
/* Driver program to test overflow state of Pixel */

#include "Pixel.h"
#include <iostream>
using namespace std;
int main()
{
    //Declare objects
    Pixel defaultP;
    Pixel grayP(100);
    Pixel redP(255,255,0);

    //Create overflow in red
    defaultP = grayP + redP;
    cout << defaultP << endl;
    if(defaultP.overflow() )
    {
        defaultP.reset();
    }
    cout << defaultP << endl;
    return 0;
}
```

示例运行的输出如下：

```
Ingers-MacBook-Pro:Programs jaingber$ g++ main.cpp Pixel.cpp
Ingers-MacBook-Pro:Programs jaingber$ ./a.out
355 100 100
255 100 100
```

我们可以看到表达式 defaultP.overflow() 返回了 true 值，表明已检测到溢出，并且已执行语句 defaultP.reset();，将 defaultP 的值重置为有效状态。

## 修改 10.1

- 1. 向 Pixel 类添加以下方法：

```
bool checkRed() const;
bool checkGreen() const;
bool checkBlue() const;
```

每个方法都应检查调用对象的 overflowFlag，如果在指定数据成员中发生溢出则返回 true，否则返回 false。

## 修改 10.1

- 2. 向 `Pixel` 类添加以下方法：

```cpp
void resetRed();
void resetGreen();
void resetBlue();
```

每个方法都应将调用对象的指定数据成员设置为 `MAXVAL`，并重置 `overflowFlag` 的相应位。

- 3. 修改输出函数

`friend ostream& operator<<(ostream& out, const Pixel& p)`

使 `Pixel` 的值使用冒号而不是空格来分隔红、绿、蓝值。

- 4. 修改输入函数

```
/*
 * Input >> operator. Expected pixel format is 100:150:100*
 */
friend istream& operator>>(istream& in, Pixel& p)
```

以处理不正确的格式，通过向用户发出警告并请求新输入。(*提示：* 请参阅第 5 章中讨论的错误处理。)

## 10.2 使用 IDE 构建 C++ 解决方案：Xcode 图像文件

数字图像可以存储在多种文件格式中，处理矢量图形时包括 CGM 和 SVG 格式，处理栅格图形时包括 JPEG、GIF、TIFF 和 PPM 格式。有大量软件包可用于查看、转换和修改数字图像。

栅格图形常用于在 Internet 上存储数字图像。栅格图像定义为图像元素（或像素）的矩形网格。该网格称为位图或像素图。位图的大小由以像素为单位的宽度和高度定义。对于彩色图像，每个像素表示一个定义为红、绿、蓝三元组 (R, G, B) 的颜色值。R、G 和 B 的值范围从零到图像文件中指定的最大颜色值。

PPM（可移植像素图）格式是为表示栅格图像而开发的一组文件格式之一。图 10.3 中提供的 PPM 图像由 C++ 程序生成。C++ 程序生成的输出文件名为 `YellowCircle.ppm` 和 `YellowBox.ppm`。PPM 文件需要一个标头，必须保留该标头才能查看或转换图像。标头包含“魔数”（PPM 文件为 P3）、可能的注释行（注释行以 # 开头并以换行符结尾）、图像的宽度和高度以及最大颜色值。

![](img/0235a4ea835dc4575bd036e024a533b3_578_0.png)

图 10.3 ASCII PPM 图像文件。(a) YellowCircle.ppm；(b) YellowBox.ppm。

可以使用文本编辑器（如 TextEdit、Emacs 或 vi）将 PPM 文件视为 ASCII 文本文件。YellowBox.ppm 的一个非常小版本的标头信息和图像数据如图 10.4 所示。

图像文件的前五行保存标头数据。魔数 P3 将文件标识为 PPM 文件。注释行以 # 开头，在此示例中，注释提供了图像文件的名称。接下来的两个整数（此示例中为 8 和 8）提供图像的宽度和高度，下一个整数 255 定义最大颜色值。随后是图像数据。图像数据由一个 8×8 的像素值网格组成。第一个像素由三元组 255 0 0 表示，即红色。第四行第四列的像素值由三元组 255 255 0 表示，即黄色。

编写一个 C++ 解决方案，创建一个红色框内居中的黄色框 PPM 图像。使用上一节开发的 Pixel 类作为网格中元素的数据类型。

```
P3
#YellowBox.ppm
8
8
255
255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0
255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0
255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0
255 0 255 0 0 255 255 0 255 255 0 255 255 0 255 255 0 255 0 0 255 0 0
255 0 0 255 0 0 255 255 0 255 255 0 255 255 0 255 255 0 255 0 0 255 0 0
255 0 255 0 0 255 255 0 255 255 0 255 255 0 255 255 0 255 0 0 255 0 0
255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0
255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0 255 0 0
```

网格。图像创建后，可以使用可用的 PPM 文件查看器查看。我们将使用 ToyViewer 查看我们的图像。ToyViewer 可在 Internet 上免费下载。

我们解决方案的算法非常简单。我们将定义一个类型为 Pixel 的二维向量来表示网格。根据像素的位置，网格中的每个像素将被分配红色 (255 0 0) 或黄色 (255 255 0) 颜色。如果像素在“框内”，则将其分配黄色颜色值，否则将其分配红色颜色值。例如，当像素的行位置大于 (height*0.25) 且小于 (height*0.75)，并且像素的列位置大于 (width*0.25) 且小于 (width*0.75) 时，该像素可被视为在框内。我们解决方案的伪代码如下：

```
main: open output file
prompt user to input width and height of desired image
createImage()
writeImage()

createImage():
for i=0,h
for j=0,w
if(inside box) image[i][j] = yellow
else image[i][j] = red

writeImage():
writeHeader()
for i=0,h
for j=0,w
write image[i][j]
if(tenth value) write a new line

writeHeader():
write P3:
write "**filename
write w,h,maximum color value
```

伪代码中的步骤足够详细，可以转换为 C++。我们将使用 Xcode 构建我们的解决方案。

```
int main(int argc, const char * argv[])
{
//Declare objects.
int width, height;
string filename;
filename = "YellowBox.ppm";

//Build an image using 2D vector of Pixels
vector< vector< Pixel >> box;

cout << "enter width and height of image: ";
cin >> width >> height;
```

