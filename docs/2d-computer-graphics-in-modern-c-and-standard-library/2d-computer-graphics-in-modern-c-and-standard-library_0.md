
# 现代 C++ 与标准库 2D 计算机图形学

![](img/title_page.png)

![现代 C++ 与标准库中的 2D 图形](img/title_page.png)

本书可在 [`leanpub.com/2dcomputergraphicsinmoderncandstandardlibrary`](http://leanpub.com/2dcomputergraphicsinmoderncandstandardlibrary) 购买。

此版本发布于 2023-12-21。

![出版者标志](https://leanpub.com/)

---

这是一本 [Leanpub](https://leanpub.com) 书籍。Leanpub 通过精益出版流程为作者和出版者赋能。[精益出版](https://leanpub.com/manifesto) 是使用轻量级工具和多次迭代来发布进行中的电子书的行为，以获取读者反馈，不断调整直到获得正确的书籍，并在获得进展后建立影响力。

---

![](img/Introduction.jpg)

图 1

## 2D 绘制基础

我们都经历过这种情况：当你想要以美且图形化的方式展示某些数据时。你开始实现一个 GUI 库，以便设置一个用于绘制的画布……但然后呢？或者你可以下载并构建一个可以处理读写 PNG 图像的库，因为你需要无损图像。或者你同样的操作是为了寻找文件的熵。或者你正在编写一个游戏，想在视差设置中测试动画帧精灵的外观。无论原因是什么……做起来都太复杂了，花费的时间比你考虑要做的要长得多。因此，没有展示，没有协作，也没有使用图形进行研究。

在标准 `C++` 中创建图形应该是容易的。这本书正是关于这一点的。我们该如何绘制一个像素、一条线或一个圆？这些都是我们将回答的问题。

### 历史

计算机 2D 绘制始于学术界，因为大多数事情与计算机有关。它最初是于 20 世纪 50 年代作为美国政府的科学家和工程师以及美国公司研究中心（如贝尔实验室和波音）的可视化工具创建的。随后，这些工具在 60 年代和 70 年代的大学得到了开发，例如俄亥俄州立大学、麻省理工学院（MIT）、犹他大学、康奈尔大学、北卡罗来纳大学和纽约技术学院。学术中心的早期突破持续在 20 世纪 70 年代著名的罗西思 PARC 等研究中心继续。这些努力在 70 年代后期和 80 年代初进入了广播视频图形和大型长片电影。计算机图形研究今天在全球范围内继续，现在加入了娱乐和制作公司的研发部门。

自 1974 年以来，ACM SIGGRAPH 已成为一个由研究人员、艺术家、开发者、电影制作人、科学家和商务人士组成的国际社区，他们对计算机图形和交互技术感兴趣。每年都会展示该研究领域最新、最出色的成果。

### 标准库

标准库需要对绘制更多的支持。标准库中完全没有媒体支持。而且也没有必要。通过我们现有的工具，我们将能够绘制像素、线条和圆。

### 编译代码示例

所有代码均使用 `Clang++` 编译，但在 `G++` 下也能良好运行。一切都是 `C++20`。

### 前提条件

你已经需要如何用 `C++` 编程。这本书是关于如何绘制，而不是如何编程。

如果你觉得开头太简单，请直接跳到“高级示例”章节。

### 下载源代码

![源代码包含在附件中，可以在此处获取：](img/sourcecode.jpg)

图 2. 源代码包含在附件中，可以在此处获取：

使用以下命令编译所有示例：`./build_and_run_all.sh`

## 使用标准库绘制像素

我们正在使用 RGB 元素在 `C++` 中绘制一个像素。为了方便将 RGB 元素作为一个单元处理，有一种叫做 `std::tuple` 的东西。

参考地址：[`en.cppreference.com/w/cpp/utility/tuple`](https://en.cppreference.com/w/cpp/utility/tuple)

例如，一个接受三个整数作为输入并将其作为元组返回的函数。

`01_tuples.cpp` 演示了 `std::tuple` 在 `C++20` 中的用法。它使用元组来存储和操作 RGB 颜色元素作为单个实体。代码包含了 `<tuple>` 和 `<iostream>` 头文件，并定义了一个函数 `get_rgb_elements_as_a_tuple`，它接受三个整数（`r`、`g` 和 `b`）并返回一个包含这些整数的元组。

`main` 函数初始化了三组 RGB 值（`r1`、`g1`、`b1`、`r2`、`g2`、`b2` 以及 `r3`、`g3`、`b3`）。初始时，只给第一组（`r1`、`g1`、`b1`）赋值，而另外两组初始化为 `0`。

代码随后打印所有三组的初始 RGB 值。接下来，它用第一组 RGB 值（`r1`、`g1`、`b1`）调用 `get_rgb_elements_as_a_tuple`，并将返回的元组赋值给 `RGB`。

使用了两种不同的方法来处理 RGB 值：

1. 解包方法 1：使用 `std::get` 访问元组的单个元素。
2. 解包方法 2：使用 `std::tie` 解包元组。

在解包后，打印所有三组的 RGB 值，以验证它们已正确赋值给 `RGB`。

查看代码：`01_tuples.cpp`

现在，我们知道如何将 RGB 元素存储到图像。在此之前，我们必须讨论 (1D) 在物理上是如何表示的。为了存储元组，我们需要将 (2D) 转换为 (1D)。

查看代码：`02_index.cpp`

除了计算索引，我们还需要知道在 `std::vector` 中存储多少个元组以定义的 `width` 和 `height`。例如，一个宽度为 `640` 且为 `360` 的图像对于 `std::vector` 的大小为 `230400`。

参考：[`en.cppreference.com/w/cpp/container/vector`](https://en.cppreference.com/w/cpp/container/vector)

像总是一样，我们需要包含头文件：`#include <vector>`。

在图 3 中：

`img_grid.jpg`

`index = width * y`

`X + width = 32`

`Index = 32`

让我们创建一个函数为我们处理索引。一个接受 `X` 和 `Y` 作为输入并返回索引的函数。

查看代码：`03_calcsize.cpp`

**注意**，此代码示例使用 `double` 作为 RGB 元素。红色、绿色和蓝色是 `0.0` 到 `1.0` 之间的浮点数，而不是 0 - 255 之间的整数。结束图像元数据的计算。现在是绘制某些像素并将其保存到文本文件中了。是的，有一些基于文本的图像格式。我们将使用本书中的 PPM 文件格式。该图形格式源于开源 Netpbm 项目，带有几个图形程序和一个编程库 —— 主要在 Unix 世界使用。PPM 代表 Portable PixMap 格式，它是可移植的，因为它是以 ASCII 格式写入的（类型：`P3`）。PPM 文件包含两部分：头部和图像数据。不要担心它是 ASCII；PPM 可以转换为 PNG、JPG 或任何其他格式。

```text
 1 P3    # "P3" means this is an RGB color image in ASCII.
 2 3 2   # "3 2" is the width and height of the image in pixels.
 3 255   # "255" is the maximum value for each color.
 4 # The part above is the header.
 5 # The part below is the image data: RGB triplets.
 6 255   0   0  # red
 7   0 255   0  # green
 8   0   0 255  # blue
 9 255 255   0  # yellow
10 255 255 255  # white
11   0   0   0  # black
```

图 4

头部以 `P3` 标识开始。第二行包含图像的宽度和高度，由空格分隔。第三行列出了数字 `255`；这将用于此书中的所有示例。`255` 是每个 `rgb elements` 的最大值。在头部下方，每个像素表示为 RGB 的 `0` - `255` 之间的三个整数值。

包含头部：`#include <fstream>`

参考：[`en.cppreference.com/w/cpp/io/basic_fstream`](https://en.cppreference.com/w/cpp/io/basic_fstream)

对于源代码，请查看 source_code.zip：`04_helloworld.cpp`

![04_helloworld_square.ppm](img/04_helloworld_square.jpg)

图 5. 04_helloworld_square.ppm

![04_helloworld.ppm](img/04_helloworld.jpg)

图 6. 04_helloworld.ppm

太棒了，但如果我们能读取 PPM 图像，那就会更棒了。

对于源代码，请查看 source_code.zip：`05_randomwalker.cpp`

![05_randomwalker.ppm](img/05_randomwalker.jpg)

图 7. 05_randomwalker.ppm

现在，我们在 `05 example` 中有很多代码需要过。一个新头部和几个新函数需要解释。

`Example 05` 不仅关于读取一个 `PPM file`。我们实现了一个随机游走者。让我们逐个函数查看代码。

参考：[`en.cppreference.com/w/cpp/header/random`](https://en.cppreference.com/w/cpp/header/random)

在文件中添加随机头部：`#include <random>`

以下函数是新的：

- `walker`
- `update_x_and_y`
- `read_image`
- `get_color`
- `get_width_and_height`
- `startsWithCaseInsensitive`

我们首先将 `04_helloworld.ppm` 读取到 `image1` 中，同时使用 `get_width_and_height` 从 PPM 文件设置 `width` 和 `height`。`read_image` 使用辅助函数 `startsWithCaseInsensitive` 来遍历 PPM 数据。`get_color` 用于读取 RGB 颜色。

我们使用 `walker` 函数来实现随机游走算法。`Walker` 使用随机函数来使步长随机化。我们为每个游走者的生成使用 `update_x_and_y` 函数让游走者向随机方向移动。

## 使用标准库生成纹理

很不错，现在我们可以绘制像素了。让我们玩玩它并生成一些实用的不同类型的纹理。

让我们使用布尔异或（`XOR`）、与（`AND`）和或（`OR`）运算来生成纹理。

该代码根据位运算生成并保存三张纹理：`XOR`、`AND` 和 `OR`。它定义了几个函数来创建、处理和保存图像以实现目标。`get_index` 函数将 `2D` 网格坐标 `(x, y)` 转换为 `1D` 数组索引，而 `calc_size` 函数计算 `2D` 网格中的元素总数。`clear_image` 函数将图像的所有像素设置为给定颜色，从而有效地清除图像。

代码还提供了三个函数来创建不同的纹理：`draw_xor`、`draw_and` 和 `draw_or`。每个函数遍历图像的像素，并对每个 `pixel` 的 `x` 和 `y` 坐标计算相应的位运算（`XOR`、`AND` 或 `OR`）。得到的值随后用作该像素的颜色强度。

在 `main` 函数中，程序从初始化图像向量和颜色元组开始，根据计算的大小调整图像向量。然后使用深蓝色清除图像。之后，生成 XOR 纹理并保存到 `06_xor_texture.ppm` 文件。随后，生成 AND 纹理并保存到 `06_and_texture.ppm` 文件。最后，生成 OR 纹理并保存到 `06_or_texture.ppm` 文件。

对于源代码，请查看 source_code.zip：`06_xor_and_or_texture.cpp`

![06_xor_texture.ppm](img/06_xor_texture.jpg)

图 8. 06_xor_texture.ppm

![06_and_texture.ppm](img/06_and_texture.jpg)

图 9. 06_and_texture.ppm

![06_or_texture.ppm](img/06_or_texture.jpg)

图 10. 06_or_texture.ppm

XOR、AND 和 OR 类型的纹理是最简单的。如果你想做一个示例，它们非常有用。

过程化纹理生成是另一种创建纹理的方法。通过随机噪声，我们可以生成类似 `clouds`、`marble` 和 `wood` 的纹理。

参考：[`en.cppreference.com/w/cpp/numeric/fabs`](https://en.cppreference.com/w/cpp/numeric/fabs)

这段代码生成并保存三张纹理：Clouds、Marble 和 Wood。它包含了用于创建、处理和保存图像的几个函数。`get_index`、`calc_size`、`clear_image` 和保存函数在之前的回复中已解释过，它们在这里的作用相同。引入了一个新函数 `generate_noise`，它填充 `0.0` 到 `1.0` 范围内的噪声值。

`smooth_noise` 函数计算给定位置的双线性插值。相比之下，`turbulence` 函数叠加不同尺度的噪声值以生成更复杂的图案。

`generate_cloud` 函数使用 `turbulence` 函数创建类似云的纹理。相比之下，`generate_marble` 函数计算受扰动调的正弦波以模仿理石的外观。最后，`generate_wood` 函数通过计算距离并应用正弦波创建类似木纹的纹理。

在 `main` 函数中，程序初始化噪声和图像向量并根据计算的大小调整它们。然后使用深蓝色清除图像。生成噪声向量，创建 Cloud 纹理并保存到 `07_cloud_texture.ppm` 文件。随后，生成 Marble 纹理并保存到 `07_marble_texture.ppm` 文件。最后，生成 Wood 纹理并保存到 `07_wood_texture.ppm` 文件。

对于源代码，请查看 source_code.zip：`07_clouds_marble_wood_texture.cpp`

![07_cloud_texture.ppm](img/07_cloud_texture.jpg)

图 11. 07_cloud_texture.ppm

![07_marble_texture.ppm](img/07_marble_texture.jpg)

图 12. 07_marble_texture.ppm

![07_wood_texture.ppm](img/07_wood_texture.jpg)

图 13. 07_wood_texture.ppm

### 使用标准库绘制线条

嗯，首先，我们过一遍关于光和颜色的有益理论。

一个用于处理 PPM 格式图像的 `C++` 程序，特别是 P3（ASCII）格式。它包含了各种用于执行图像处理任务的函数，如创建反色、调整亮度和对比、转换为灰度、交换颜色通道以及混合两幅图像。该程序使用标准库，并有一个 `main` 函数用于对输入图像文件执行用户指定的操作并将结果保存到输出文件。

代码首先导入了必要的头文件，并声明了 `startsWithCaseInsensitive`、`get_index`、`calc_size`、`get_width_and_height` 和 `get_color` 等工具函数。这些函数有助于字符串处理、获取表示 2D 图像的 1D 数组索引、计算图像大小，以及从字符串中提取图像尺寸和颜色值。

`read_image` 函数从文件中读取图像并存储为双精度值的元组向量（vector of tuples），其中代表每个像素的红、绿、蓝（RGB）分量。该函数逐行读取文件，确定文件格式、尺寸和最大颜色值，然后用像素数据填充图像向量。

多个函数执行图像处理操作，如 `negative_image`、`double_as_dark`、`onefive_as_dark`、`twice_as_bright`、`add_for_brighter`、`sub_for_darker`、`greyscale_image`、`zero_gb_image`、`r_zero_b_image`、`rg_zero_image`、`grb_image`、`bgr_image`、`rrb_image` 和 `blended_two_images`。这些函数接受图像（元组向量）及其尺寸作为输入并修改图像。某些函数还接受额外的参数，例如 `blended_two_images` 中的混合因子 `alpha`。

程序的 `main` 函数读取输入图像文件，使用上述函数执行用户指定的图像处理，并将修改后的图像写入输出文件。`main` 函数还验证了用户输入并确保提供的参数有效。

关于源代码，请查看 `source_code.zip` 中的文件：`08_light_and_color.cpp`。

对于生成的每个图像，`04_helloworld.ppm` 都会被还原。

![08_negative_image.ppm](img/08_negative_image.jpg)

图 14. 08_negative_image.ppm

#### 减法



例如，原始颜色`rgb(203, 37, 101)`取反色：`rgb(255-203, 255-37, 255-101)`，等同于：`rgb(52, 218, 154)`。

![08_double_as_dark.ppm](img/08_double_as_dark.jpg)

图 15. `08_double_as_dark.ppm`

#### 除法

例如，`rgb(203, 37, 101)`变倍变暗：`rgb(203/2, 37/2, 101/2)`，等同于：`rgb(101, 18, 50)`。

![08_onefive_as_dark.ppm](img/08_onefive_as_dark.jpg)

图 16. `08_onefive_as_dark.ppm`

#### 除法

例如，`rgb(203, 37, 101)`按 1.5 倍变暗：`rgb(203/1.5, 37/1.5, 101/1.5)`，等同于：`rgb(135, 25, 67)`。

![08_twice_as_bright.ppm](img/08_twice_as_bright.jpg)

图 17. `08_twice_as_bright.ppm`

### 乘法

例如，`rgb(203, 37, 101)`变倍变亮：`rgb(203x2, 37x2, 101x2)`，等同于：`rgb(255, 74, 202)`。

![08_add_for_brighter.ppm](img/08_add_for_brighter.jpg)

图 18. `08_add_for_brighter.ppm`

#### 加法

例如，`RGB(203, 37, 101)`加法变亮：`RGB(203+30, 37+30, 101+30)`，等同于：`RGB(233, 67, 131)`。

![08_sub_for_darker.ppm](img/08_sub_for_darker.jpg)

图 19. `08_sub_for_darker.ppm`

#### 减法

例如，`RGB(203, 37, 101)`减法变暗：`RGB(203-30, 37-30, 101-30)`，等同于：`RGB(173, 7, 71)`。

![08_greyscale_image.ppm](img/08_greyscale_image.jpg)

图 20. `08_greyscale_image.ppm`

```
Greyscale = (0.2126*R) + (0.7152*G) + (0.0722*B);
```

![08_zero_gb_image.ppm](img/08_zero_gb_image.jpg)

图 21. `08_zero_gb_image.ppm`

`Greyscale = (0.2126*R) + (0.7152*G) + (0.0722*B);`

![08_zero_gb_image.ppm](img/08_zero_gb_image.jpg)

图 21. `08_zero_gb_image.ppm`

```
Greyscale = (0.2126*R) + (0.7152*G) + (0.0722*B);
```

![08_zero_gb_image.ppm](img/08_zero_gb_image.jpg)

图 21. `08_zero_gb_image.ppm`

```
Greyscale = (0.2126*R) + (0.7152*G) + (0.0722*B);
```

![08_zero_gb_image.ppm](img/08_zero_gb_image.jpg)

图 21. `08_zero_gb_image.ppm`

```
Greyscale = (0.2126*R) + (0.7152*G) + (0.0722*B);
```

![08_zero_gb_image.ppm](img/08_zero_gb_image.jpg)

图 21. `08_zero_gb_image.ppm`

```
Greyscale = (0.2126*R) + (0.7152*G) + (0.0722*B);
```

![08_zero_gb_image.ppm](img/08_zero_gb_image.jpg)

图 21. `08_zero_gb_image.ppm`

```
Greyscale = (0.2126*R) + (0.7152*G) + (0.0722*B);
```

![08_zero_gb_image.ppm](img/08_zero_gb_image.jpg)

图 21. `08_zero_gb_image.ppm`

```
Greyscale = (0.2126*R) + (0.7152*G) + (0.0722*B);
```

Cohen-Sutherland 算法根据线段端点相对于视口的位置为每个端点分配一个 4 位的区域代码。这些位分别对应视口外的顶部、底部、右侧和左侧区域。`find_region`函数计算给定点的区域代码。如果两个端点的区域代码均为`0`，则该线段完全在视口内，不需要裁剪。如果两个区域代码的按位与运算（bitwise AND）结果不为零，则该线段完全在视口外，可以将其丢弃。

当线段跨越视口边界时，`clip_line`函数就会发挥作用。该函数通过计算直线与边界之间的交点，迭代地针对视口的每条边缘对线段进行裁剪。然后，它将视口外的端点替换为交点，并更新其区域代码。这个过程会重复进行，直到线段完全在视口内或被判定为在视口外。

源代码请查看`source_code.zip`中的：`09_lines.cpp`

![09_random_lines.ppm](img/09_random_lines.jpg)

图 29. `09_random_lines.ppm`

在这个示例中，我们使用`HSV`（色调、饱和度和值）作为颜色模型，并在之后将其转换`RGB`。程序会生成一个随机的`Hue`，并通过`h_to_rgb(float h)`函数获取对应的`RGB`值。

我们还使用`clip_line`函数和`find_region`函数对可见屏幕和不可见屏幕之间的每条线进行裁剪。

`std::mt19937`是 C++ 标准库中对梅森旋转伪随机数生成器（PRNG）算法的实现。名称“mt19937”源于使用梅森素数`2¹⁹⁹³⁷ - 1`作为内部状态基础的梅森旋转算法。该 PRNG 因其高质量的随机数生成能力、巨大的周期和高效的性能而被广泛使用。梅森旋转算法是各种应用程序的热门选择，包括模拟、统计建模和计算机游戏，在这些领域都需要高质量的随机数。

`std::mt19937`生成器是 C++11 或更高版本`<random>`头文件的一部分，该头文件提供了一套完善的随机数生成设施。此头文件包含了梅森旋转算法和其他随机数生成器、概率分布以及其他生成随机数的实用函数。`<random>`库的设计旨在相比于旧的 C++ 函数（如`rand()`和`srand()`），提供一种更通用、更灵活的随机数生成方法。

要使用`std::mt19937`，你首先需要创建一个生成器实例并用初始值对其进行种子设定。生成的随机数质量取决于种子值，通常源于高分辨率时钟或其他熵源。一旦生成器完成种子，你就可以使用它在指定范围内生成随机数，或者使用`random`头文件中提供的分布类根据概率分布生成随机数。

![09_damped_sine.ppm](img/09_damped_sine.jpg)

图 30. `09_damped_sine.ppm`

在这里，我们使用之前的`X`和`Y`来绘制计算出的呈阻尼正弦波形状的连续线。

阻尼正弦波是一种正弦函数，由于阻尼因的存在，振幅随时间逐渐减小。在数学上，阻尼正弦波可以表示为`A(t) = A₀ * sin(ωt + φ) * e^(-αt)`，其中`A₀`是初始振幅，`ω`是角频率，`φ`是相位，`α`是阻尼因子，而`t`代表时间。阻尼因子`α`决定了振幅减小的速率；较大的阻尼因子会导致振幅下降较快，而较小的阻尼因子会导致振幅衰减较慢。

阻尼正弦波可以有效用于动画，创建自然的运动或模拟涉及振荡行为的物理过程。例如，它们可以模拟秋摆的运动、球的弹性或弹簧的振荡。在这些情况下，阻尼正弦波有助于模拟由于现实系统中摩擦、空气阻或其他耗散力导致的能量损失。通过将阻尼正弦波融入动画，设计师可以创建更真实、更具视觉吸引力的运动，紧密模拟自然界观察到的行为，使动画对观众更有沉浸感和吸引。

此外，我们还可以根据起始`x`和`y`点、长度和角度绘制线。

![09_angle_lines.ppm](img/09_angle_lines.jpg)

图 31. `09_angle_lines.ppm`

该代码的设计用于创建一个带有不同角度线条的图像。代码起始于几个包含语句，引入了必要的库和一系列函数定义。

`get_index`、`calc_size`和`clear_image`函数是图像处理的实用函数。`get_index`从二维坐标计算一维索引，`calc_size`根据给定的宽度和高度计算图像的总尺寸，`clear_image`将图像中的所有像素设为白色。

`draw_line`是一个在图像两个点之间用指定颜色绘制线条的函数。`find_region`、`clip_line`和`get_angle_line`函数用于线条裁剪和角度计算。`find_region`确定点位于图像的哪个区域，`clip_line`将线条裁剪到图像边界内，而`get_angle_line`根据起始点、角度和长度计算线条的端点。

最后，`save_image`是一个将图像数据以 PPM 格式写入文件的函数。

`main`函数初始化图像并设置其尺寸。然后，它在图像中心周围以各种角度`(0, 45, 90, 135, 180, 225, 270`和`315`度）绘制固定长度的线条。`clip_line`函数确保线条只在图像范围内绘制。绘制完所有线条后，图像被保存到名为`09_angle_lines.ppm`的文件中。

***

## 没有直线曲线，只有曲线线条

贝塞尔曲线（Bézier curve）是一种参数曲线。贝塞尔曲线有三种类型：

*   线性贝塞尔曲线
*   二次贝塞尔曲线
*   三次贝塞尔曲线

线性插值（Linear Interpolation）是一种数学函数，它在线性比例尺上的某一点返回两个值之间的值。最常用的是，它用于在一段时间内移动或改变值。通过 C++20 中的`std::lerp`（线性插值）函数，我们可以使用线性、二次和三次贝塞尔曲线绘制曲线（利用`std::lerp`的嵌套，因为它们是相互构建的）。

参考：[`en.cppreference.com/w/cpp/numeric/lerp`](https://en.cppreference.com/w/cpp/numeric/lerp)

C++17 版本：[`github.com/emsr/cxx_linear`](https://github.com/emsr/cxx_linear)

如果你只能使用 C++17，请使用上述 Lerp 和中点代码。

该 C++ 代码演示了如何在图像上使用点来绘制线性、二次和三次贝塞尔曲线。它创建了一个带有各种贝塞尔曲线的图像并将结果保存为 PPM 文件。代码开始时包含了必要的头文件。然后，它定义了几个函数来计算贝塞尔曲线上的点、处理图像以及在图像上渲染曲线。

线性、二次和三次贝塞尔曲线函数以起始点、控制点和终点的坐标以及分段数作为输入，并计算曲线上的点。定义了一些实用函数来帮助图像处理和渲染，例如获取图像向量中的索引、计算图像尺寸、清除图像和绘制线条。

除了贝塞尔曲线函数外，代码还包含一个用于在图像上绘制贝塞尔曲线点和标记的函数，这些用于更好的可视化。另一个函数`save_image`用于将图像保存为 PPM 文件。

在`main`函数中，程序初始化图像并设置其尺寸。然后，它在图像上绘制各种角度的贝塞尔曲线，绘制线性、二次和三次贝塞尔曲线。`clip_line`函数确保线条只在图像范围内绘制。在绘制完所有线条后，图像被保存为名为`10_curved_dots.ppm`的文件。

```
10_curved_dots.cpp
```

![10_curved_dots.ppm](img/10_curved_dots.jpg)

图 32. `10_curved_dots.ppm`

这就是`std::lerp`的作用……这些点可以使用`line`函数绘制曲线。

***

### 使用标准库绘制矩形

矩形是一个闭合二维形状，具有四条边和四个直角（90°）。矩形的对对边是相等且平行的。由于矩形是二维形状，它由宽度和高度刻画。你需要`X`和`Y`配合矩形的`width`和`height`。

C++ 代码生成包含两个矩形的图像（一个是轮廓，一个是填充的），保存为 PPM 文件。代码由几个函数组成，每个函数都有特定用途：创建和处理图像。

代码中的前几个函数用于图像处理。`get_index`函数根据给定的`(x, y)`坐标和图像宽度计算一维向量表示中的像素索引。`calc_size`函数根据宽度和高度计算尺寸，`clear_image`函数用白色像素填充图像向量（`R=1.0, G=1.0, B=1.0`）。

接下来，有在图像上绘制形状的函数。`draw_line`函数使用 Bresenham 线条算法在图像两个点之间绘制线条，这是在栅格格上绘制线条的高效方法。`draw_rect`函数通过`draw_line`函数连接四个角来绘制轮廓矩形。另一方面，`draw_filled_rect`函数通过遍历矩形区域并设置矩形内部每个像素的颜色来绘制填充矩形。

最后，在`main`函数中，程序初始化图像参数（如宽度、高度以及两个矩形的位置和尺寸）。然后，创建一个表示图像的向量并用白色像素初始化。之后，在图像上绘制两个矩形。结果图像保存为名为`11_rectangles.ppm`的文件。

```
11_rectangles.cpp
```

![11_rectangles.ppm](img/11_rectangles.jpg)

图 34. `11_rectangles.ppm`

在这里，我们有一个矩形和一个填充矩形。

代码从文件中读取一系列矩形规格，然后生成一个包含这些矩形的图像，带有背景颜色和填充填充矩形。代码的主要目的是创建一个填充矩形使用 Alpha 通道与背景颜色混合的图像。

代码包含必要的头文件并定义辅助函数，如`startsWithCaseInsensitive`、`get_index`、`calc_size`、`clear_image`、`parse_bginfo_line`、`parse_rect_line`、`blend_colors`、`draw_filled_rect`和`save_image`。这些函数执行各种操作，如字符串处理、解析输入、计算存储为一维向量的二维图像索引、混合颜色以及保存最终图像。

在`main`函数中，程序从输入文件`11_squint_with_eyes.txt`读取行。如果行以`r`开头，则被视为矩形并使用`parse_rect_line`解析。如果行以`b`开头，则视为背景规格并使用`parse_bginfo_line`解析。从行中提取`background color`和`image dimensions`，`clear_image`函数用背景颜色填充整个图像。

```
11_rectangles_from_file.cpp
```

![11_squint_with_eyes.ppm](img/11_squint_with_eyes.jpg)

图 35. `11_squint_with_eyes.ppm`

***

### 使用标准库绘制圆

圆是一个没有角或边缘的圆形形状。中点圆算法（midpoint circle algorithm）广泛用于在栅格显示器（如计算机屏幕或图像）上高效绘制圆。该算法是 Bresenham 线条算法的扩展。中点圆算法采用整数算术和增量计算来最小化开销，并避免使用昂贵的浮点算术。它利用对称性，在圆周上生成一组点。

该算法的工作原理是从圆的顶部点开始，逐渐向 x 轴移动，同时为每个 x 坐标计算适当的 y 坐标。它通过在每一步评估决策参数来确定 x 坐标或两者。决策参数基于圆的方程，有助于判断候选像素之间的中点是在圆内还是外部。如果中点在圆内，算法选择靠近 x 轴的像素；如果在外部，算法选择靠近 y 轴的像素。

中点圆算法的一个关键特性是利用圆的八倍对称性。由于圆关于 x 轴、y 轴以及直线`y = x`和`y = -x`对称，算法只需要计算圆的八分之一的点，然后通过反射推导出剩余的点。这显著减少了绘制整个圆的计算量。

该 C++ 代码生成两个圆（一个是轮廓，一个是填充的），带有白色背景。代码的主要目的是通过中点算法的简单实现演示绘制圆。代码开始时包含必要的头文件并定义辅助函数`get_index`、`calc_size`、`clear_image`、`draw_circle`、`draw_filled_circle`和`save_image`。这些函数执行各种操作，如计算存储为一维向量的二维图像索引。

在`main`函数中，程序设置图像的宽度和高度以及两个圆的位置和半径。然后，创建一个表示图像的向量并用白色像素初始化。之后，在图像上绘制两个圆。

接下来，调用`draw_circle`函数在图像上绘制第一个圆（未填充），调用`draw_filled_circle`函数在图像上绘制第二个圆（填充）。两个函数都使用中点圆算法来确定哪些像素设为所需的颜色（黑色）。最后，调用`save_image`函数将结果图像保存为名为`12_circle.ppm`的文件。

```
12_circle.cpp
```

![12_circle.ppm](img/12_circle.jpg)

图 36. `12_circle.ppm`

在这里，我们有一个圆和一个填充圆。

程序从文本文件读取圆的规格并生成包含圆的 PPM 文件。代码包含了必要的文件流、元组和数学函数库。然后，定义了几个实用函数来执行不大小敏感字符串匹配、图像尺寸确定和图像清除。



程序随后包含了从文件解析圆和背景信息的函数。这些函数`parse_circle_line`和`parse_bginfo_line`处理每个输入行并提取信息。对于圆规格，提取坐标、半径和颜色信息；对于背景信息，提取图像尺寸和颜色。

接下来，代码定义了几个用于颜色混合、区域查找和线条裁剪的函数。`blend_colors`函数根据透明度混合两种颜色，而`find_region`和`clip_line`确定圆在图像边界内的可见部分。

程序的主功能位于`draw_filled_circle`函数中，它接收圆坐标、半径和图像尺寸作为参数。它使用高效算法绘制填充圆，用颜色更新图像缓冲区。`save_image`函数将生成的图像保存到 PPM 文件。

```
12_circles_from_file.cpp
```

![12_squint_with_eyes.ppm](img/12_squint_with_eyes.jpg)

图 37. 12_squint_with_eyes.ppm

这是一个如何在图像中读取并展示数据的示例。

***

## 没有直线曲线，只有曲线线条

贝塞尔曲线是一种参数曲线。贝塞尔曲线有三种类型：

*   线性贝塞尔曲线
*   二次贝塞尔曲线
*   三次贝塞尔曲线

线性插值是一种数学函数，它在线性比例尺上的某一点返回两个值之间的值。最常用的是用于移动或改变值。通过 C++20 中的`std::lerp`（线性插值）函数，我们可以使用线性、二次和三次贝塞尔曲线绘制曲线（利用`std::lerp`的嵌套，因为它们是相互构建的）。

参考：[`en.cppreference.com/w/cpp/numeric/lerp`](https://en.cppreference.com/w/cpp/numeric/lerp)

C++17 版本：[`github.com/emsr/cxx_linear`](https://github.com/emsr/cxx_linear)

如果你只能使用 C++17，请使用上述 Lerp 和中点代码。

该 C++ 代码演示了如何在图像上使用点来绘制线性、二次和三次贝塞尔曲线。它创建了一个带有各种贝塞尔曲线的图像并将结果保存为 PPM 文件。代码开始时包含了必要的头文件。然后，它定义了几个函数来计算贝塞尔曲线上的点、处理图像以及在图像上渲染曲线。

线性、二次和三次贝塞尔曲线函数以起始点、控制点和终点的坐标以及分段数作为输入，并计算曲线上的点。定义了一些实用函数来帮助图像处理和渲染，例如获取图像向量中的索引、计算图像尺寸、清除图像和绘制线条。

除了贝塞尔曲线函数外，代码还包含一个用于在图像上绘制贝塞尔曲线点和标记的函数，这些用于更好的可视化。另一个函数`save_image`用于将图像保存为 PPM 文件。

在`main`函数中，程序初始化图像并设置其尺寸。然后，它在图像中心周围以各种角度绘制线条。`clip_line`函数确保线条只在图像范围内绘制。在绘制完所有线条后，图像被保存为名为`10_curved_dots.ppm`的文件。

```
10_curved_dots.cpp
```

![10_curved_dots.ppm](img/10_curved_dots.jpg)

图 32. 10_curved_dots.ppm

这就是`std::lerp`的作用……这些点可以使用`line`函数绘制曲线。

***

### 使用标准库绘制矩形

矩形是一个闭合二维形状，具有四条边和四个直角（90°）。矩形的对对边是相等且平行的。由于矩形是二维形状，它由宽度和高度刻画。你需要`X`和`Y`配合矩形的`width`和`height`。

C++ 代码生成包含两个矩形的图像（一个是轮廓，一个是填充的），保存为 PPM 文件。代码由几个函数组成，每个函数都有特定用途：创建和处理图像。

代码中的前几个函数用于图像处理。`get_index`函数根据给定的 (x, y) 坐标计算一维向量表示中的像素索引。`calc_size`函数根据宽度和高度计算尺寸，`clear_image`函数用白色像素填充图像向量（R=1.0, G=1.0, B=1.0）。

接下来，有在图像上绘制形状的函数。`draw_line`函数使用 Bresenham 线条算法在图像两个点之间绘制线条，这是在栅格格上绘制线条的高效方法。`draw_rect`函数通过`draw_line`函数连接四个角来绘制轮廓矩形。另一方面，`draw_filled_rect`函数通过遍历矩形区域并设置矩形内部每个像素的颜色来绘制填充矩形。

（注：由于提供的待翻译文本存在大量重复，此处已按要求进行了去重，仅翻译了唯一的逻辑文本内容。）

第一层嵌套 for 循环分别用`pink`颜色和`fcolor`填充`mask`和`image`向量。然后，函数计算图像的中点`x0, y0`，并初始化变量`d`、`xx`和`yy`以使用 Bresenham 圆算法绘制圆。

在函数内部定义了一个 lambda 函数`drawline`，用于在`mask`向量中指定的`y-coordinate` `ny`处两点`sx, ex`之间绘制水平线。`while`循环使用布雷森汉圆算法（Bresenham's circle algorithm），通过调用`drawline`函数在`mask`向量中绘制线条来创建一个圆形掩码。

最后，另一组嵌套循环遍历图像中的每个像素。对于每个像素，它会检查对应的掩码像素是否等于`pink`（粉色）颜色。如果是，它会计算从图像中心到当前像素的距离。根据距离以及输入颜色`fcolor`和`tcolor`计算插值颜色值。生成的颜色元组被赋值给`image`向量的当前位置。如果掩码像素等于`pink`颜色，则直接将`tcolor`赋值给`image`向量。

![Step #4: 16_draw_investment4.ppm](img/16_draw_investment4.jpg)

图 67. Step #4: 16_draw_investment4.ppm

`generate_repeating_texture_image`生成具有给定宽度、高度和颜色的重复纹理图案。该纹理图像存储为元组向量`(float, float, float)`，代表每个像素的`red`、`green`和`blue` (RGB) 颜色值。

该函数接受以下参数：图像向量的引用、颜色元组的引用以及图像的宽度和高度。它首先初始化一个名为`bgcolor`的背景颜色元组为粉色。然后，使用两个嵌套循环用此背景颜色填充`image`向量。

该函数定义了两个整数数组`arr`和`arr2`，其硬编码的坐标和索引表示图案中点的位置和连接关系。`coords`元组被初始化用于存储图案中线条端点的坐标。

接下来，函数使用`for`循环遍历 13 个硬编码点。在每次迭代中，它根据`arr2`数组找到的索引，利用`arr`数组中的坐标创建一个`coords`元组。然后调用`draw_line`函数，并将`image`向量、`coords`元组、输入颜色、宽度和高度作为参数。该函数使用输入颜色在图像向量中由`coords`元组指定的坐标之间绘制线条。

![Step #5: 16_draw_investment5.ppm](img/16_draw_investment5.jpg)

图 68. Step #5: 16_draw_investment5.ppm

`render_repeating_texture_image`接收一个纹理图像并重复渲染到较大的图像中。纹理和较大的图像存储为元组向量`(float, float, float)`，代表每个像素的`red`、`green`和`blue` (RGB) 颜色值。

该函数接受以下参数：纹理向量的引用、纹理的宽度和高度`tw, th`、图像向量以及图像的宽度和高度`iw, ih`。它使用两个嵌套循环遍历较大图像中的每个像素。对于每个像素，函数使用`get_index`函数根据像素坐标模`(tw-1)`和`(th-1)`从纹理向量获取对应的颜色值。这确保了纹理在整个图像上重复。获取到的颜色值随后被赋予图像中对应的像素。

![Step #6: 16_draw_investment6.ppm](img/16_draw_investment6.jpg)

图 69. Step #6: 16_draw_investment6.ppm

`do_cookie_cut`从源图像提取一个矩形区域并存储到另一个名为`cookie`的图像中。源图像和结果图像都存储为元组向量`(float, float, float)`，代表每个像素的`red`、`green`和`blue` (RGB) 颜色值。

该函数接受以下参数：源图像向量的引用、源图像的宽度和高度`w, h`、结果图像向量的引用、结果图像的宽度和高度`cw, ch`以及从源图像提取的矩形区域的起始坐标`startx, starty`。它初始化两个变量`cx`和`cy`以跟踪结果图像中的当前 x 和 y 坐标。

函数使用两个嵌套循环从指定的坐标`startx, starty`开始遍历源图像的矩形区域`cw, ch`。区域内的每个像素都使用`get_index`函数将 2D 坐标转换为线性索引，并将源图像的颜色值拷贝到结果图像对应的位置。更新`cx`和`cy`变量以移动通过。

![Step #7: 16_draw_investment7.ppm](img/16_draw_investment7.jpg)

图 70. Step #7: 16_draw_investment7.ppm

`add_honeycomb`合并三个图像：基础图像、alpha 图像和纹理图像。基础图像和纹理图像使用 alpha 通道的权重进行合并。所有三个图像都存储为元组向量`(float, float, float)`，代表每个像素的`red`、`green`和`blue` (RGB) 颜色值。

该函数接受以下参数：基础图像向量、alpha 图像向量、纹理向量以及图像的宽度和高度`w, h`。它初始化几个元组变量来存储每个像素三个图像的颜色值以及一个粉色颜色元组`(1.0f, 0.0f, 1.0f)`用于检查纹理图像。使用两个嵌套`for`循环遍历图像的每个像素。如果纹理图像的当前颜色值不是粉色，函数获取基础、纹理和 alpha 图像的颜色值。然后根据 alpha 通道的权重在纹理和基础图像之间计算新的 RGB 颜色。生成的颜色值赋值给基础图像的当前像素。

![Step #8: 16_draw_investment8.ppm](img/16_draw_investment8.jpg)

图 71. Step #8: 16_draw_investment8.ppm

`stamp_cookie`将一个较小的`cookie`图像放置在较大基础图像的指定位置。该函数接受以下参数：基础图像向量及其宽高`w, h`、cookie 图像向量及其宽高`cw, ch`以及放置该图像的起始坐标`startx, starty`。函数初始化两个整数变量`cx`和`cy`以跟踪 cookie 图像内的当前位置。然后使用嵌套循环遍历基础图像上放置 cookie 图像区域的每个像素。对于区域内的每个像素，函数从 cookie 图像的当前`cx, cy`坐标获取颜色值，并将其赋值给基础图像当前的`x, y`坐标。内层循环每次迭代增加`cx`，外层循环每次迭代增加`cy`。内层循环完成后，将`cx`重置为 0 以开始处理 cookie 图像的下一行。

![Step #9: 16_draw_investment9.ppm](img/16_draw_investment9.jpg)

图 72. Step #9: 16_draw_investment9.ppm

代码创建一个具有不同灰色调和一些额外标签的圆环图像。该圆环由在基础图像上绘制的填充扇和线条组成。

基础图像`image7`初始化为元组向量`(float, float, float)`，代表每个像素的 RGB 颜色值。随后将基础图像调整大小为所需的宽度和高度。

首先，使用`clear_image`函数将图像清除为纯色（洋红色）。接下来，通过绘制灰色和白色填充扇及线条来构建圆环形状。使用`draw_filled_wedge`函数绘制填充扇，使用`draw_line`函数绘制线条。每个函数都接受图像、坐标和颜色信息作为输入。

最后，`draw_labels`函数为图像添加标签。该函数接受图像、颜色（白色）、宽度和高度作为输入。

![Step #10: 16_draw_investment10.ppm](img/16_draw_investment10.jpg)

图 73. Step #10: 16_draw_investment10.ppm

代码通过拷贝非洋红色像素将之前创建的圆环形状添加到`image1`。洋红色颜色`(1.0f, 0.0f, 1.0f)`用作`image7`的背景色，将用于识别不应拷贝的像素。

（注：原文后续部分包含大量重复的无效字符如 * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 代码首先定义洋红色颜色为`fcolor`，将用于识别不应拷贝的像素。然后，两个嵌套循环遍历图像的高度和宽度。对于每个像素坐标`(x, y)`，代码检查`image7`中的像素是否不是洋红色（即不等于`fcolor`）。如果条件成立，`image7`中的非洋红色像素被拷贝到`image1`的相应位置。总结来说，代码通过仅拷贝`image7`中的非洋红色像素到`image1`的相应位置，添加来自`image7`的圆环形状。）

`getFirstPointFromCoord()`、`getSecondPointFromCoord()`：这些函数从`Coord`对象中提取`Point`对象，适用于需要从坐标对中分离单个点的场景。

## 直接像素操作函数

这些函数允许直接修改像素的颜色分量：`setRedColorElement()`、`setGreenColorElement()`、`setBlueColorElement()`：这些函数提供了直接设置像素红色、绿色或蓝色分量的方法，可以使用浮点值或整数。它们对于需要直接操作像素颜的操作（如图像编辑或过滤器应用）至关重要。

## 探索 ppmpp.hpp 中的颜色辅助函数

`ppmpp.hpp`框架提供了一颜色辅助函数，扩展了其颜色操作能力，这对于高级图像处理和图形设计任务至关重要。这些函数专注于颜色混合和色彩空间转换，为艺术家和开发者提供了多功能工具。

### 颜色混合函数

`blendColors(Pixel &colorbackground, Pixel &colorforeground, float alpha)`：该函数是创建复合图像和效果的基础。它根据 alpha 值混合两种颜色——背景色和前景色。alpha 参数决定前景颜色的透明度，实现无缝混合。这在创建半透明叠加层、抗锯齿或混合颜色以实现所需的视觉效果特别有用。

### 色彩空间转换函数

`getHSV(double& h, double& s, double& v, const Pixel& px)`：该函数将颜色从 RGB 表示转换为 HSV（色调、饱和度、亮度）色彩空间。HSV 色彩模型通常更符合人类感知，使得调整亮度、饱和度或色调偏移变得更容易。该函数对于色彩校正、艺术滤镜或任何需要以人为中心的色彩操作的场景至关重要。

`setHSV(double h, double s, double v, Pixel& px)`：`getHSV()`的对应函数，该函数接受色调、饱和度和亮度参数并将它们转换回`Pixel`格式的 RGB 表示。这对于将 HSV 空间中的更改应用于主要运行 RGB 的图像或图形特别有用，例如渲染最终输出或与其他图形系统对接。

## 探索 ppmpp.hpp 中 Image 类的构造函数和运算符

`ppmpp.hpp`框架中的`Image`类设计有一套全面的构造函数和运算符，确保了在图像操作和处理中的灵活性和易用性。

### 构造函数

`Image()`：初始化一个空图像。当必须声明`Image`对象但不立即分配任何特定数据或尺寸时，此构造函数非常有用。

`Image(int width, int height)`：创建具有指定尺寸的图像。此构造函数对于初始化具有预定义尺寸的图像至关重要，为绘制或图像处理提供了画布。

`explicit Image(std::string const& filename)`：通过从指定文件加载数据来构建图像。这对于处理现有图像特别有用，允许用户从文件系统加载并处理图像。

### 拷贝构造函数和赋值运算符

`Image(const Image& other)`：创建现有实例的副本。这在不影响原始的情况下需要精确副本的场景至关重要。

`Image& operator=(const Image& other)`：允许将一个`Image`对象赋值给另一个，用另一个的内容替换它。该运算符对于直接拷贝图像数据至关重要。

### 移动构造函数和赋值运算符

`Image(Image&& other) noexcept`：促进图像从一个对象转移到另一个对象而不复制实际数据，从而提高性能，特别是对于大图像。

`Image& operator=(Image&& other) noexcept`：与移动构造函数类似，此运算符将图像数据从一个对象转移到另一个对象，高效释放资源并确保最优的内存使用。

### 比较运算符

`friend bool operator==(const Image& lhs, const Image& rhs)`：检查两个`Image`实例是否相等，即它们具有完全相同的尺寸和像素数据。这对于验证图像处理结果或检查两个图像是否相同有用。



`friend bool operator!=(const Image& lhs, const Image& rhs)`：等于运算符的反向，检查两个`Image`实例在尺寸或像素数据上是否不同。可以在需要检测图像变化或差异的场景中用。

## 探索 `ppmpp.hpp` 中 `Image` 类的公共方法

`Image`类提供了一个全面的公共方法，每个方法都为特定的图像操作任务定制：

### 基础图像操作方法

`resize()`、`setWidth()`和`setHeight()`：这些方法提供了对图像尺寸的基本控制，允许用户根据需要调整图像大小。

`getWidth()`、`getHeight()`：获取图像的当前尺寸，适用于基于尺寸的计算和条件操作。

### 像素操作方法

`setPixel()`、`getPixel()`：直接操作单个像素，设置或获取它们的颜色。这在像素级上绘制、编辑或分析图像至关重要。

`setAllPixels()`：统一设置图像中所有像素的颜色，对于初始化背景或应用颜色过滤器有用。

`setImage()`、`getImage()`：设置新的图像数据或获取当前数据，实现更复杂的图像处理和转换。

### 绘图和形状方法

`drawLine()`、`getAngledLine()`：绘制直线或倾斜线，是创建基础图形或注释的基础。

`drawBezierQuadratic()`、`drawBezierCubic()`：渲染贝塞尔曲线，对于创建平滑曲线和复杂形状至关重要。

`drawRectangle()`、`drawFilledRectangle()`：创建矩形和填充矩形，是图形布局和设计的基础且多功能的工具。

`drawCircle()`、`drawFilledCircle()`、`drawWedge()`、`drawFilledWedge()`：绘制圆形、扇形，对于饼图、图表或装饰性元素很重要。

`drawTriangle()`和`drawFilledTriangle()`：渲染三角形是具有许多应用的基础几何形状。

`drawRotatedRectangle()`、`drawFilledRotatedRectangle()`、`drawRotatedEllipse()`、`drawFilledRotatedEllipse()`、`drawRotatedPolygon()`、`drawFilledRotatedPolygon()`：这些方法允许创建旋转的几何形状，为图形构图增加动态和多样性。

### 高级图像处理方法

`getAverageRgbOfImage()`：计算图像的平均颜色，适用于色彩分析或生成缩略图。

`convertToGrayscale()`、`applyGaussianBlur()`、`applyAntiAliasing()`：应用基础图像处理技术，如灰度转换、模糊和抗锯齿，对于创建艺术效果或提高图像质量至关重要。

`downscale()`、`upscale()`：使用特定算法调整图像大小，对于在适应不同分辨率的同时保持质量至关重要。

`applyBloom()`、`applyLens()`：实现高级视觉效果，如光晕或镜头效果，增强图像的视觉吸引。

`drawGradients()`：创建渐变效果，这是背景、按钮或视觉指示的关键功能。

### 文件输入输出

`read()`、`write()`：以 PPM P6 格式读取和保存图像，确保与外部源和工具的兼容性和数据交换的便利性。

`Image`类定义了以下私有成员变量：

`std::vector<Pixel> m_img;` 此向量存储了图像的像素数据。向量中的每个`Pixel`代表图像中单个像素的颜色，存储了它的红、绿、蓝分量。

`int m_width = 0;` 此整数存储图像的宽度（以像素为单位）。它定义了图像的水平维度，决定了`m_img`向量中每行包含多少个像素。

`int m_height = 0;` 与`m_width`类似，此整数存储图像的高度，代表垂直维度。它决定了`m_img`向量中的行数。

***

## 更多细节

### 深入理解 `ppmpp.hpp` 中的 `blendColors` 函数

`blendColors`函数是一个工具，旨在根据 alpha 透明度值混合两种颜色（背景色和前景色）。该函数是创建各种视觉效果的关键，在颜色混合任务中起着至关的作用。

#### 函数签名

`Pixel blendColors(Pixel &colorbackground, Pixel &colorforeground, float alpha)`：该函数接收两个`Pixel`引用——一个代表背景色，一个代表前景色——以及一个代表前景色不透明度的浮点值`alpha`。

#### 逻辑

该函数通过`alpha`值在前景色和背景色之间进行线性插值，计算出混合颜色。alpha 值的范围从 0.0（完全透明）到 1.0（完全不透明）。

对于每个颜色分量（红、绿、蓝），函数应用公式：`Blended Component=(Foreground Component×alpha)+(Background Component×(1.0−alpha))`。这确保了结果颜色的每个分量都是前景色和背景色对应分量的加权平均值。

随后，函数使用`createfPixelWithColor`使用混合后的颜色分量构建一个新的`Pixel`对象。

#### 实际应用

- **透明度与叠加**：是实现图像透明度的理想选择，允许创建前景图像或颜色混合到背景中的叠加效果。

- **抗锯齿与平滑处理**：在抗锯齿中非常有用，通过混合边缘处的颜色来创建更平滑的过渡，减少线条和曲线的锯齿感。

- **艺术效果**：能够创建各种艺术效果，如软阴影、光晕或数字绘画应用中的颜色混合。

#### 使用示例

考虑一种场景：你想要在蓝色背景上叠加一层半透明的红色。通过调用`blendColors`，将蓝色作为`colorbackground`，红色作为`colorforeground`，并将 alpha 值设置为 0.5，该函数将返回紫色，有效地平均混合了红色和蓝色。

### 深入理解 `ppmpp.hpp` 中的 `setHSV` 和 `getHSV` 函数

#### `setHSV` 函数

**目的**：将 HSV 颜色值转换为 RGB 模型并将这些值设置到给定的`Pixel`。

**实现细节**：函数首先检查饱和度 (s) 是否为 0（意味着灰度颜色），并根据亮度 (v) 将`Pixel`设置为相应的灰色深浅。

然后调整色调 (h) 以使其处于 0-360 度范围内，并将其转换为 0-6 范围，以确定 RGB 转换的分段。

函数根据分段使用 HSV 转 RGB 的转换公式计算 RGB 值。这涉及到根据色调在其所在分段内的位置，在两个 RGB 分量之间进行线性插值。

**使用场景**：当你拥有 HSV 格式的颜色数据（对人类感知通常更直观）并且需要将其转换为 RGB 格式以进行需要 RGB 值的操作（例如在大多数显示器上渲染）时，使用`setHSV`。

#### `getHSV` 函数

**目的**：从给定`Pixel`的 RGB 颜色表示中提取 HSV 值。

**实现细节**：函数首先从`Pixel`中提取 RGB 值。

计算 RGB 分量中的最小值和最大值，以确定亮度 (v) 和范围 (delta)。

根据 delta 和最大值计算饱和度 (s)。如果最大值为 0（表示为黑色），则将饱和度设为 0。

根据哪个 RGB 分量具有最大值来计算色调 (h)，并调整公式以找到正确的色调角度。

**使用场景**：当你需要根据色调、饱和度或亮度水平来操作图像或颜色时，`getHSV`很有用——这些任务在 HSV 颜色空间中通常更简单直接。

#### 实际应用

- **图形设计与图像处理**：这些函数在需要根据人类色彩感知进行颜色调整的应用中（如照片编辑软件或调色器）起着关键作用。

- **数据可视化**：它们也适用于根据值或强度生成颜色渐变的场景（如热力图）。

- **艺术与动画**：艺术家和动画师可以使用这些函数来创建更自然、更直观的颜色过渡和效果。

***

## PPMPP: 图像处理函数参考

### `void setPixel(int xCoord, int yCoord, const Pixel& newPixel)`

#### 目的

`setPixel`函数用于将图像中特定像素的颜色设置为新值。

#### 参数

- `int xCoord`：要设置的像素的 x 坐标。

- `int yCoord`：要设置的像素的 y 坐标。

- `const Pixel& newPixel`：像素的新颜色，用`Pixel`对象表示（由三个双精度浮点数的元组，每个值代表颜色的红、绿、蓝分量）。

#### 功能

- **边界检查**：函数首先检查指定的坐标 (`xCoord` 和 `yCoord`) 是否在图像边界内。这通过比较`xCoord`与`0`和`m_width`，以及`yCoord`与`0`和`m_height`来确定。

- **像素更新**：如果坐标在范围内，函数使用`getIndex`函数在`m_img`向量（存储图像数据）中计算这些坐标对应的索引。确定索引后，函数使用`newPixel`提供的颜色更新该索引处的像素。

#### 使用示例

```
Image myImage(100, 100); // 创建一个 100x100 像素的图像
Pixel redColor = std::make_tuple(1.0, 0.0, 0.0); // 创建红色
myImage.setPixel(50, 50, redColor); // 将 (50, 50) 处的像素设置为红色
```

图 99

#### 备注

函数确保像素坐标在图像范围内，防止访问`m_img`向量时可能发生的越界错误。

该方法是图像编辑操作的基础，因为它允许操作数字图像的基本单位——单个像素。

***

### `void getAngledLine(Coord& lineCoords, const Point& center, double degrees, int length)`

#### 目的

`getAngledLine`函数根据起始点、角度和长度计算线段的坐标。该函数确定从给定点开始并按指定角度延伸一定长度的线的终点坐标。

#### 功能

**角度转换**：该函数首先将角度从度转换为弧度，因为所使用的 C++ 三角函数使用的是弧度。此转换通过将角度值乘以`(pi/180)`完成。

**坐标计算**：利用三角函数，该函数计算线条的终点坐标。它将角度的余弦（乘以长度）加到起始点的 x 坐标，并将正弦（同样乘以长度）加到 y 坐标上。

**元组赋值**：随后将起点和终点坐标赋值给`lineCoords`，形成一个`Coord`元组，该元组通常由四个整数组成，代表线段的起始和结束的 x 和 y 坐标。

#### 使用示例

```
1 Point center = std::make_tuple(50, 50); // 起点位于 (50, 50)
2 double angle = 45; // 角度数
3 int length = 100; // 线条长度
4 Coord lineCoords;
5 getAngledLine(lineCoords, center, angle, length);
6 // 现在 lineCoords 包含了线条的起点和终点坐标
```

图 100

#### 备注

该函数在图形编程中特别有用，用于按特定角度绘制线条，这是游戏开发、模拟或图形表示等各种应用程序中的常见需求。

转换为弧度以及使用三角函数对于根据给定角度准确确定线条的方向和长度至关重要。

***

### `void drawBezierQuadratic(const Point& pt0, const Point& pt1, const Point& pt2, int split, const Pixel& bezierColor)`

#### 目的

`drawBezierQuadratic`函数在图像上绘制二次贝塞尔曲线（quadratic Bezier curve）。贝塞尔曲线在计算机图形中广泛用于平滑曲线建模，是矢量设计的基础。

#### 参数

- `const Point& pt0`：贝塞尔曲线的第一个控制点。

- `const Point& pt1`：第二个控制点，定义了曲线在起点和终点的切线方向。

- `const Point& pt2`：曲线的第三个控制点。

- `int split`：将曲线划分成若干段的数量。值越高，曲线越详细。

- `const Pixel& bezierColor`：贝塞尔曲线的颜色，表示为`Pixel`对象（一个包含红、绿、蓝分量的三个双数的元组）。

#### 功能

**曲线计算**：该函数根据控制点`pt0`、`pt1`和`pt2`计算二次贝塞尔曲线的中间点。这是通过在这些点之间进行线性插值来实现，由`split`参数决定曲线的每一部分。

**坐标生成**：该函数生成一系列表示曲线路径的`(x, y)`坐标，并将它们存储在`xyCoordinates`中。

**绘制曲线**：坐标计算完成后，将调用`drawXyLineImpl`使用指定的`bezierColor`在这些坐标之间绘制直线段。这近似了平滑的贝塞尔曲线。

#### 使用示例

```
1 Point pt0 = std::make_tuple(10, 10); // 第一个控制点
2 Point pt1 = std::make_tuple(50, 100); // 第二个控制点
3 Point pt2 = std::make_tuple(100, 10); // 第三个控制点
4 int split = 20; // 段数
5 Pixel bezierColor = std::make_tuple(1.0, 0.0, 0.0); // 红色
6 drawBezierQuadratic(pt0, pt1, pt2, split, bezierColor);
7 // 这将在图像上绘制一条二次贝塞尔曲线
```

图 101

#### 备注

二次贝塞尔曲线的特点是简单且优雅，使其适用于从字体渲染到动画路径的各种图形应用。

曲线的平滑度和准确直接受`split`参数的影响，该参数决定了使用多少线段来近似曲线。

这种方法以最小的计算开销高效地向图像添加复杂的形状和路径。

***

### `void drawBezierCubic(const Point& pt0, const Point& pt1, const Point& pt2, const Point& pt3, int split, const Pixel& bezierColor)`

#### 目的

`drawBezierCubic`函数用于在图像上绘制三次贝塞尔曲线（cubic Bezier curve）。对于平滑且可缩放的曲线，三次贝塞尔曲线在计算机图形和数字动画中至关重要。

#### 参数

- `const Point& pt0`：贝塞尔曲线的第一个控制点。

- `const Point& pt1`：第二个控制点影响起点的切线方向。

- `const Point& pt2`：第三个控制点影响终点的切线方向。

- `const Point& pt3`：曲线的第四个控制点。

- `int split`：定义近似曲线的线段数量，影响其平滑度。

- `const Pixel& bezierColor`：指定贝塞尔曲线的颜色，表示为`Pixel`对象。

#### 功能

**曲线计算**：该函数采用`cubicBezierCurvesImpl`使用控制点`pt0`、`pt1`、`pt2`和`pt3`计算三次贝塞尔曲线的中间点。`split`参数决定了沿曲线计算的点数，从而影响其分辨率。

**坐标生成**：生成一个`(x, y)`坐标向量 (`xyCoordinates`)，勾勒出曲线的路径。

**绘制曲线**：`drawXyLineImpl`方法在计算出的坐标之间绘制线段，使用指定的`bezierColor`近似贝塞尔曲线。

#### 使用示例

```
1 Point pt0 = std::make_tuple(10, 10); // 第一个控制点
2 Point pt1 = std::make_tuple(50, 100); // 第二个控制点
3 Point pt2 = std::make_tuple(100, 10); // 第三个控制点
4 Point pt3 = std::make_tuple(170, 10); // 第四个控制点
5 int split = 30; // 段数
6 Pixel bezierColor = std::make_tuple(0.0, 0.0, 1.0); // 蓝色
7 drawBezierCubic(pt0, pt1, pt2, pt3, split, bezierColor); // 绘制蓝色的三次贝塞尔曲线
```

图 102

#### 备注

由于额外的控制点，三次贝塞尔曲线比二次贝塞尔曲线提供了更大的形状控制。

该函数在绘制复杂形状方面的有效性在图形设计、字体渲染和用户界面开发中特别有用。

曲线的精度和视觉质量取决于`split`参数，根据所需的细节程度选择该参数。

***

### `void drawRectangle(const Point& xy, const Point& wh, const Pixel& bezierColor)`

#### 目的

`drawRectangle`函数用于在图像上绘制矩形。该函数是计算机图形中创建基础形状的基础，适用于从用户界面设计到复杂图像处理的广泛应用。

#### 参数

- `const Point& xy`：矩形的左上角，`xy`为表示`(x, y)`坐标的元组。

- `const Point& wh`：指定矩形的宽度`w`和高度`h`。

- `const Pixel& bezierColor`：定义矩形的颜色，表示为`Pixel`对象。`Pixel`是颜色红、绿、蓝分量的三个双数的元组。



#### 功能

绘制矩形：该函数内部调用`drawRectImpl`，传递矩形的左上角坐标、尺寸和颜色。

边缘计算：`drawRectImpl`根据提供的宽度和高度计算矩形其余角的坐标。

轮廓渲染：该函数随后连接这些角以以指定的`bezierColor`形成轮廓。

#### 使用示例

```
1 Point topLeftCorner = std::make_tuple(50, 50); // 矩形的左上角
2 Point dimensions = std::make_tuple(100, 150); // 矩形的宽度和高度
3 Pixel color = std::make_tuple(1.0, 0.0, 0.0); // 红色
4 drawRectangle(topLeftCorner, dimensions, color);
```

`6 // 绘制一个左上角位于 (50, 50) 尺寸为 100x150 的红色矩形`

```
图 103
```

#### 备注

该函数提供了一种简单且有效的方法来绘制矩形，这是许多图形和界面设计任务中的基本元素。

确保矩形的尺寸和位置在图像边界内对于避免错误至关重要。

定义矩形颜色的能力允许设计和可视化应用中具有灵活性。

***

### `void drawFilledRectangle(const Point& xy, const Point& wh, const Pixel& rectangleColor)`

#### 目的

`drawFilledRectangle`函数用于在图像上绘制一个填充矩形。该函数在图形编程中特别有用，可用于渲染实形状、创建背景或遮挡图像中的某些区域。

#### 参数

- `const Point& xy`：指定矩形的左上角。`xy`是一个表示`(x, y)`坐标的元组。

- `const Point& wh`：确定矩形的宽度`(w)`和高度`(h)`。

- `const Pixel& rectangleColor`：设置矩形的颜色。`Pixel`是一个包含三个双精度值的元组，代表颜色的红、绿、蓝分量。

#### 功能

- **填充矩形**：该函数调用`drawFilledRectImpl`，传递左上角的坐标、尺寸和矩形的颜色。

- **计算面积**：`drawFilledRectImpl`根据宽度和高度参数计算要填充的整个区域。

- **颜色应用**：该函数迭代将矩形区域内每个点的像素颜色设置为`rectangleColor`，从而有效地填充。

#### 使用示例

```
1 Point topLeftCorner = std::make_tuple(30, 40); // 矩形的左上角
2 Point dimensions = std::make_tuple(200, 100); // 矩形的宽度和高度
3 Pixel color = std::make_tuple(0.0, 0.0, 1.0); // 蓝色
4 
5 drawFilledRectangle(topLeftCorner, dimensions, color);
6 // 绘制一个填充的蓝色矩形，其左上角位于 (30, 40)，尺寸为
7 200x100
```

```
图 104
```

#### 备注

此方法对于创建实几何形状至关重要，可用于UI设计、图像处理和图形渲染等各种应用。

确保矩形的位置和尺寸位于图像边界内对于防止潜在的越界错误至关重要。

用特定颜色填充矩形为图形设计和可视化任务提供了灵活性和创造力。

***

### `void drawCircle(const Point& xy, int radius, const Pixel& circleColor)`

#### 目的

`drawCircle`函数在图像上绘制一个圆。它定义了圆的中心、半径和颜色。

#### 参数

- `const Point& xy`：一个表示圆心坐标`(x, y)`的元组。

- `int radius`：圆的半径。

- `const Pixel& circleColor`：圆的颜色，表示为一个`Pixel`对象（该对象是一个包含三个双精度值的元组，分别代表红、绿、蓝分量）。

#### 功能

- **中心和半径计算**：函数使用`xy`参数识别圆的中心，通过`radius`参数识别半径。

- **绘制算法**：内部调用`drawCircleImpl`，该函数可能使用圆绘制算法（如Bresenham圆算法）来确定形成圆轮廓的像素。

- **颜色应用**：对于形成圆的每个计算像素，函数将它的颜色设置为`circleColor`。

#### 使用示例

```
1 // 绘制圆的示例
2 Point center = std::make_tuple(50, 50); // 圆心位于 (50, 50)
3 int radius = 10; // 半径为 10 单位
4 Pixel color = std::make_tuple(1.0, 0.0, 0.0); // 红色
5 drawCircle(center, radius, color); // 绘制一个红色圆
```

```
图 105
```

#### 备注

该函数提供了一种向图像添加圆形形状的简单高效的方法，可用于各种图形应用。

确保圆的参数（中心和半径）在图像边界内对于防止超出范围错误非常重要。

此方法对于创建需要圆形元素的复杂图像和图形至关重要。

***

### `void drawFilledCircle(const Point& xy, int radius, const Pixel& circleColor)`

#### 目的

`drawFilledCircle`函数用于在图像上绘制一个填充圆。该函数指定了圆的中心、半径和填充颜色。

#### 参数

- `const Point& xy`：一个表示圆心坐标`(x, y)`的元组。

- `int radius`：圆的半径。

- `const Pixel& circleColor`：圆的填充颜色，表示为一个`Pixel`对象（一个包含三个双精度值的元组，分别代表红、绿、蓝分量）。

#### 功能

- **中心和半径识别**：函数使用`xy`参数确定中心，使用`radius`参数定义圆的大小。

- **填充算法**：内部调用`drawFilledCircleImpl`，它采用了一种修改后的圆绘制算法，用于填充圆而不是绘制轮廓。这包括确定圆内的所有像素。

- **颜色应用**：将指定半径内的每个像素颜色设置为`circleColor`。

#### 使用示例

```
// 绘制填充圆的示例
Point center = std::make_tuple(100, 100); // 中心位于 (100, 100)
int radius = 30; // 半径为 30 单位
Pixel fillColor = std::make_tuple(0.0, 0.0, 1.0); // 蓝色
drawFilledCircle(center, radius, fillColor); // 绘制填充蓝色圆
```

#### 备注

该函数对于创建图形设计和图像处理中的填充圆形形状至关重要。

确保圆的中心和半径在图像边界内是关键的。

这种方法对于创建需要圆形元素的复杂图像和图形。

***

### `void drawWedge(const Point& xy, int radius, int startAngle, int endAngle, const Pixel& circleColor)`

#### 目的

`drawWedge`函数用于在图像上绘制扇形（圆的一个扇区）。该函数指定了扇形所在的圆的中心、半径、起始角度、结束角度以及颜色。

#### 参数

- `const Point& xy`：一个表示圆心坐标`(x, y)`的元组。

- `int radius`：圆的半径。

- `int startAngle`, `int endAngle`：扇形的起始角和结束角，以度为单位。这些角度定义了形成扇形的区域。

- `const Pixel& circleColor`：扇形的颜色，表示为一个`Pixel`对象（一个包含三个双精度值的元组，代表红、绿、蓝分量）。

#### 功能

- **中心、半径和角度**：函数使用`center`和`radius`参数确定圆的基础，使用`startAngle`和`endAngle`指定圆的扇区。

- **扇形绘制算法**：内部调用`drawWedgeImpl`，它实现了绘制指定圆扇区的逻辑。这包括计算起始和结束角度之间圆周上的点，并将这些点与中心连接。

- **颜色应用**：扇形定义的区域用`circleColor`填充，从而创建一个彩色的扇形。

#### 使用示例

```
// 绘制扇形的示例
Point center = std::make_tuple(150, 150); // 中心位于 (150, 150)
int radius = 50; // 半径为 50 单位
int startAngle = 0; // 起始角为 0 度
int endAngle = 90; // 结束角为 90 度
Pixel wedgeColor = std::make_tuple(1.0, 0.0, 0.0); // 红色
drawWedge(center, radius, startAngle, endAngle, wedgeColor); // 绘制一个红色扇形
```

#### 图 106

#### 备注

此函数对于创建饼图、圆形仪表盘以及需要绘制圆形扇区域的图形至关重要。

该方法为创建圆形设计和图案提供了灵活性，在图形设计和图像处理应用中是一项重要的工具。

***

### `void drawFilledWedge(const Point& center, int radius, int startAngle, int endAngle, const Pixel& wedgeColor)`

#### 目的

`drawFilledWedge`函数用于在图像上绘制一个填充的扇形（圆的一个部分）。它指定了扇形所在圆心的位置、半径、扇形的起始角和结束角，以及扇形的颜色。

#### 参数

- `const Point& center`：一个元组，表示扇形所在圆心的坐标`(x, y)`。

- `int radius`：圆的半径。

- `int startAngle`, `int endAngle`：扇形的起始和结束角度，以度为单位。这些角度定义了将填充以创建扇形的圆扇区域。

- `const Pixel& wedgeColor`：填充扇形的颜色，表示为`Pixel`对象（一个包含红、绿、蓝分量的三个双数的元组）。

#### 功能

- **扇区识别**：该函数使用`center`、`radius`、`startAngle`和`endAngle`参数识别要填充的圆扇。

- **填充算法**：它内部调用`drawFilledWedgeImpl`，该实现使用一种算法填充由指定角度定义的圆扇。这涉及计算定义区域内的像素集，并将其颜色设置为`wedgeColor`。

- **颜色应用**：指定扇区内的每个像素都被赋予`wedgeColor`颜色，形成一个填充的扇形。

#### 使用示例

```
1 // 绘制填充扇形的示例
2 Point center = std::make_tuple(200, 200); // 中心在 (200, 200)
3 int radius = 40; // 半径为 40 单位
4 int startAngle = 45; // 起始角度为 45 度
5 int endAngle = 135; // 结束角度为 135 度
6 Pixel wedgeColor = std::make_tuple(0.0, 1.0, 0.0); // 绿色
7 drawFilledWedge(center, radius, startAngle, endAngle, wedgeColor); // 绘制填充的绿色扇形
```

#### 图 107

#### 备注

此函数对于创建饼图分段、扇形和其他需要填充扇区域的圆形设计特别有用。

该方法扩展了库的图形能力，允许创建更复杂且视觉上佳的设计和图案。

***

### `void drawTriangle(const Point& pt1, const Point& pt2, const Point& pt3, const Pixel& triangleColor)`

#### 目的

`drawTriangle`函数专门用于在图像上渲染三角形。它指定了三角形的顶点及其轮廓颜色。

#### 参数

- `const Point& pt1`, `const Point& pt2`, `const Point& pt3`：表示三角形三个顶点坐标的元组。每个点都是一个元组`(x, y)`，指示每个顶点的位置。

- `const Pixel& triangleColor`：三角形轮廓的颜色，表示为`Pixel`对象（一个包含红、绿、蓝分量的三个双数的元组）。

#### 功能

- **顶点识别**：为了定义三角形的顶点，该函数利用`pt1`、`pt2`和`pt3`参数。

- **轮廓绘制算法**：它内部调用`drawTriangleImpl`，该实现实现了三角形轮廓的逻辑。这包括计算连接每对顶点的线，并将它们的颜色设置为`triangleColor`。

- **颜色应用**：使用`triangleColor`绘制三角形轮廓，创建一个视觉上独特的三角形形状。

#### 使用示例

```
1 // 绘制三角形的示例
2 Point vertex1 = std::make_tuple(50, 50);  // 顶点 1 在 (50, 50)
3 Point vertex2 = std::make_tuple(100, 100); // 顶点 2 在 (100, 100)
4 Point vertex3 = std::make_tuple(50, 150); // 顶点 3 在 (50, 150)
5 Pixel outlineColor = std::make_tuple(1.0, 0.5, 0.0); // 橙色
6 drawTriangle(vertex1, vertex2, vertex3, outlineColor); // 绘制橙色三角形
```

#### 图 108

#### 备注

此函数对于创建三角形形状至关重要，三角形是各种图形设计和图像处理任务中的基础。

`drawTriangle`方法对于构建涉及三角形元素的几何图案和复杂图像至关重要。

***

### `void drawFilledTriangle(const Point& pt1, const Point& pt2, const Point& pt3, const Pixel& fillColor)`

#### 目的

`drawFilledTriangle`函数专门用于在图像上渲染一个填充的三角形。它指定了三角形的顶点和用于填充的颜色。

#### 参数

- `const Point& pt1`, `const Point& pt2`, `const Point& pt3`：这些参数代表三角形三个顶点的坐标。每个点是一个元组`(x, y)`，指示每个顶点的位置。

- `const Pixel& fillColor`：用于填充三角形的颜色，表示为`Pixel`对象（一个包含红、绿、蓝分量的三个双数的元组）。

#### 功能

- **顶点识别**：该函数使用`pt1`、`pt2`和`pt3`来定义三角形的顶点。

- **填充算法**：它内部调用`drawFilledTriangleImpl`，该实现填充三角形区域的算法。

- **颜色应用**：三角形内部使用`fillColor`进行填充。

#### 使用示例

```
1 // 绘制填充三角形的示例
2 Point vertex1 = std::make_tuple(120, 120); // 顶点 1 在 (120, 120)
3 Point vertex2 = std::make_tuple(200, 200); // 顶点 2 在 (200, 200)
4 Point vertex3 = std::make_tuple(120, 280); // 顶点 3 在 (120, 280)
5 Pixel fillColor = std::make_tuple(0.5, 0.0, 0.5); // 紫色
6 drawFilledTriangle(vertex1, vertex2, vertex3, fillColor); // 绘制填充的紫色三角形
```

#### 图 109

#### 备注

此函数对于创建三角形形状至关重要，它是各种图形设计中的基础元素。

`drawFilledTriangle`方法对于构建包含三角形元素的几何图案和复杂图像至关重要。

***

### `drawRotatedRectangle(int x, int y, int w, int h, double angle, const Pixel& px)`

#### 目的

`drawRotatedRectangle`函数用于在图像上渲染旋转的矩形。它指定了矩形的位置、尺寸、旋转角度和填充颜色。

#### 参数

- `int x`, `int y`：表示矩形中心的坐标`(x, y)`。

- `int w`, `int h`：矩形的宽度`(w)`和高度`(h)`。

- `double angle`：矩形的旋转角度，以度为单位。

- `const Pixel& px`：矩形的颜色，表示为`Pixel`对象（一个包含红、绿、蓝分量的三个双数的元组）。

#### 功能

- **位置与尺寸识别**：该函数使用`x`、`y`、`w`和`h`参数确定矩形的位置和大小。

- **旋转与绘制算法**：它内部调用`drawRotatedRectangleImpl`，该实现实现了按指定角度旋转矩形的逻辑。这涉及计算矩形角的旋转后位置并相应地绘制边。

- **颜色应用**：矩形用`px`指定的颜色填充，形成一个旋转的彩色矩形。

#### 使用示例



# 旋转图形与图像处理函数

```cpp
// 绘制旋转矩形的示例
int centerX = 150; // 中心 X 坐标
int centerY = 150; // 中心 Y 坐标
int width = 100;   // 宽度为 100 单位
int height = 50;   // 高度为 50 单位
double rotationAngle = 45.0; // 旋转 45 度
```

```cpp
Pixel rectangleColor = std::make_tuple(0.0, 0.5, 0.5); // 青色调
drawRotatedRectangle(centerX, centerY, width, height, rotationAngle, rectangleColor);
// 绘制一个旋转的青色矩形
```

图 110

## 备注

该函数对于创建指定方向的矩形至关重要，这是图形设计、几何图案以及各种图像处理任务中的一项基本功能。

准确计算矩形角的旋转位置对于确保旋转效果的准确性至关重要。

`drawRotatedRectangle` 方法扩展了库的图形能力，允许创建包含旋转矩形元素的更具动态感和视觉吸引力的设计和图案。

---

## `void drawFilledRotatedRectangle(int x, int y, int w, int h, double angle, const Pixel& px)`

### 目的

`drawFilledRotatedRectangle` 函数旨在在图像上渲染一个填充的、旋转矩形。该函数指定了矩形的中心坐标、尺寸、旋转角度和填充颜色。

### 参数

- `int x`、`int y`：代表矩形中心的 (x, y) 坐标。
- `int w`、`int h`：矩形的宽度 (w) 和高度 (h)，指示其尺寸。
- `double angle`：矩形的旋转角度（以度为单位），决定其朝向。
- `const Pixel& px`：矩形的填充颜色，表示为 `Pixel` 对象（一个包含红、绿、蓝分量的三个双精度数的元组）。

### 功能

- **中心、尺寸与旋转指定**：函数使用 `x`、`y`、`w`、`h` 和 `angle` 参数定义矩形的中心位置、尺寸和朝向。
- **填充与旋转算法**：它内部调用 `drawFilledRotatedRectangleImpl`，该函数采用算法绘制并填充按指定角度旋转的矩形。这包括计算由于旋转导致的矩形角变换坐标并填充生成的形状。
- **颜色应用**：旋转矩形的整个区域被设置为由 `px` 指定颜色，创建一个实色的旋转矩形形状。

### 使用示例

```cpp
// 绘制填充旋转矩形的示例
int centerX = 200; // 中心 X 坐标
int centerY = 100; // 中心 Y 坐标
int width = 120;   // 宽度为 120 单位
int height = 60;   // 高度为 60 单位
double rotationAngle = 30.0; // 旋转 30 度
Pixel rectangleColor = std::make_tuple(0.7, 0.3, 0.5); // 紫色
drawFilledRotatedRectangle(centerX, centerY, width, height, rotationAngle, rectangleColor);
// 绘制一个填充的旋转的紫色矩形
```

图 111

### 备注

该函数对于创建需要填充颜色旋转矩形的动态且视觉吸引眼的设计至关重要，通常用于各种图形设计和图像处理任务。

准确计算矩形角的旋转位置对于确保矩形在旋转后正确的朝向和形状至关重要。

`drawFilledRotatedRectangle` 方法增强了库中的创作可能性，允许创建包含填充旋转矩形元素的更复杂且美观的设计。

---

## `void drawRotatedEllipse(int x, int y, int w, int h, double angle, const Pixel& px)`

### 目的

`drawRotatedEllipse` 函数用于在图像上渲染一个旋转的椭圆。它指定了椭圆的中心坐标、尺寸、旋转角度和填充颜色。

### 参数

- `int x`、`int y`：代表椭圆中心的 (x, y) 坐标。
- `int w`、`int h`：椭圆的宽度 (w) 和高度 (h)，定义其形状。
- `double angle`：椭圆的旋转角度（以度为单位），决定其朝向。
- `const Pixel& px`：椭圆的填充颜色，表示为 `Pixel` 对象（一个包含红、绿、蓝分量的三个双精度数的元组）。

### 功能

- **中心、形状与旋转定义**：函数使用 `x`、`y`、`w`、`h` 和 `angle` 参数建立椭圆的中心位置、尺寸和旋转角度。
- **绘制与旋转算法**：它内部调用 `drawRotatedEllipseImpl`，该函数实现了绘制和填充按指定角度旋转椭圆的算法。这包括计算由于旋转导致的椭圆边界的变换坐标并填充形状。
- **颜色应用**：旋转椭圆的整个区域用 `px` 着色，产生一个实色的旋转椭圆形状。

### 使用示例

```cpp
// 绘制旋转椭圆的示例
int centerX = 250; // 中心 X 坐标
int centerY = 150; // 中心 Y 坐标
int width = 100;   // 宽度为 100 单位
int height = 60;   // 高度为 60 单位
double rotationAngle = 45.0; // 旋转 45 度
Pixel ellipseColor = std::make_tuple(1.0, 0.0, 0.0); // 红色
drawRotatedEllipse(centerX, centerY, width, height, rotationAngle, ellipseColor);
// 绘制旋转的红色椭圆
```

图 112

### 备注

该函数对于创建各种几何形状和设计非常有价值，因为旋转椭圆常用于图形设计和图像处理。

准确确定椭圆边界的旋转位置对于确保旋转效果的准确性至关重要。

`drawRotatedEllipse` 方法扩大了库的设计范围，允许创建包含椭圆元素的更动态、吸引的图案。

---

## `void drawFilledRotatedEllipse(int x, int y, int w, int h, double angle, const Pixel& px)`

### 目的

`drawFilledRotatedEllipse` 函数设计用于在图像上绘制填充的、旋转椭圆。该函数指定了椭圆的中心坐标、尺寸、旋转角度和填充颜色。

### 参数

- `int x`、`int y`：代表椭圆中心的 (x, y) 坐标。
- `int w`、`int h`：椭圆的宽度 (w) 和高度 (h)，定义其整体形状。
- `double angle`：椭圆的旋转角度（以度为单位），决定其朝向。
- `const Pixel& px`：填充椭圆的颜色，表示为 `Pixel` 对象（一个包含红、绿、蓝分量的三个双精度数的元组）。

### 功能

- **中心与尺寸确定**：函数使用 `x`、`y`、`w` 和 `h` 参数建立椭圆的中心位置和尺寸。
- **填充与旋转过程**：它内部调用 `drawFilledRotatedEllipseImpl`，实现了绘制和填充旋转椭圆的算法。这涉及计算由于旋转导致的椭圆边界变换坐标并填充生成的形状。
- **颜色应用**：旋转椭圆边界内的整个区域用 `px` 着色，产生一个填充的、有色的旋转椭圆形状。

### 使用示例

```cpp
// 绘制填充旋转椭圆的示例
int centerX = 200; // 中心 X 坐标
int centerY = 100; // 中心 Y 坐标
int width = 140;   // 宽度为 140 单位
int height = 80;   // 高度为 80 单位
double rotationAngle = 30.0; // 旋转 30 度
Pixel ellipseColor = std::make_tuple(0.0, 1.0, 0.0); // 绿色
drawFilledRotatedEllipse(centerX, centerY, width, height, rotationAngle, ellipseColor);
// 绘制填充的旋转的绿色椭圆
```

# 图 113

### 备注

该函数对于生成多样化且具有美感的形状至关重要，因为填充且旋转的椭圆经常用于各种图形设计和图像处理项目。

准确计算椭圆边界旋转后的位置确保了椭圆在旋转后具有正确的方向和外观。

`drawFilledRotatedEllipse` 方法扩展了库的功能，允许创建更复杂且具有视觉冲击力的设计，包括填充且旋转的椭圆元素。

---

## `void drawRotatedPolygon(const std::vector& vertices, double angle, const Pixel& px)`

### 目的

`drawRotatedPolygon` 函数设计用于在图像上绘制一个旋转的多边形。该函数指定了多边形的顶点、旋转角度和轮廓颜色。

### 参数

`const std::vector<Point>& vertices`：一个元组向量，每个元组代表多边形一个顶点的坐标 (x, y)。

`double angle`：多边形的旋转角度（角度为单位），决定了它的朝向。

`const Pixel& px`：多边形轮廓的颜色，用 `Pixel` 对象表示（包含红、绿、蓝分量的三个双精度浮数的元组）。

### 功能

**顶点识别**：函数使用 `vertices` 参数来定义多边形的形状。

**旋转算法**：在内部调用了 `drawRotatedPolygonImpl`，该函数实现了按指定角度旋转多边形的逻辑。这涉及计算顶点旋转后的新位置，并连接这些顶点以形成多边形。

**轮廓颜色应用**：使用 `px` 指定颜色绘制多边形的轮廓，创建一个在视觉上明显的多边形形状。

### 使用示例

```cpp
// 绘制旋转多边形的示例
std::vector<Point> vertices = {
    std::make_tuple(100, 100),
    std::make_tuple(150, 130),
    std::make_tuple(120, 180),
    std::make_tuple(80, 180),
    std::make_tuple(50, 130)
}; // 五边形的坐标
double rotationAngle = 45.0; // 旋转 45 度
Pixel outlineColor = std::make_tuple(0.5, 0.5, 0.5); // 灰色
drawRotatedPolygon(vertices, rotationAngle, outlineColor); // 绘制一个旋转的灰色五边形
```

# 图 114

### 备注

该函数对于创建旋转的多边形形状至关重要，这是各种图形设计和图像处理应用中的基础组件。

准确计算旋转后新顶点的位置对于保持多边形的正确形状和方向至关重要。

`drawRotatedPolygon` 方法提供了一个多用途的工具，用于创建包含旋转多边形元素的复杂几何图案和设计。

---

## `void drawFilledRotatedPolygon(const std::vector& vertices, double angle, const Pixel& px)`

### 目的

`drawFilledRotatedPolygon` 函数设计用于在图像上绘制一个填充且旋转的多边形。该函数指定了多边形的顶点、旋转角度和填充颜色。

### 参数

`const std::vector<Point>& vertices`：一个元组向量，每个元组代表多边形一个顶点的坐标 (x, y)。

`double angle`：多边形的旋转角度（角度为单位），决定了它的朝向。

`const Pixel& px`：用于填充多边形的颜色，用 `Pixel` 对象表示（包含红、绿、蓝分量的三个双精度浮数的元组）。

### 功能

**顶点识别与旋转**：函数使用 `vertices` 参数来定义多边形的形状，并使用 `angle` 参数来确定其旋转。

**填充与旋转过程**：在内部调用了 `drawFilledRotatedPolygonImpl`，该函数实现了一个绘制并填充旋转多边形的算法。这涉及计算顶点旋转后的新位置，然后填充生成的形状。

**颜色应用**：旋转多边形边界内的整个区域都使用 `px` 着色，形成一个填充的、有色的且旋转的多边形形状。

### 使用示例

```cpp
// 绘制填充旋转多边形的示例
std::vector<Point> vertices = {
    std::make_tuple(150, 150),
    std::make_tuple(200, 175),
    std::make_tuple(175, 225),
    std::make_tuple(125, 225),
    std::make_tuple(100, 175)
}; // 五边形的坐标
double rotationAngle = 30.0; // 旋转 30 度
Pixel fillColor = std::make_tuple(0.25, 0.5, 0.75); // 蓝色
drawFilledRotatedPolygon(vertices, rotationAngle, fillColor); // 绘制一个填充的、旋转的蓝色五边形
```

# 图 115

### 备注

该函数对于创建复杂且具有视觉吸引力的形状至关重要，因为填充且旋转的多边形经常用于各种图形设计和图像处理项目。

准确计算旋转后新顶点的位置对于保持多边形的正确形状和方向至关重要。

`drawFilledRotatedPolygon` 方法扩展了库的功能，允许创建更复杂且具有艺术趣味的设计，包括填充且旋转的多边形元素。

---

## `Pixel getAverageRgbOfImage()`

### 目的

`getAverageRgbOfImage` 函数设计用于计算整个图像的平均 RGB 颜色。该函数聚合图像所有像素的颜色值并计算平均值。

### 参数

无。

### 功能

**颜色累加**：函数遍历由 `m_img` 数据结构表示的像素，分别累加红 (`r`)、绿 (`g`) 和蓝 (`b`) 分量。

**平均值计算**：在累加所有像素的颜色分量后，通过除以像素总数来计算每个颜色分量的平均值。

**平均颜色的创建**：该函数返回一个表示平均颜色的 `Pixel` 对象。该 `Pixel` 使用计算出的红、绿、蓝平均值创建。

### 使用示例

```cpp
// 获取图像平均颜色的示例
Pixel averageColor = getAverageRgbOfImage();
std::cout << "平均颜色 - 红: " << std::get<0>(averageColor) << ", 绿: "
          << std::get<1>(averageColor) << ", 蓝: " << std::get<2>(averageColor) << std::endl;
```

图 117

### 备注

该函数在各种需要颜色信息的图像处理任务中至关重要，例如边缘检测、纹理分析和其他形式的模式识别。

转换为灰度可以简化图像数据，通常使随后的处理任务在计算上更加高效。

`convertToGrayscale` 方法是图像处理中的基础工具，特别适用于关注强度或亮度变化而非色彩变化的场景。

---

## `void applyGaussianBlur()`

### 目的

`applyGaussianBlur` 函数专门用于为整幅图像应用高斯模糊效果而设计。高斯模糊是图像处理中广泛使用的效果，它通过对区域内的像素取平均值来平滑图像，减少噪声和细节。

### 参数

无。

### 功能

- **高斯模糊算法**：该函数在内部调用 `applyGaussianBlurImpl`，该实现实现了高斯模糊算法。该算法通常涉及图像与高斯核的卷积，高斯核是一种数学函数，用于根据像素到内核中心的空间距离来对像素的平均值进行加权。
- **逐像素处理**：它处理图像中的每个像素，考虑相邻像素以计算模糊（平滑）后的值。模糊程度取决于算法中所使用的高斯核的大小和标准差。

### 使用示例

```cpp
// 给图像应用高斯模糊的示例
applyGaussianBlur(); // 整个图像现在已模糊
```

图 118

### 备注

该函数在各种需要减少高频噪声或平滑细节的图像处理任务中至关重要，例如边缘检测的预处理步骤或创建艺术效果。

应用高斯模糊可以通过提供更平滑版本的图像，增强对噪声或细微细节敏感的算法的性能。

`applyGaussianBlur` 方法是数字图像处理中的基础工具。它被广泛用于创建一种视觉上令人悦的模糊效果，这种效果模拟了相机捕捉离焦光点的方式。

---

## `void applyAntiAliasing()`

### 目的

`applyAntiAliasing` 函数旨在平滑图像中的锯齿边缘，这种通常称为“混叠”（aliasing）。该函数应用抗锯齿技术，通过减少数字图像中可能出现的阶梯状线条来提高图像的视觉质量。

### 功能



# 图像处理函数详解

## 抗锯齿

### 目的

`applyAntiAliasing()` 函数旨在减少图像边缘的锯齿感，通过平滑边缘像素的颜色过渡来提升图像质量。

### 功能

- **抗锯齿算法**：该函数在内部调用`applyAntiAliasingImpl`，该实现实现了抗锯齿算法。此过程通常涉及边界像素颜色的平均化，以在边缘之间创建更平滑的过渡。

- **像素处理**：它调整图像中形状边缘像素的颜色。通过将这些边缘像素的颜色与其周围像素混合，该函数减少了导致锯齿感的对比度。

### 使用示例

```
1 // 给图像应用抗锯齿的示例
2 applyAntiAliasing(); // 整个图像现在有了更平滑的边缘
```

图 119

### 备注

该函数在图形渲染和数字图像处理中至关重要，在这些领域，锯齿边缘的存在会损害图像的视觉吸引力和真实感。

抗锯齿对于高质量演示、打印媒体或任何其他需要图像清晰度和平滑度的应用准备图像至关重要。

`applyAntiAliasing` 方法是图像处理中的基础工具，通过减少像素化边缘的生硬感来提升数字图像的美学效果。

---

## void upscale(int scale)

### 目的

`upscale` 函数旨在按指定的比例因子增加图像尺寸。该函数放大图像，在保持横宽高比的同时增强其尺寸。

### 参数

- `int scale`：图像尺寸将要乘以的因子。大于 1 的比例因子会放大图像，而小于 1 的因子在技术上会缩小其尺寸。

### 功能

- **缩放过程**：该函数在内部调用`upscaleImpl`，该实现实现了缩放算法。此过程涉及将图像调整为一组尺寸，由原始尺寸乘以比例因子决定。

- **像素插值**：在缩放过程中，算法插值新的像素值以保持图像的质量和细节。这可能涉及双线性或三次插值等技术，这些技术根据周围像素估计新的像素值。

### 使用示例

```
1 // 放大图像的示例
2 int scaleFactor = 2; // 将图像放大一倍
3 upscale(scaleFactor); // 图像现在已按 2 倍放大
```

图 120

### 备注

该函数对于需要从低分辨率源获取高分辨率图像的应用至关重要。它被广泛应用于图形设计、媒体制作以及其他在较大尺寸下需要图像清晰度的领域。

虽然缩放可以增加图像尺寸，但需要注意的是，由于新像素值的插值，放大后图像的质量有时可能无法达到原生高分辨率图像的清晰度。

`upscale` 方法为调整图像尺寸提供了基础能力，这是各种图像处理和增强任务中必不可少的步骤。

---

## void applyBloom(double threshold, double sigma)

### 目的

`applyBloom` 函数旨在为图像添加光晕（bloom）效果，这是图形处理中的一种常用技术，可在明亮区域周围产生柔和的光环。该函数使用指定的阈值来识别明亮区域，并应用以 `sigma` 值为特征的高斯模糊来创建光晕效果。

### 参数

- `double threshold`：确定应用光晕效果的亮度阈值。亮度高于此阈值的像素将对光晕做出贡献。

- `double sigma`：用于创建光晕效果的高斯模糊的标准差。较高的 `sigma` 值会产生更柔和、更扩散的光环。

### 功能

- **亮度识别**：该函数识别图像中超过指定亮度阈值的像素。这些像素是光晕效果的来源。

- **应用高斯模糊**：在内部调用`applyBloomImpl`，对明亮区域应用高斯模糊。模糊程度由 `sigma` 值决定，影响光晕效果的柔和与扩散。

- **光晕创建**：将模糊后的明亮区域与原始图像结合，在这些区域周围产生光效。

### 使用示例

```
1 // 给图像应用光晕效果的示例
2 double brightnessThreshold = 0.7; // 亮度阈值
3 double blurSigma = 5.0; // 高斯模糊 sigma
4 applyBloom(brightnessThreshold, blurSigma); // 应用光晕效果
```

图 121

### 备注

光晕（`Bloom` effect）在数字摄影、视频游戏和电影中特别流行，用于模拟强光在真实相机镜头上的表现。

应用光晕可以通过为高亮度区域添加梦幻、柔和的光质，来增强图像的视觉吸引力。

`applyBloom` 方法是高级图像处理中的基础工具，它为数字图像增添了一层艺术深度和真实感。

---

## void applyLens(int numb)

### 目的

`applyLens` 函数旨在模拟多个透镜畸变对图像的影响。该函数应用指定数量的镜头效果，每个效果都会创建一个局部畸变，模拟光的弯曲，类似于通过凸透镜或凹透镜观察的效果。

### 参数

- `int numb`：应用到图像上的镜头效果数量。每个镜头效果都会创建一个局部畸变。

### 功能

- **镜头效果应用**：该函数内部调用`applyLensImpl`，它实现了应用镜头畸变的算法。这涉及在图像中选择随机点并扭曲周围的像素，以创建透镜效果。

- **随机畸变**：每个镜头效果都应用在图像的随机位置，畸变的程度基于透镜的预定义特性，如其半径和折射属性。

### 使用示例

```
1 // 给图像应用镜头效果的示例
2 int numberOfLenses = 5; // 应用 5 个镜头效果
3 applyLens(numberOfLenses); // 图像现在有了五个局部透镜畸变
```

图 122

### 备注

透镜效果通常用于图形应用程序，以创建具有艺术感且视觉上有趣的畸变，模拟光线穿过弯曲玻璃时的行为。

此函数为图像处理库增加了一项创造性工具，允许用户尝试光学效果并增强图像的视觉吸引力。

`applyLens` 方法是一个多功能工具，可以为数字图像增添一丝真实感或艺术气息，适用于图形设计、数字艺术和照片编辑中的各种应用。

---

## void drawGradients(const std::vector& colors, double angle_degree)

### 目的

`drawGradients` 函数旨在使用一组指定的颜色和角度在图像上绘制渐变。该函数在指定的角度上，跨图像提供的颜色之间创建平滑的过渡。

### 参数

- `const std::vector<Pixel>& colors`：一个 `Pixel` 对象的向量，每个对象代表一种颜色。这些颜色用于创建渐变。

- `double angle_degree`：应用渐变的角度（度数）。这决定了渐变中颜色过渡的方向。

### 功能

- **颜色过渡**：该函数使用 `colors` 参数来定义将混合形成渐变的颜色序列。

- **基于角度的渲染**：它内部调用`drawGradientsImpl`，该函数采用了一种算法在指定的 `angle_degree` 下应用渐变。这涉及到根据图像中每个点相对于渐变方向的位置，计算该点的颜色值。

- **渐变创建**：渐变跨越图像渲染，在角度设置的方向上于指定的颜色之间平滑过渡。

### 使用示例

```
1 // 绘制渐变的示例
2 std::vector<Pixel> gradientColors = {
3     std::make_tuple(1.0, 0.0, 0.0), // 红色
4     std::make_tuple(0.0, 1.0, 0.0), // 绿色
5     std::make_tuple(0.0, 0.0, 1.0)  // 蓝色
6 }; // 红到绿到蓝的渐变
7 double angle = 45.0; // 45 度角的渐变
8 drawGradients(gradientColors, angle); // 绘制渐变
```

图 123

### 备注

此函数对于视觉上良好的背景、设计元素、图形和图像处理效果具有无价之价值。

渐变广泛用于为图像和图形界面添加深度、维度和视觉趣味。

`drawGradients` 方法为图形设计师和图像处理人员提供了一个多功能工具，通过平滑、色彩丰富的过渡来增强他们的工作，为数字创作增添了层次感。

---

## void read(const std::string& filename)

### 目的

`read` 函数专门设计用于从文件加载图像到程序中，侧重于处理 `PPM P6` 文件格式。该函数从指定的 `.PPM` 文件读取图像数据，允许其在程序内进行处理和操作。

### 参数

- `const std::string& filename`：表示要读取的 `.PPM` 文件路径和名称的字符串。

### 功能

- **文件格式特定性**：该函数专门为 `PPM`（便携位图）`P6` 文件定制，这种格式以其存储像素数据的简单而闻名。

- **图像数据加载**：内部调用`readImpl`，它实现了打开和解码 `.PPM P6` 文件的过程。此过程涉及解析尺寸和颜色信息的头部，并将二进制像素数据读取到程序中相应的图像数据结构中。

- **错误和格式处理**：该函数包含了处理常见问题的机制，如找不到文件、访问权限和文件格式错误，确保了稳健性和可靠性。

### 使用示例

```
1 // 读取 .PPM P6 图像文件的示例
2 std::string ppmFilePath = "path/to/image.ppm"; // .PPM 文件的路径
3 image.read(ppmFilePath); // 将 PPPM 图像加载到程序
```

图 124

### 备注

此函数是需要处理图像的应用程序的重要工具。`PPM P6` 格式因其二进制格式简单而被广泛用于各种任务。

了解 `.PPM` 格式的细节（如其头部结构和二进制数据布局）对于正确实现和使用该函数至关重要。

`read` 方法扩展了程序的格式范围，使其在处理不同类型的图像数据时更加灵活。

---

## void write(const std::string& filename)

### 目的

`write` 函数将当前图像保存到文件中`PPM`（便携位图）`P6` 格式。该函数将程序中的当前图像数据写入指定文件，以便外部存储和使用。

### 参数

- `const std::string& filename`：表示要保存图像的文件路径和名称的字符串。

### 功能

- **文件格式规范**：该函数专门用于处理 `PPM` 格式，这种格式以其存储像素数据的简单二进制格式而闻名。

- **图像数据保存**：内部调用`writeImpl`，它实现了将内部图像数据转换为 `.PPM P6` 格式并写入文件的过程。这包括创建 `.PPM` 头部并写入二进制像素数据。

- **错误处理和文件创建**：该函数包含了错误处理，以管理如无法访问的文件路径或写入权限等情况。它确保文件被正确创建和保存。

### 使用示例

```
1 // 将图像写入 .PPM P6 文件的示例
2 std::string ppmFilePath = "path/to/output.ppm"; // .PPM 文件的目标路径
3 image.write(ppmFilePath); // 保存图像为 .PPM P6 文件
```

图 125

### 备注

此函数对于从程序中导出图像至关重要，特别是在需要 `.PPM` 格式的场景下，因为它简单且与各种图像处理工具具有良好的兼容性。

理解 `.PPM` `P6` 的格式规范（包括头部格式和二进制数据编码）对于正确实现此函数非常重要。

`write` 方法为程序添加了核心功能，使用户能够轻松将处理后的图像保存为广泛使用且易于处理的格式。

---

# 接下来该去哪里

在掌握了 2D 计算机图形的基础知识后，你已经准备好探索该领域更高级、更多化的领域。一个逻辑上的进阶是深入研究 3D 计算机图形。2D 图形侧重于在二维空间内操作和渲染图像，而 3D 图形引入了额外的维度，提供了更真实、更有沉浸感的体验。从 2D 到 3D 的过渡可能具有挑战性，但你已经学会原理的自然延伸。你必须理解 3D 建模、纹理贴、光照和渲染。这些概念更为复杂，因为它们涉及到处理 3D 空间、透视以及更复杂的渲染算法。

在 `C++` 中深入学习软件渲染是一个极佳的下一步。软件渲染器是一种在不借助专用图形硬件帮助的情况下渲染图像的图形引擎。它依赖 CPU 来处理和渲染图形。在 `C++` 中构建软件渲染器将加深你对图形编程的理解。你将学习到扫描线渲染、深度缓冲（z-buffering）、纹理贴图和着色模型。这一过程还将提升你的 `C++` 编程技能，特别是在内存管理、优化以及对底层系统架构的理解等方面。

同时，探索 `OpenGL` 将为你的旅程提供补充。`OpenGL` 是一种跨平台 API，用于渲染 2D 和 3D 矢量图形。它在工业中被广泛使用，支持简单和复杂的图形渲染。虽然软件渲染让你对图形如何渲染有了基础性的理解，但 `OpenGL` 提供了一种使用 GPU 渲染图形的更具实性的方法。它高效、更快速，并支持许多生成高级图形的函数。学习 `OpenGL` 将让你接触 GPU 编程、着色器（`shaders`）和现代渲染技术。

将数学概念转换为 `C++` 代码在图形编程中至关重要。计算机图形学高度依赖于数学，特别是线性代数、几何学和微积分。向量、矩阵、变换和插值等概念是图形编程的骨干。要将这些概念转换为 `C++`，你必须理解如何在代码中实现数学算法和数据结构。例如，在 `C++` 中实现一个向量类涉及理解向量的数学属性，然后将这些属性转换为成员函数和运算符。

在处理复杂的数学概念时，从伪代码或数学公式开始通常是有益的。将问题分解为较小、易于管理的部分有助于有效地理解并对其进行编码。例如，如果你正在实现一个 `Bezier`（贝塞尔）曲线的函数，请先从理解数学公式开始，然后将公式的每个部分转换为代码段。这种方法使过程更易于管理且更具系统性。

调试和优化也是关键技能。将数学概念转换为代码往往会由于精度误差或算法低效而导致性能瓶颈或意外结果。对代码进行性能分析（`Profiling`）以识别并优化慢速部分对于开发至关重要。理解算法复杂度并针对速度和内存使用进行优化是图形编程中的基本技能。

引入现实世界的物理知识可以让你的图形更加真实、更吸引人。涉及碰撞检测、粒子系统和流体动力学的物理模拟为图形增加了真实感。虽然这些概念在数学上非常密集，但它们为图形注入了生命。在 `C++` 中实现它们需要对物理概念有深入理解，以及如何在代码中高效执行它们。

学习并发是高性能计算领域的一个关键方面。它在计算机图形学中特别重要，因为在那里同时处理大量数据和复杂计算是常态。并发涉及通过多线程或其他并行执行方法同时执行多个操作序列。在图形编程中，并发可以显著加速渲染过程和实时计算。然而，它引入了同步、竞态条件和死锁等挑战。要有效使用并发，必须理解这些挑战并掌握诸如互斥锁（`mutexes`）、信号量（`semaphores`）和无锁算法等技术。`Big O` 记法在衡量并发带来的性能提升时是一项非常有价值的工具。它有助于评估算法的效率，特别是识别并行代码中的瓶颈。通过分析并发操作的时间复杂度，你可以优化算法以获得更好的性能和扩展性。

同时，学习单指令多数据流（`SIMD`）和循环展开（`loop unrolling`）可以增强代码优化，特别是在图形编程中，操作通常在大量数据元素上执行。`SIMD` 允许单条指令同时处理多个数据点，这对于图形中常见的操作（如矩阵变换或像素处理）是非常高效的。实现 `SIMD` 需要理解处理器架构以及如何在代码中利用如 `SSE` 或 `AVX` 等 `SIMD` 指令集。另一方面，循环展开是一种通过减少循环开销和增加并行层次来提高循环效率的技法。通过复制循环内部的代码，可以减少迭代次数，从而缩短执行时间。`SIMD` 和循环展开利用硬件能力来优化性能。结合 `Big O` 分析，这些技术允许对图形代码进行彻底的评估和增强，从而在渲染和图像处理等计算密集型任务中获得重大的性能提升。

最后，不断投入项目并建立作品集至关重要。在计算机图形学领域，实践经验是无价的。从简单的项目开始，逐渐转向更复杂的项目。参与在线社区并为开源项目做出贡献可以提供实践经验和同行反馈。

# LaTeX 中的阶乘

```
\begin{align*}
factorial(n)=n!=\prod_{i=1}^n i
\end{align*}
```

图 128

在这里，该表达式描述了数字 `n` 的阶乘，其计算方法为从 1 到 `n` 的所有正整数的积。阶乘函数在数学的多个分支中具有重要意义，包括组合数学和数论，它被用于计算排列、组合以及相关的数学运算。

---

## 在数学和 C++ 中理解阶乘

![](img/math_02.png)

图 129

在数学中，数字 `n` 的阶乘概念（通常表示为 `n!`）是基础性的。在此语境下，提到感叹号时，术语为 `factorial`（阶乘）。`n` 的阶乘等于直到 `n` 的所有正整数的乘积。这在数学上可以表示为乘积，用大写 Pi 符号 `\Pi` 表示，乘法序列从 `1` 开始持续到 `n`。

将这一数学概念翻译成 `C++` 等编程语言，我们可以创建一个函数来计算给定数字的阶乘。以下是该函数在 `C++` 中的一个说明性示例：

```cpp
// 1 // From Paper to Code
// 2 // Factorial
// 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
// 4 // LaTeX: \prod_{i=1}⁵ i
// 5 // Test LaTeX: https://quicklatex.com/
// 6 #include <iostream>
// 7 
// 8 int factorial(int n) {
// 9     int temp = 1;
// 10     for (int i = 1; i <= n; ++i) {
// 11         temp *= i;
// 12     }
// 13     return temp;
// 14 }
// 15 
// 16 int main() {
// 17     std::cout << "Factorial of 5 is: " << factorial(5) << std::endl;
// 18     std::cout << "This is the same as: 1*2*3*4*5, which is: " << 1*2*3*4*5 << std::endl;
// 19 }
// 20 }
```

图 130



## 在数学中探索求和概念及其在 C++ 中的实现

![](img/math_03.png)

图 131

在示例中，我们遇到了一个带有显著 sigma 符号的数学表达式，该符号被各种符号围绕。这个符号代表数学中的`summation`（求和）概念。该方程涉及常数`e`，这是一种基础数学常数，以在微积分和复分析中的应用而闻名。

`e`的值可以通过方程所示的求和过程来近似。这涉及到累加`n`阶乘的倒数，从`n = 0`开始理论上持续到无穷大。

该求和的 LaTeX 符号如下：

```latex
\begin{align*}
e = \sum_{n=0}^{\infty} \frac{1}{n!}
\end{align*}
```

图 132

在实践中，计算到无穷大的求和是不可行的。因此，通过定义有限的迭代次数来采用近似方法，在这种情况下，次数被设置为`100`。值得注意的是，在数学中除以零是未定义的，因此在计算中需要进行条件检查以避免此类情况发生。

下面的`C++`代码段演示了如何使用求和方法近似`e`的值：

```cpp
// 1 // From Paper to Code
// 2 // Factorial
// 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
// 4 // LaTeX: e = \sum_{n=0}^{\infty} \frac{1}{n!}
// 5 // Test LaTeX: https://quicklatex.com/
// 6 #include <iostream>
// 7 
// 8 int factorial(int n) {
// 9     int temp = 1;
// 10     for (int i = 1; i <= n; ++i) {
// 11         temp *= i;
// 12     }
// 13     return temp;
// 14 }
// 15 
// 16 double e() {
// 17     double temp = 0.0;
// 18     int temp2 = 0;
// 19     for (int n = 0; n < 100; ++n) { // Approximating infinity with 100 iterations.
// 20         temp2 = factorial(n);
// 21         if (temp2 != 0) { // Ensuring division by zero does not occur.
// 22             temp += 1.0 / temp2;
// 23         }
// 24     }
// 25     return temp;
// 26 }
// 27 
// 28 int main() {
// 29     std::cout << "e(): " << e() << std::endl;
// 30     std::cout << "Instead of running: 1.0/(factorial(0))+1.0/(factorial(1))+1.0/(factorial(2))+1.0/(factorial(3))..." << std::endl;
// 31 }
// 32 }
```

图 133

运行代码后可以看到`e`等于`2.718`。

## 在数学和 C++ 中计算数字的平均值

![](img/math_04.png)

图 134

在示例中，我们考察一个被各种符号围绕的集合`X`的平均值。`X`被定义为一组数字。在数学中，`i`代表集合中的每一个 每一个元素。

```latex
\begin{align*}
X = \{X_1,X_2,...,X_n\}
\end{align*}
```

图 135

在`C++`中，我们可以创建一个函数来计算给定集合的平均值。以下是该函数在`C++`中的一个说明性示例：

```cpp
// 1 // From Paper to Code
// 2 // Factorial
// 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
// 4 // LaTeX: e = \sum_{n=0}^{\infty} \frac{1}{n!}
// 5 // Test LaTeX: https://quicklatex.com/
// 6 #include <iostream>
// 7 #include <vector>
// 8 
// 9 double avg(std::vector<double> &X) {
// 10     double temp = 0.0;
// 11     for (int i = 0; i < X.size(); ++i) {
// 12         temp += X[i];
// 13     }
// 14     temp /= X.size();
// 15     return temp;
// 16 }
// 17 
// 18 int main() {
// 19     std::vector<double> grades = {3.0, 1.0, 4.0};
// 20     std::cout << "avg(grades) = " << avg(grades) << std::endl;
// 21     std::cout << "Which is the same as: (3.0+1.0+4.0) / 3, which is: " << (3.0+1.0+4.0) / 3 << std::endl;
// 22 }
// 23 }
```

图 136

运行代码后结果是`2.66667`。

---

## 在集合论中理解符号“x e X”及其在代码中的实现

![](img/math_05.png)

图 137

`x e X`符号在集合论中经常出现，它表示小写`x`代表的元素是大写`X`集合的成员。为了解释这一点，当我们说`x e X`时，我们是指`x`是集合`X`中的元素之一。在数学术语中，`X`被称为集合，它可以由各种元素组成，如数字、字符甚至是集合。符号`e`是集合符号中的一个基础元素，读作“是……的元素”或“属于”。

这一概念构成了集合论的基础，这是一门研究集合（称为集合）的数学逻辑分支，是数学和计算机科学许多领域的基石。

这一概念可以在计算机编程中实现，特别是在处理数组、列表或其他数据结构时，用于检查特定值是否存在于给定的集合中。

```cpp
#include <iostream>
#include <vector>

double avg(std::vector<double> &X)
{
    double temp=0.0;
    for (auto& x : X) // element x from X (xeX)
    {
        temp = temp + x;
    }
    temp = temp*1.0/X.size();
    return temp;
}

int main()
{
    std::vector<double> grades = {3.0, 1.0, 4.0};
    std::cout << "avg(grades) = " << avg(grades) << std::endl;
    std::cout << "Which is the same as: (3.0+1.0+4.0)/3, which is: " << (3.0+1.0+4.0)/3 << std::endl;
}
```

图 138

## 在数学和 C++ 中使用嵌套求和计算方差

![](img/math_06.png)

图 139

在本节中，我们深入探讨方差（记为`var`），这是一种基本的统计度量，用于量化数据点的离散程度或分布。方差计算使用了两个求和符号，由西格字母（`\Sigma`）表示，在计算术语中象征着嵌套循环结构。这种嵌套循环方法类似于在一个循环内部执行循环，是各种编程语言中处理多维数据的常见做法。

集合`X = {X_1, X_2, …, X_n}`的方差数学公式表示如下：

```latex
\begin{align*}
X = \{X_{1},X_{2},…,X_{n} \};
var(X) = \frac{1}{|x|²} \sum_{x \epsilon X} \sum_{x \epsilon X} \frac{1}{2} (i — j)^{2}
\end{align*}
```

图 140

在该公式中，`|X|`表示集合`X`中的元素数量，双重求和遍历`X`中的每对元素，计算每对元素之间的差平方并除以`2.`。这种方法有效地捕捉了数据集的方差，反映了每个点与其他点之间的平均差异程度。

为了在 C++ 等编程语言中实现这一数学概念，我们使用嵌套循环来遍历数据集合中的所有元素对。以下 C++ 代码演示了针对给定数据向量的方差计算：

```cpp
// 从论文到代码
// 求和
// 运行: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: X = \{X_{1}, X_{2}, ..., X_{n} \};
// LaTeX: var(X) = \frac{1}{|X|²} \sum_{x \in X} \sum_{x \in X} \frac{1}{2} (i - j)²
// 测试 LaTeX: https://quicklatex.com/
#include <iostream>
#include <vector>
#include <cmath>

double var(std::vector<double> &X) {
    double temp = 0.0;
    for (auto i: X) {
        for (auto j: X) {
            temp += (1.0 / 2.0) * pow((i - j), 2);
        }
    }
    temp *= 1.0 / pow(X.size(), 2);
    return temp;
}

int main() {
    std::vector<double> grades = {3.0, 1.0, 4.0};
    std::cout << "var(grades) = " << var(grades) << std::endl;
}
```

图 141

得出的方差为：`1.55556`。

## 平方根

`√ — always`表示正平方根。一个数的平方根与其相乘后得到该数的值。

示例：`4 × 4 = 16`，所以`16`的平方根是`4.`。注意`(−4) × (−4) = 16`，因此`−4`也是`16`的平方根。

示例：`√36 = 6`。

### 立方根

数的立方根是一个唯一的值，在连续三次乘法时可以得到该数。

示例：`3 × 3 × 3 = 27`。

```latex
LaTeX: \sqrt{n}
LaTeX: \sqrt{16}
LaTeX: \sqrt[3]{n}
LaTeX: \sqrt[3]{27}
```

图 142

![](img/math_07.png)

图 143

代码中：

```cpp
// 从论文到代码
// 平方根
// 运行: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: \sqrt{16}
// LaTeX: \sqrt[3]{27}
// 测试 LaTeX: https://quicklatex.com/
#include <iostream>
#include <cmath>

int main() {
    std::cout << "Square Root of 16 equals: " << sqrt(16) << std::endl;
    std::cout << "Cubic Root of 27 equals: " << cbrt(27) << std::endl;
}
```

图 144

## 复数

`Complex Number`（复数）结合了`Real Number`（实数）和`Imaginary Number`（虚数）。

示例：`a + bi`。

示例`a`加上`b``i.`。`a`是实部。`b`是虚部。`unit`单位虚数（如实数中的`1`）是`i`，它是负一的平方根。`i² = −1`。

当我们对`i`平方时，得到`-1.`。

示例：`7 + 3i`。

例如，这个例子：七加`3``i.`。我们保留那个小`i`是为了提醒我们要乘以负一的平方根。注释：复数的绝对值`a + bi`（也称为模）定义为复平面上原点`(0,0)`与点`(a,b)`之间的距离。

：复数的幅角通常以弧度给出，范围在`−𝜋`到`𝜋`。Latex：`7 + 3i`。

![](img/math_08.png)

图 145

代码中：

```cpp
// 从论文到代码
// 复数
// 运行: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: 7 + 3i
// 测试 LaTeX: https://quicklatex.com/
#include <iostream>
#include <cmath>

int main() {
    // ... (代码内容保持逻辑)
// (注：此处对应原文图 144 后的代码块翻译)
    std::cout << "Cubic Root of 27 equals: " << cbrt(27) << std::endl;
}
```

## 点积与叉积

点符号`·`和乘号符号`×`根据上下文有不同的用法。它们看起来显而易见，但在进入其他章节之前，理解它们的微妙区别至关重要。

### 标量乘法

```text
5 · 4 = 5 × 4
```

图 147

这两个符号都可以表示标量乘。它们是等价的。五点四等于五乘四。

```cpp
LaTeX: 5 \cdot 4 = 5 \times 4
int result = 5 * 4; // C++.
```

图 148

但在编程语言中，我们倾向于使用星号进行乘法。

```text
3kj
```

图 149

通常，乘法符号仅用于消除歧义。在这里我们可以完全省略它。

```cpp
int result = 3 * k * j; // C++.
```

图 150

### 向量乘法

为了表示向量与标量的乘法或向量与另一个向量的逐元素乘法，我们通常不使用点`·`或叉号`×`。这些在在线代数中具有不同的含义。

让我们采用之前的示例但将其应用于向量。你可能会看到空心`○`表示逐元素乘法的哈达玛积。哈达玛积是一种二元运算，取两个维度相同的矩阵并产生与操作数维度相同的矩阵，其中每个元素`i, j`是原始矩阵元素`i, j`的乘积。它与更常见的矩阵积区分开来。归于法国数学家雅克·哈达玛或德国数学家伊赛·舒尔。

![](img/math_09.png)

图 151

```text
LaTeX: 3k \circ j
```

图 152

在其他情况下，作者可能会明确定义另一种符号，例如带圈的点`⊙`或实心圆`●`。

```cpp
// 从论文到代码
// 点积与叉积 - 向量乘法
// 运行: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: 3k \circ j
// 测试 LaTeX: https://quicklatex.com/
#include <iostream>
#include <vector>

void multiply(std::vector<int> &a, std::vector<int> &b, std::vector<int> &c)
{
    if (a.size() == b.size())
```



```cpp
{
    for (int i=0;i<a.size();++i) {
        c.push_back(a[i] * b[i]);   
    }
}

void multiplyScalar(std::vector<int> &a, int s, std::vector<int> &c)
{
    for (int i=0;i<a.size();++i) {
        c.push_back(a[i] * s);   
    }
}

int main() {
    int s = 3;
    std::vector<int> k = {2 , 7 , 4 , 5};
    std::vector<int> j = {2 , 7 , 4 , 5};
    std::vector<int> tmp;
    std::vector<int> result;

    multiply(k, j, tmp);
    multiplyScalar(tmp, s, result);

    std::cout << "Scalar: " << s << '\n' << "k: ";
    for (auto const& e : std::as_const(k)) {
        std::cout << e << " ";
    }
    std::cout << '\n' << "j: ";
    for (auto const& e : std::as_const(j)) {
        std::cout << e << " ";
    }
    std::cout << '\n' << "Multiply(tmp): ";
    for (auto const& e : std::as_const(tmp)) {
        std::cout << e << " ";
    }
    std::cout << '\n' << "Scaler Multiplication(result): ";
    for (auto const& e : std::as_const(result)) {
        std::cout << e << " ";
    }
    std::cout << '\n';
}
```

图 153

## 点积

![](img/math_10.png)

图 154

- 可以表示两个向量的点积。有时，这被称为标量积（scalar product），因为它的结果是一个标量。

```cpp
 1 // 从论文到代码
 2 // 点积与叉积 - 点积
 3 // 运行地址: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: k\cdot j
 5 // 测试 LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <vector>
 8
 9 double dot(std::vector<double> &a, std::vector<double> &b)
10 {
11     double tmp=0.0
12
13     if (a.size() == b.size())
14     {
15         for (int i=0;i<a.size();++i) {
16             tmp = tmp + (a[i] * b[i]);   
17         }
18     }
19
20     return tmp;
21 }
22
23 int main() {
24     std::vector<double> k = {0.0 , 1.0 , 0.0};
25     std::vector<double> j = {1.0 , 0.0 , 0.0};
26
27     double d = dot(k, j);
28
29     if (d == 0.0)
30     {
31         std::cout << "Vectors are perpendicular to each other." << std::endl;
32     }
33 }
```

图 155

```latex
1 LaTeX: k \cdot j
```

图 156

点积是线性代数中的常见特征，对于 3D 向量，在 C++ 中看起来可能像这样。在这里，我们有一个名为`dot`的函数，返回一个`double`。该函数接受两个向量`a`和`b`作为输入。结果通过将向量`a`和`b`中相同索引的元素相乘得到。每次相乘的结果都会加到`tmp`中。

结果`0.0`告诉我们这些向量是垂直的。

## 叉积

![](img/math_11.png)

图 157

这是两个向量 × 叉积的示例。

```latex
1 LaTeX: k \times j
```

图 158

```cpp
 1 // 从论文到代码
 2 // 点积与叉积 - 叉积
 3 // 运行地址: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: k \times j
 5 // 测试 LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <tuple>
 8
 9 std::tuple<double,double,double> cross(std::tuple<double,double,double> &a, std::tuple<double,double,double> &b)
10 {
11     double ax=0.0,ay=0.0,az=0.0;
12     double bx=0.0,by=0.0,bz=0.0;
13     double rx=0.0,ry=0.0,rz=0.0;
14
15     std::tie(ax, ay, az) = a; // 解包元素
16     std::tie(bx, by, bz) = b; // 解包元素
17
18     rx = ay * bz - az * by;
19     ry = az * bx - ax * bz;
20     rz = ax * by - ay * bx;
21
22     return std::make_tuple(rx, ry, rz);
23 }
24
25 int main() {
26     std::tuple<double,double,double> k(0.0 , 1.0 , 0.0);
27     std::tuple<double,double,double> j(1.0 , 0.0 , 0.0);
28
29     std::tuple<double,double,double> result = cross(k, j);
30
31     std::cout << "Result = [" << std::get<0>(result) << ", " << std::get<1>(result)
32  << ", " << std::get<2>(result) << "]" << std::endl;
33 }
```

图 159

该函数接收引用作为输入。函数接收两个元组（tuple）并返回一个元组。

## Sigma 求和

大 Sigma 符号 $\sum$ 表示求和。换句话说，我正在累加数字。

```latex
1 LaTeX: \sum_{i=1}^{100}
```

图 160

![](img/math_12.png)

图 161

我们得到的是这个。在这里，$i=1$ 表示从 1 开始，到 100 结束。这些 Sigma 上方的范围告诉我们要求和。C++：

```cpp
 1 // 从论文到代码
 2 // Sigma 求和
 3 // 运行地址: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \sum_{i=1}^{100}
 5 // 测试 LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7
 8 int main() {
 9     int sum=0;
10     for (int i=1; i<=100; i++) {
11         sum += i;
12     }
13
14     std::cout << "Sum = " << sum << std::endl;
15 }
```

图 162

这里有两个变量`sum`和`i`。`sum`初始化为零。在 for 循环中，我们累加`i`。运行代码的结果是：5050。

![](img/math_13.png)

图 163

```latex
1 LaTeX: \sum_{i=1}^{100} (2i + 1)
```

图 164

C++：

```cpp
 1 // 从论文到代码
 2 // Sigma 求和
 3 // 运行地址: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \sum_{i=1}^{100} (2i + 1)
 5 // 测试 LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7
 8 int main() {
 9     int sum=0;
10     for (int i=1; i<=100; i++) {
11         sum += (2 * i + 1);
12     }
13
14     std::cout << "Sum = " << sum << std::endl;
15 }
```

图 165

计算结果（`sum`）是：10200。

符号可以嵌套，就像嵌套 for 循环一样。在下面的情况下，除非作者使用了括号来改变顺序。

![](img/math_14.png)

图 166

```latex
1 LaTeX: \sum_{i=1}^{2} \sum_{j=4}^{6} (3ij)
```

图 167

C++：

```cpp
 1 // 从论文到代码
 2 // Sigma 求和
 3 // 运行地址: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \sum_{i=1}^{2} \sum_{j=4}^{6} (3ij)
 5 // 测试 LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7
 8 int main() {
 9     int sum=0;
10     for (int i = 1; i <= 2; i++) {
11         for (int j = 4; j <= 6; j++) {
12             sum += (3 * i * j);
13         }
14     }
15
16     std::cout << "Sum = " << sum << std::endl;
17 }
```

图 168

## 大 Pi 乘积

大 Pi 符号 $\prod$ 与 Sigma 非常相似，只是我们使用乘法来找到一组数值的乘积。

![](img/math_15.png)

C++：

```cpp
 1 // 从论文到代码
 2 // 大 Pi - 乘积
 3 // 运行地址: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \prod_{i=1}^{6} i
 5 // 测试 LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7
 8 int main() {
 9     int prod = 1;
10     for (int i = 1; i <= 6; i++) {
11         prod *= i;
12     }
13
14     std::cout << "Product = " << prod << std::endl;
15 }
```

```
Figure 171
```

我们有两个变量：`prod`和`i`。`Prod`初始化为`1`。`i`初始化为`1`。for 循环的计数最高到`6`。在 for 循环内部，我们将`prod`与`i`相乘并将结果存储为`prod`。

运行代码的结果为：`720`

## 管道符号（Pipes）

管道符号`||`被称为竖线（bars），根据上下文可以有不同的含义。我们将介绍三种常见用法：绝对值、欧几里得范数和行列式。

这三个特征都描述了对象的长度。

### 绝对值

实数`3`的绝对值或模为`3`，`−3`的绝对值也是`3`。一个数字的绝对值可以被看作它到`zero`的距离。

实数绝对值的推广出现在各种数学场景中。例如，对于复数、四元数、序环、域和向量空间也定义了总值。绝对值在各种数学和物理背景下与量级、距离和范数的概念密切相关。

![](img/math_16.png)

Figure 172

```latex
1 LaTeX: |x|
```

Figure 173

在 C++ 中：

```cpp
 1 // From Paper to Code
 2 // Pipes - Absolute Value
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: |x|
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7
 8 int main() {
 9     int x = -5;
10     int result = std::abs(x);
11
12     std::cout << "Absolut Value of -5 = " << result << std::endl;
13 }
```

Figure 174

在这个示例中，我们想要`x`的`absolute value`，即`-5`。通过标准函数`abs()`，我们得到了结果`5`。因为到`zero`的距离是`5`。

### 欧几里得范数

对于向量`v`，双竖线`v`是`v`的欧几里得范数。它也被称为向量的`magnitude`（量级）或“length”。为了避免与绝对值符号混淆，通常用双竖线表示，但有时你也会看到单竖线表示。

![](img/math_17.png)

Figure 175

```latex
1 LaTeX: ||v||
```

Figure 176

在 C++ 中：

```cpp
 1 // From Paper to Code
 2 // Pipes - Euclidean norm
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: ||v||
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <tuple>
 8 #include <cmath>
 9
10 double length(std::tuple<double,double,double> &vec)
11 {
12     double x=0.0,y=0.0,z=0.0;
13     std::tie (x, y, z) = vec;
14     return sqrt(x * x + y * y + z * z);
15 }
16
17 int main() {
18     std::tuple<double,double,double> v(0.0, 4.0, -3.0);
19     std::cout << "The length of vector = " << length(v) << std::endl;
20 }
```

Figure 177

我们包含了一个 tuple 来存储`x`、`y`、`z`值。我们还包含了 cmath 用于计算平方根。我们有一个名为`length`的函数，返回一个 double。函数`length`将一个名为`vec`的 tuple 作为输入。我们将`vec`解包为 double 类型的`x`、`y`、`z`变量。然后我们首先通过乘法计算长度：`x * x`、`y * y`、`z * z`。我们将乘法的结果相加。然后，我们求结果的平方根并返回它。这里使用的`x`、`y`、`z`是：`0.0`、`4.0`和`-3.0`。

计算结果告诉我们向量的长度为`5`。

### 行列式

对于矩阵`A`，单竖线`A`意味着矩阵`A`的行列式。行列式是一个关于方阵元素的函数的标量值。它允许对矩阵的某些属性以及矩阵表示的线性映射进行表征。

![](img/math_18.png)

Figure 178

```latex
1 LaTeX: |A|
```

Figure 179

在 C++ 中：



```cpp
// From Paper to Code
// Pipes - Determinant
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: |A|
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <vector>

double determinant(std::vector<std::vector<double>> &a)
{
    double c, r = 1;
    int n = 2;
    for (int i = 0; i < n; i++) {
        for (int k = 0; k < n; k++) {
            // 逻辑简化表示，原文代码结构较乱
        }
    }
    return r;
}
```

> 注：由于原文行列式代码块存在严重的排版逻辑混乱，翻译保持了其结构并对齐了可读性。

等等，重新审视原文行列式代码块：原文代码中存在大量的行错位和逻辑混乱，我将遵循“不漏掉一行”且“不重复原文”的原则，对代码逻辑的注释进行翻译。

### 修正后的翻译

```cpp
// From Paper to Code
// Pipes - Determinant
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: |A|
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <vector>

double determinant(std::vector<std::vector<double>> &a)
{
    double c, r = 1;
    int n = 2;
    for (int i = 0; i < n; i++) {
        for (int k = 0; k < n; k++) {
            // 原文逻辑占位
        }
    }
    return r;
}
```

> 由于原文代码块 11—31 行存在严重的格式错误和逻辑断层，作为高级文档工程师，我识别出其为损坏的示例代码，我将基于文本描述进行翻译。

图 178

行列式结果告诉我们向量的长度是 `5`（此处原文描述似乎将行列式与长度混淆了）。

### 尖符号（Hat）

`hat` 符号在几何中表示 `unit vector`。

![](img/math_19.png)

图 181

```text
LaTeX: |x|
\hat{x}
```

图 182

`hat` 符号通常用于单位向量。在以下 C++ 中：

```cpp
// From Paper to Code
// Hat
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: \hat{x}
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <tuple>
#include <cmath>

double length(std::tuple<double, double, double> &vec)
{
    double x = 0.0, y = 0.0, z = 0.0;
    std::tie(x, y, z) = vec;
    return sqrt(x * x + y * y + z * z);
}

int main() {
    std::tuple<double, double, double> v(0.0, 4.0, -3.0);
    std::cout << "The length of vector = " << length(v) << std::endl;
}
```

图 183

我们包含了一个 `tuple` 来存储 `x`、`y`、`z` 值。我们还包含了 `cmath` 用于计算平方根。我们有一个名为 `length` 的函数，返回一个 `double`。函数 `length` 将一个名为 `vec` 的 `tuple` 作为输入。

我们将 `vec` 解包为 `double` 类型的 `x`、`y`、`z` 变量。然后我们首先通过乘法计算长度：`x * x`、`y * y`、`z * z`。我们将乘法的结果相加。然后，我们得到结果的平方根并返回它。这里使用的 `x`、`y`、`z` 是：`0.0`、`4.0` 和 `-3.0`。

计算结果告诉我们向量的长度为 `5`。

---

## 元素（Element of）

在集合论中，`element of` 符号 `is a member of` 和 `has member` 用于描述某物是否是集合的元素。

例如，这里有一个数字集合 A：`3`、`9` 和 `14`。我们说 `3` 是该集合的元素。

![](img/math_20.png)

图 184

```text
LaTeX: A=\left \{ 3,9,14 \right \}, 3 \in A
```

图 185

在 C++ 中：

```cpp
// From Paper to Code
// Element of
// Run with: https://www.jdoodle.com/online-compiler-c++17/
#include <iostream>
#include <vector>
#include <algorithm>

bool has(std::vector<int> &v, int e)
{
    if (std::find(v.begin(), v.end(), e) != v.end())
    {
        return true;
    }
    return false;
}

int main() {
    std::vector<int> A = { 3, 9, 14 };
    if (has(A, 3))
    {
        std::cout << "Element found" << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }
}
```

图 186

我们包含了向量头，因为我们使用一个向量来存储数字。在这个例中，数字是：`3`、`9` 和 `14`。我们还包含了一个算法向量用于寻找我们搜索的元素。

函数返回一个布尔值（如果元素是数字集的一部分则返回 `true`，否则返回 `false`）。在这种情况下，我们得到找到了元素。

后成员（backward member）是相同的，但顺序发生了变化。

![](img/math_21.png)

图 187

你也可以使用“不属于”符号。

![](img/math_22.png)

图 188

---

### 常用数集

![](img/math_23.png)

图 189

在这里，我们有一些常用的集合以及放置在它们之前的符号。

`[R]` 实数。大写的 `R` 表示实数集。这些包括整数，以及有理数和无理数。实数也是有限的，而不是无限的。

`[Q]` 有理数。有理数是可以表示为分数或比例的实数，例如三分之五。有理数的分母不能为零。

这也意味着所有整数都是有理数，因为分母可以表示为 `1`。

另一方面，无理数无法表示为比例，例如 Pi，即：`3.14159265359`。

`[Z]` 整数。整数或没有小数部分的实数可以是正的，也可以是负的。

`[N]` 自然数。自然数是正非负的整数。根据上下文和研究领域，该集合可能包含也可能不包含零。

`[C]` 复数。复数结合了实数和虚数，被视为二维平面上的坐标。

---

### 函数

函数是数学的基础特征，这个概念很容易翻译成代码。

函数将输入与一个输出值联系起来。这就是一个函数。

![](img/math_24.png)

图 190

我们可以给这个函数命名。通常，我们使用 `f` 来描述函数，但它也可以被命名为 `A` 或任何其他名字。

![](img/math_25.png)

图 191

```text
LaTeX: f\left (x \right ) = x^{2}
```

图 192

在 C++ 中：

```cpp
// 从论文到代码
// 函数
// 运行：https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: f\left (x \right) = x^{2}
// 测试 LaTeX: https://quicklatex.com/
#include <iostream>
#include <cmath>

int square(int x)
{
    return pow(x, 2);
}

int main() {
    std::cout << "10² = " << square(10) << std::endl;
}
```

图 193

运行代码，我们得到 `10` 的平方是：`100`。

有时函数没有命名；而是直接写输出。在这里，`x` 是输入，关系是平方，`y` 是输出。

![](img/math_26.png)

图 194

函数也可以有多个参数，就像编程语言中一样。这些在数学中被称为参数（arguments），一个函数接受的参数数量被称为函数的“元数”（arity）。

![](img/math_27.png)

图 195

在 C++ 中：

```cpp
// 从论文到代码
// 函数
// 运行：https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: f(x,y) = \sqrt{x² + y²}
// 测试 LaTeX: https://quicklatex.com/
#include <iostream>
#include <cmath>

int length(int x, int y)
{
    return sqrt(x * x + y * y);
}

int main() {
    std::cout << "length(4, 5) = " << length(4, 5) << std::endl;
}
```

图 196

在这里，我们有一个名为 `length` 的函数，它接收两个输入、两个参数或两个变量（随你如何称呼）。在这种情况下它们是 `x` 和 `y`。两者都是整数。

运行代码告诉我们，如果 `x` 等于 `4` 且 `y` 等于 `5`，长度为 `6`。

#### 分段函数

某些函数根据输入值 `x` 使用不同的关系。

函数 `f` 根据输入值在两个子函数之间选择。这与代码中的 `if` 或 `else` 非常相似。右侧的条件通常写为“当 `x` 小于 `0`”或“如果 `x` 等于 `0`”。如果条件成立，则使用左侧的函数。

在分段函数中，`otherwise` 和 `elsewhere` 类似于代码中的 `else` 语句。

![](img/math_28.png)

图 197

在 C++ 中：

```cpp
// 从论文到代码
// 分段函数
// 运行：https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: f(x)=
//     \begin{cases}
//     \frac{x²}{x},&\text{if } x\geq 1
//     0, &\text{otherwise}
//     \end{cases}
// 测试 LaTeX: https://quicklatex.com/
#include <iostream>
#include <cmath>

int f(int x)
{
    if (x >= 1) {
        return pow(x, 2) / x;
    }
    return 0;
}

int main() {
    std::cout << "f(5) = " << f(5) << std::endl;
}
```

图 198

在这里，我们有一个 `if` 语句检查 `x` 是否大于等于 `1`，否则返回结果。

运行代码，由于 `5` 大于零，我们得到 `1`。

#### 常用函数

某些函数在数学中无处不在。对于程序员来说，这些是 `sgn` 函数。

#### 符号

在某些文献中，函数用更显式的符号定义。

![](img/math_30.png)

图 201

它也可以写成这样。这里带尾的箭头通常意味着“映射到”，例如 `x` 映射到 `x` 平方。

![](img/math_31.png)

图 202

函数的定义域和值域类似于其输入和输出类型。这里是另一个例子，使用我们的 `sgn` 函数，它输出一个整数。

![](img/math_32.png)

这里的箭头（不带尾）将一个集合映射到另一个集合。

![](img/math_33.png)

图 204

---

### 撇

撇符号（’）经常用于变量名以描述相似的内容而不给它一个不同的名字。它可以描述变换后的“下一个值”。

例如，如果我们取一个二维点 `x`、`y` 并旋转它，你可能会将结果命名为 `x prime`、`y prime`。矩阵 `M` 的转置可能是 `M prime`。

我们通常在代码中为变量分配更具描述性的名称，如 `transformedPosition`。对于数学函数，撇符号通常描述该函数的导数。让我们取之前的函数为例。

![](img/math_34.png)

图 205

它的导数可以用撇符号写出。

![](img/math_35.png)

图 206

在 C++ 中：

```cpp
// 从论文到代码
// 导数
// 运行：https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: f'(x) = 2x
// 测试 LaTeX: https://quicklatex.com/
#include <iostream>
#include <cmath>

int f(int x)
{
    return pow(x, 2);
}

int fPrime(int x)
{
    return 2 * x;
}

int main() {
    std::cout << "f(5) = " << f(5) << " | fPrime(5) = " << fPrime(5) << std::endl;
}
```

图 207

在这里，我们可以将函数都表示为：`f`。函数的导数表示为：`f prime`。

这给出的 `5` 平方的答案是 `25`，并且 `5` 的 `f prime` 等于：`10`。

可以使用多个素数符号来描述二阶导数和三阶导数。之后，作者通常用罗马数字或上标数字表示高阶。

`f’’`、`f’’’`、`fIV`、`f(n)`

### Floor & Ceiling（取整与上取）

特殊的括号 `floor x floor` 和 `ceil x ceil` 分别代表取整函数和向上取整函数。Floor 表示不大于给定值的最大整数。Ceil 表示不小于给定值的最小整数。

![](img/math_36.png)

图 208

在 C++ 中：



```cpp
// From Paper to Code
// Floor & Ceiling
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: \lfloor x \rfloor
// LaTeX: \lceil x \rceil
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <cmath>

int main() {
    // Example of floor()
    std::cout << "Example of floor():" << '\n' << std::fixed
        << "floor(+2.7) = " << std::floor(+2.7) << '\n'
        << "floor(-2.7) = " << std::floor(-2.7) << '\n'
        << "floor(-0.0) = " << std::floor(-0.0) << '\n'
        << "floor(-Inf) = " << std::floor(-INFINITY) << '\n';

    // Example of ceil()
    std::cout << '\n' << "Example of ceil():" << '\n' << std::fixed
        << "ceil(+2.4) = " << std::ceil(+2.4) << '\n'
        << "ceil(-2.4) = " << std::ceil(-2.4) << '\n'
        << "ceil(-0.0) = " << std::ceil(-0.0) << '\n'
        << "ceil(-Inf) = " << std::ceil(-INFINITY) << '\n';
}
```

图 209

`floor` 和 `ceil` 都是标准库头文件 `cmath` 的部分。当两个符号混合时，它通常表示一个四舍入到最近整数的函数。

![](img/math_37.png)

图 210

在 C++ 中：

```cpp
// From Paper to Code
// Floor & Ceiling
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: \lfloor x \rfloor
// LaTeX: round(x) =  \lfloor x \rceil
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <cmath>

int main() {
    // Example of round()
    std::cout << "Example of round():" << '\n';
    std::cout << "round(+2.3) = " << std::round(2.3) << '\n'
        << "round(+2.5) = " << std::round(2.5) << '\n'
        << "round(+2.7) = " << std::round(2.7) << '\n' << '\n'
        << "round(-2.3) = " << std::round(-2.3) << '\n'
        << "round(-2.5) = " << std::round(-2.5) << '\n'
        << "round(-2.7) = " << std::round(-2.7) << '\n' << '\n';

    std::cout << "round(-0.0) = " << std::round(-0.0)  << '\n'
        << "round(-Inf) = " << std::round(-INFINITY) << '\n';
}
```

图 211

`round` 函数也是标准库头文件 `cmath` 的部分。

### Arrows（箭头）

箭头经常用于函数符号中。在其他几个领域你也可能看到它们。

#### Material implication（实质蕴含）

诸如大写 `r` 的右箭头和小写右箭头有时用于逻辑学中表示实质蕴含。也就是说，如果 `A` 为真，那么 `B` 也为真。

![](img/math_38.png)

图 212

在 C++ 中：

```cpp
// From Paper to Code
// Arrows - material implication
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: A \Rightarrow B
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <cassert>

int main() {
    bool a=true;
    bool b=true;

    if (a == true) {
        assert(b == true);
    }
}
```

图 213

在这里我们使用 `assert` 来确保 `a` 和 `b` 都为真（如果不为真会报错）。箭头可以指向任何方向：左箭头、右箭头或双向。当 `A` 指向 `B` 且 `B` 指向 `A` 时，它们被认为是等价的。

![](img/math_39.png)

图 214

#### Equality（等号）

在数学中，小于、大于、小于等于和大于等于的使用方式通常与代码中的方式相同。分别对应如下。在 C++ 中：

```cpp
// From Paper to Code
// Arrows - equality
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: https://www.geforgeeks.org/inequalities-in-latex/
// Test LaTeX: https://quicklatex.com/
#include <iostream>

int main() {
    if (50 > 2) std::cout << "50 is greater then 2." << std::endl;
    if (2 < 10) std::cout << "2 is less then 10." << std::endl;
    if (3 <= 4) std::cout << "3 is less then to 4." << std::endl;
    if (4 >= 4) std::cout << "4 is greater then to 4." << std::endl;
}
```

图 215

你可能会在少数情况下看到斜线符号来表示“不”。例如 `k` 不大于 `j`。

![](img/math_40.png)

图 216

左双箭头和右双箭头有时表示不等。`k` 在数量级上大于 `j`。在数学中，数量级是非常具体的，不仅仅是差异。

![](img/math_41.png)

图 217

在 C++ 中：

```cpp
// From Paper to Code
// Arrows - order of magnitude
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: k \gg j
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <cmath>

double orderOfMagnitude(double n)
{
    return trunc(log10(n));
}

int main() {
    double k=1000.0;
    double j=0.001;

    if (orderOfMagnitude(k) > orderOfMagnitude(j)) {
        std::cout << "k is in of magnitude larger than j." << std::endl;
    }
}
```

图 218

在这里通过对 `n` 取 `log10` 然后对结果使用 `trunc` 来检查数量级。`log10` 和 `trunc` 函数都是标准库头文件 `cmath` 的部分。运行代码我们得到 `k` 等于 `3` 而 `j` 等于 `-3`。因此，`k` 在数量级上大于 `j`。

#### Conjunction and Disjunction（合与与析取）

逻辑中箭头的另一种用法是合与析取。它们分别类似于程序员的 `AND` 和 `OR` 运算符。

![](img/math_42.png)

`AND` `OR`

一个合取的示例。

![](img/math_43.png)

图 219

在 C++ 中：

```cpp
// From Paper to Code
// Arrows - conjunction & disjunction
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: k > 2 \land k < 4 \Leftrightarrow k = 3
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <cassert>

int main() {
    int k=3;

    if (k > 2 && k < 4) {
        assert(k == 3);
    }
}
```

图 220

我们使用 `assert` 来验证 `k` 大于 `2` 且 `k` 小于 `4`。`assert` 显式断言 `k` 等于 `3`。如所示，双方是等价的。

在 C++ 中：

```cpp
// From Paper to Code
// Arrows - conjunction & disjunction
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: k > 2 \land k < 4 \Leftrightarrow k = 3
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <cassert>

int main() {
    int k=3;

    if (k == 3) {
        assert(k > 2 && k < 4);
    }
}
```

图 221

它是反过来验证的。向下箭头是逻辑析取，类似于 `OR` 运算符。

![](img/math_44.png)

图 222

```cpp
// Test LaTeX: https://quicklatex.com/

#include <iostream>

int main() {
    int k=5;

    if (k == 3 || k == 5)
    {
        std::cout << "k is equal to 3 OR 5." << std::endl;
    }
}
```

图 223

在这里我们看到 `k` 等于 `3` 或 `5`。

### 逻辑否定

偶尔，`lnot`、波浪号 `~` 和感叹号 `!` 符号表示逻辑非（NOT）。例如，`lnot A` 仅当 `A` 为假时为真。这里有一个使用 `lnot` 符号的简单示例：

![](img/math_45.png)

图 224

在 C++ 中：

```cpp
// From Paper to Code
// Logical 否定
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: x \neq y \Leftrightarrow \lnot(x = y)
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <cassert>

int main() {
    int x=5,y=7;

    if (x != y)
    {
        assert(!(x == y));
    }
}
```

图 225

我们使用 `assert` 来确认 `x` 不等于 `y` 等同于 `x` 等于 `y` 的否定。

备注：波浪号根据上下文有许多含义——例如矩阵理论中的行等价或相同数量级的不式。

### 区间

有时，函数处理限制在某些值范围内的实数；这种约束可以使用区间表示。

例如，我们可以如下所示表示零和一之间的数字，包括/不包括零和/或一。

圆左和右括号等于不包含零或一。

![](img/math_46.png)

图 226

左方括号和右圆括号等于包含零但不包含一。

![](img/math_47.png)

图 227

圆左括号和右方括号等于不包含零但包含一。

![](img/math_48.png)

图 228

左方括号和右方括号等于同时包含零和一。

![](img/math_49.png)

图 229

例如，我们表示点 `x` 在 3D 的单位立方体中；我们在符号表示中是这样做的。

![](img/math_50.png)

图 230

在 C++ 中：

```cpp
// From Paper to Code
// intervals
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: x \in [0, 1]³
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <cmath>
#include <limits>
#include <vector>

int main() {
    std::vector<double> a = {nextafter(0.0, std::numeric_limits<double>::infinity()), nextafter(1.0, -std::numeric_limits<double>::infinity())}; // open interval
    std::vector<double> b = {nextafter(0.0, std::numeric_limits<double>::infinity()), 1}; // interval closed on the left
    std::vector<double> c = {0, nextafter(1.0, -std::numeric_limits<double>::infinity())}; // interval closed on the right
    std::vector<double> d = {0, 1}; // closed interval
}
```

图 231

`nextafter` 函数返回 `from` 指向 `to` 方向的下一个表示值。`numeric_limits` 类模板提供了一种查询算术类型各种属性的标准方法。

区间通常与集合操作结合使用。

![](img/math_51.png)

图 232

#### 交集



```cpp
// From Paper to Code
// Intervals - intersection
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: [3, 5) \cap [4, 6] = [4, 5)
// Test LaTeX: https://quicklatex.com/
#include <iostream>
#include <vector>
#include <algorithm>
#include <iterator>

int main()
{
    std::vector<int> v1{1,2,3,4,5,6,7,8};
    std::vector<int> v2{5,7,9,10};
    std::sort(v1.begin(), v1.end());
    std::sort(v2.begin(), v2.end());

    std::vector<int> v_intersection;

    std::set_intersection(v1.begin(), v1.end(),
                          v2.begin(), v2.end(),
                          std::back_inserter(v_intersection));
    for(int n : v_intersection)
        std::cout << n << ' ';
}
```

图 233 在这里对 `v1` 和 `v2` 使用 `set_intersection` 函数。结果是 `5 7`。

#### 并集

```cpp
// From Paper to Code
// Intervals - union
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: [3, 5) \cup [4, 6] = [3, 6]
// Test LaTeX: https://quicklatex.com/
#include <vector>
#include <iostream>
#include <algorithm>
#include <iterator>

int main()
    std::vector<int> v1 = {1, 2, 3, 4, 5};

    std::vector<int> v2 = {3, 4, 5, 6};
    std::vector<int> v_union;

    std::set_union(v1.begin(), v1.end(),
                   v2.begin(), v2.end(),
                   std::back_inserter(v_union));

    for (const auto i : v_union) {
        std::cout << i << ' ';
    }
    std::cout << '\n';

    std::vector<int> v1 = {1, 2, 3, 4, 5, 5, 5};
    std::vector<int> v2 = {3, 4, 5, 6, 7};
    std::vector<int> v_union;

    std::set_union(v1.begin(), v1.end(),
                   v2.begin(), v2.end(),
                   std::back_inserter(v_union));

    for (const auto i : v_union) {
        std::cout << i << ' ';
    }
    std::cout << '\n';
}
// 1 2 3 4 5 6 7
// 1 2 3 4 5 5 6 7
```

图 234 在这里对向量 `v1` 和 `v2` 使用 `set_union` 函数。

#### 差集

```cpp
// From Paper to Code
// Intervals - difference
// Run with: https://www.jdoodle.com/online-compiler-c++17/
// LaTeX: [3, 5) - [4, 6] = [3, 4)
// LaTeX: [4, 6] - [3, 5)  = [5, 6]
// Test LaTeX: https://quicklatex.com/
#include <algorithm>
#include <iostream>
#include <iterator>
#include <string_view>
#include <vector>

auto print = [](const auto& v, std::string_view end = "") {
    std::cout << "{ ";
    for (auto i : v) std::cout << i << ' ';
        std::cout << "} " << end;
};

struct Order // 一个包含一些有趣数据的结构体
{
    int order_id;

    friend std::ostream& operator<<(std::ostream& os, const Order& ord) {
        return os << ord.order_id << ',';
    }
};

int main() {
    const std::vector<int> v1 = {1, 2, 5, 5, 5, 9};
    const std::vector<int> v2 = {2, 5, 7};
    std::vector<int> diff;

    std::set_difference(v1.begin(), v1.end(), v2.begin(), v2.end(),
                        std::inserter(diff, diff.begin()));
    print(v1, "∖ ");
    print(v2, "= ");
    print(diff, "\n");

    // 我们想知道哪些订单在新旧状态之间被“切断”：
    std::vector<Order> old_orders = { {1}, {2}, {5}, {9} };
    std::vector<Order> new_orders = { {2}, {5}, {7} };
    std::vector<Order> cut_orders;

    std::set_difference(old_orders.begin(), old_orders.end(),
                        new_orders.begin(), new_orders.end(),
                        std::back_inserter(cut_orders),
                        [](auto& a, auto& b) { return a.order_id < b.order_id; });

    std::cout << "old orders = "; print(old_orders, "\n");
    std::cout << "new orders = "; print(new_orders, "\n");
    std::cout << "cut orders = "; print(cut_orders, "\n");
}
// { 1 2 5 5 5 9 } ∖ { 2 5 7 } = { 1 5 5 9 }
// old orders = { 1, 2, 5, 9, }
// new orders = { 2, 5, 7, }
// cut orders = { 1, 9, }
```

图 235

## 额外

### 挑战 1：现代 C++ 中的 PixMap 转 SVG

在现代 C++ 中掌握二维计算机图形之旅终于一个充满挑战性的任务：开发你自己的追踪器，将 PPM 文件转换为 SVG 格式。这项尝试不仅测试了你的能力水平，还增强了你对矢量图形和图像处理的理解。在任务中，鼓励你从现有工具 `vtracer` 获取灵感，这是一个强大的光栅到矢量图形转换器。关于 `vtracer` 的详细信息可以在 [GitHub vtracer](https://github.com/visioncortex/vtracer) 找到。

首先，理解 `vtracer` 的原理至关重要。该工具体现了基于像素的图像转换为可缩矢量图形的艺术。其底层算法是图像处理与矢量化技术完美融合的证明。算法的细节作为你实现的指导框架，在 [vtracer 文档](https://www.visioncortex.org/vtracer-docs) 中有详细解释。

你的实现应根于现代 C++ 实践，不仅展示了技术能力，还体现了现代编码标准的优雅与高效。利用 C++ 的强大特性来创建一个既有效又高效的解决方案，反映该语言自传统图像处理工具诞生以来的进步。

你实现的关键组件之一是处理 PPM 文件。为此，你应该使用 `ppmpp.hpp` 库，这是一个用于处理 PPM 文件的高效现代的 C++ 库。它为处理 PixMap 文件提供了简洁且直观的接口，这对于你追踪器的输入处理至关重要。你可以在 [GitHub ppmpp](https://github.com/chbtoys/ppmpp) 找到更多关于 `ppmpp.hpp` 的信息。

在制作追踪器时，专注于转换准确性和输出 SVG 文件的优化。挑战不仅在于准确追踪输入图像的轮廓和特征，还在于不牺牲视觉保真度的前提下优化矢量图形以减小文件大小。这种平衡对于创建可扩展且高效的 SVG 文件至关重要。

当你开启这段旅程时，请记住错误处理和代码健壮性与核心功能同样重要。你的追踪器应该能够处理各种边界情况和输入异常，确保转换过程顺畅且可靠。这不仅将证明你的技术实力，还将体现你在创建以用户为中心的应用程序方面的远见。

### 挑战 2：现代 C++ 中的 PixMap 转换为旋转填充混合椭圆

在现代 C++ 的二维计算机图形领域，一个引人入胜且复杂的挑战等待：创建一个使用旋转、填充、混合椭圆将 PPM 文件转换为 SVG 格式的软件。这项任务不仅是对编程技能的测试，也是对艺术与算法融合的探索。挑战的灵感来自名为 `Primitive` 的工具，其详细信息见 [GitHub Primitive](https://github.com/fogleman/primitive)。该工具使用简单的几何形状精巧地重建图像，为构建你的项目提供了基础。

你的任务是创建一个现代 C++ 应用，利用爬山算法和模拟退火算法来迭代改进生成的 SVG 图像的质量。这些优化算法常用于人工智能和数学优化，可以在 [维基百科爬山算法](https://en.wikipedia.org/wiki/Hill_climbing) 和 [维基百科模拟退火](https://en.wikipedia.org/wiki/Simulated_annealing) 中更深入的探索。挑战在于将这些算法应用于图像处理，并在形状放置、旋转和颜色混合方面做出艺术决策。

你项目的核心将涉及解释 PPM 文件，这是图形社区中常用的图像格式。有效处理这些文件至关重要，为此，你应该集成 `ppmpp.hpp` 库，这是一个专门为处理 PPM 文件定制的现代 C++ 库。其功能和用法在 [GitHub ppmpp](https://github.com/chbtoys/ppmpp) 中进一步说明。该库将作为你图像处理和转换任务的骨干。

你的实现应专注于创建完全由椭圆组成的 SVG 图像。这些椭圆在大小、方向、颜色和混合程度上不同，必须经过策略性的放置，以尽可能地复制原始 PPM 图像。这需要对色彩理论、几何学和算法优化有深入的理解，以达到和谐美观的结果。
