
```cpp
stream >> x;
return x;
}

/**
 * Extracts the country and associated value from an input line.
 * @param line a line containing a country name, followed by a number
 * @param country the string for holding the country name
 * @param value the variable for holding the associated value
 * @return true if a line has been read, false at the end of the stream
 */
void read_line(string line, string& country, double& value)
{
    int i = 0; // Locate the start of the first digit
    while (!isdigit(line[i])) { i++; }
    int j = i - 1; // Locate the end of the preceding word
    while (isspace(line[j])) { j--; }

    country = line.substr(0, j + 1); // Extract the country name
    value = string_to_double(line.substr(i)); // Extract the number value
}

int main()
{
    ifstream in1;
    ifstream in2;
    in1.open("worldpop.txt"); // Open input files
    in2.open("worldarea.txt");

    ofstream out;
    out.open("world_pop_density.txt"); // Open output file
    out << fixed << setprecision(2);

    string line1;
    string line2;

    // Read lines from each file
    while (getline(in1, line1) && getline(in2, line2))
    {
        string country;
        double population;
        double area;

        // Split the lines into country and associated value
        read_line(line1, country, population);
        read_line(line2, country, area);

        // Compute and print the population density
        double density = 0;
        if (area != 0) // Protect against division by zero
        {
            density = population * 1.0 / area;
        }
        out << setw(40) << left << country
            << setw(15) << right << density << endl;
    }

    return 0;
}
```

### 工作示例 8.1 查找重复内容

本工作示例处理一个文件，以定位包含重复单词的行。

## 8.6 随机访问与二进制文件

在接下来的章节中，你将学习如何在文件中的任意位置读写数据，以及如何编辑图像文件。

### 8.6.1 随机访问

> 通过在执行读取或写入操作前移动文件指针，你可以访问随机访问文件中的任意位置。

到目前为止，你一次从文件中读取一个数据项，一次向文件写入一个数据项，没有向前或向后跳转。这种访问模式称为顺序访问。在许多应用中，我们希望访问文件中的特定数据项，而不必先读取所有前面的数据项。这种访问模式称为随机访问（见图 3）。随机访问与“随机”无关——该术语表示你可以读取并修改文件中任意位置存储的任何数据项。

只有文件流支持随机访问；连接键盘和终端的 cin 和 cout 流不支持。每个文件流有两个特殊位置：读取位置和写入位置（见图 4）。这两个位置决定了下一个字符被读取或写入的位置。

下面的函数调用将读取和写入位置移动到给定值，该值从流的开头开始计算。

```cpp
strm.seekg(position);
strm.seekp(position);
```

要确定读取和写入位置的当前值（从文件开头计算），请使用

```cpp
position = strm.tellg();
position = strm.tellp();
```

![](img/23fb3582e93ebc95909e1de029c3d388_399_0.png)

![](img/23fb3582e93ebc95909e1de029c3d388_399_1.png)

在正式晚宴上，食物按顺序上桌。而在自助餐中，你可以“随机访问”所有食物。

![](img/23fb3582e93ebc95909e1de029c3d388_400_0.png)

### 8.6.2 二进制文件

许多文件，尤其是包含图像和声音的文件，不是以文本形式存储信息，而是以二进制数存储。这些数字以字节序列表示，就像在计算机内存中一样。（每个字节是 0 到 255 之间的一个值。）在二进制格式中，浮点数总是占用 8 个字节。我们将通过图像的二进制文件格式来研究随机访问。

我们必须介绍一些关于二进制文件的技术问题。要以读和写的方式打开二进制文件，请使用以下命令：

```cpp
fstream strm;
strm.open(filename, ios::in | ios::out | ios::binary);
```

你可以通过以下调用读取一个字节

```cpp
int input = strm.get();
```

该调用返回 0 到 255 之间的一个值。要读取整数，请读取四个字节 b₀、b₁、b₂、b₃，并将它们组合为 b₀ + b₁ · 256 + b₂ · 256² + b₃ · 256³。我们将为此任务提供一个辅助函数。

>> 运算符不能用于从二进制文件中读取数字。

### 8.6.3 处理图像文件

在本节中，你将学习如何编写一个用于编辑 BMP 格式图像文件的程序。与更常见的 GIF、PNG 和 JPEG 格式不同，BMP 格式非常简单，因为它不使用数据压缩。因此，BMP 文件体积巨大，你很少会在实际使用中见到它们。不过，图像编辑器可以将任何图像转换为 BMP 格式。

BMP 格式有不同版本；我们只介绍最简单也最常见的一种，有时称为 24 位真彩色格式。在这种格式中，每个像素由三个字节表示，分别对应蓝、绿、红值。例如，青色（蓝色和绿色的混合色）是 255 255 0，红色是 0 0 255，中灰色是 128 128 128。

BMP 文件以包含各种信息的文件头开始。我们只需要以下各项：

| 位置 | 项目 |
|---:|---|
| 2 | 此文件的字节大小 |
| 10 | 图像数据的起始位置 |
| 18 | 图像的像素宽度 |
| 22 | 图像的像素高度 |

要试用该程序，请取一张你喜爱的图像，使用图像编辑器将其转换为 BMP 格式（或使用本书代码文件中的 queen-mary.bmp），然后运行该程序，并在图像编辑器中查看转换后的文件。练习 P8.21 和 P8.22 要求你实现更有趣的效果。

**ch08/imagemod.cpp**

```cpp
1  #include <iostream>
2  #include <fstream>
3  #include <cstdlib>
4
5  using namespace std;
6
7  /**
8     Processes a pixel by forming the negative.
9     @param blue the blue value of the pixel
10    @param green the green value of the pixel
11    @param red the red value of the pixel
12  */
13 void process(int& blue, int& green, int& red)
14 {
15    blue = 255 - blue;
16    green = 255 - green;
17    red = 255 - red;
18 }
19
20 /**
21    Gets an integer from a binary stream.
22    @param stream the stream
23    @param offset the offset at which to read the integer
24    @return the integer starting at the given offset
25 */
26 int get_int(fstream& stream, int offset)
27 {
28    stream.seekg(offset);
29    int result = 0;
30    int base = 1;
31    for (int i = 0; i < 4; i++)
32    {
33       result = result + stream.get() * base;
34       base = base * 256;
35    }
36    return result;
37 }
38
39 int main()
40 {
41    cout << "Please enter the file name: ";
42    string filename;
43    cin >> filename;
44
45    fstream stream;
46    // Open as a binary file
47    stream.open(filename.c_str(), ios::in | ios::out | ios::binary);
48
49    int file_size = get_int(stream, 2); // Get the image dimensions
50    int start = get_int(stream, 10);
51    int width = get_int(stream, 18);
52    int height = get_int(stream, 22);
// Scan lines must occupy multiples of four bytes
int scanline_size = width * 3;
int padding = 0;
if (scanline_size % 4 != 0)
{
    padding = 4 - scanline_size % 4;
}

if (file_size != start + (scanline_size + padding) * height)
{
    cout << "Not a 24-bit true color image file." << endl;
    return 1;
}

stream.seekg(start); // Go to the start of the pixels

for (int i = 0; i < height; i++) // For each scan line
{
    for (int j = 0; j < width; j++) // For each pixel
    {
        int pos = stream.tellg(); // Go to the start of the pixel

        int blue = stream.get(); // Read the pixel
        int green = stream.get();
        int red = stream.get();

        process(blue, green, red); // Process the pixel

        stream.seekg(pos); // Go back to the start of the pixel

        stream.put(blue); // Write the pixel
        stream.put(green);
        stream.put(red);
    }

    stream.seekg(padding, ios::cur); // Skip the padding
}

return 0;
}
```

## 自测

- 25. 用通俗的语言说明，以下代码段做了什么？

    ```cpp
    strm.seekg(0);
    strm.put(0);
    ```

- 26. 你如何修改 `imagemod.cpp` 程序，以交换每个像素的绿色和蓝色值，从而产生迷幻效果？

- 27. 如果你对同一个图像文件运行两次 `imagemod.cpp` 程序，会发生什么？

- 28. 我们能否仅使用顺序访问来实现图像修改程序？如果不能，为什么？

- 29. 假设一个 BMP 文件以 BMP 格式存储一张 100 x 100 像素的图像，图像数据从偏移量 64 开始。该文件的总大小是多少？

**动手实践** 现在你可以尝试本章末尾的练习：R8.12、R8.13、P8.21。

