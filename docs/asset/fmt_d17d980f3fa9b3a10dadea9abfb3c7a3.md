
```c
void write_image(char *filename, struct image *img)
{
    struct pam *pam = &img->pam;
    pam->file = pm_open(filename);
    if (pam->file)
        if (pam->format == PGM_FORMAT || pam->format == PPM_FORMAT) ? 1 : 0;
        pnm_writepaminit(pam);
        if (pam->format == PGM_FORMAT || pam->format == PGM_FORMAT)
            write_image_pixel_data(img);
        else if (pam->format == PPM_FORMAT || pam->format == PPM_FORMAT)
            write_image_pixel_data(img);
        else {
            fprintf(stderr, "error: file %s, line %d: shouldn't be here!\n", FILE__, __LINE__);
            exit(EXIT_FAILURE);
        }
    pm_close(pam->file);
}
```

第 3 行。正如我们在 `read_image()` 中所做的那样，我们引入变量 `pam` 作为 `&img->pam` 的简写。这并非必须；仅仅是为了减少杂乱。

第 4 行。在这里我们调用第 14.5 节描述的 `libnetpbm/pm_open()` 函数打开文件写入。我们本可以调用 C 标准的 `fopen()`，例如

```c
FILE *fp = fopen(filename, "w");
```

但正如第 14.5 节所述，`pm_open()` 提供了几个额外的有用功能。其，它将名为 "-" 文件处理为标准输出 `stdout` 的请求；其，它会检查错误。如果无法打开请求的文件写入，它会向 `stderr` 打印消息并退出程序！因此，没有必要检查 `pm_open()` 调用的成功。注意我们将 `pam->file` 设置为 `pm_open()` 打开的流。其他向流写入的函数会在 `pam` 结构中查找流地址。

第 5 行。正如第 14.5 节所述，`libnetpbm` 格式化 `pam` 结构中 `format` 成员的编码，并默认以原始格式写入图像。在这里我们检查它是否表示普通格式 `plain format`，如果是，我们设置覆盖库的默认行为。

第 7 行。第 14.5 节描述的 `libnetpbm/pnm_writepaminit()` 函数通过从 `pam` 结构中提取所需信息写入图像头数据，例如第 14.3.2 节描述的“P5 w h M”部分。输出到流 `pam->file`。

## 列表 14.8：函数 `write_pgm_pixel_data()` 的实现。

```c
1 static void write_pgm_pixel_data(struct image *img)
2 {
3     struct pam *pam = &img->pam;
4     tuple *row = pnm_allocpamrow(pam);
5     for (int i = 0; i < pam->height; i++) {
6       for (int j = 0; j < pam->width; j++) {
7           row[j][0] = img->g[i][j];
8       }
9       pnm_writeprow(pam, row);
10  }
11}
12 }
```

第 8 行。此处程序根据图像类型进行分支。如果图像是 `PGM` 类型，我们调用 `write_pgm_pixel_data()` 来写入像素数据。如果图像是 `PPM` 类型，我们调用 `write_ppm_pixel_data()` 来写入像素数据。`这些函数稍后会描述。`除非我们仔细干预 `pam` 结构的格式，否则这些应该是唯一的可能性。任何其他情况都是异常的且不应该发生。然而，我们提供了代码以捕获假设的情况。

第 17 行。我们完成了写入；因此我们调用第 14.5 节描述的 `pm_close()` 关闭输出流。`pm_close()` 函数是 C 标准 `fclose()` 的封装——它会检查 `fclose()` 的状态并在发生错误时调用 `exit()`。

### 14.8.4 - 函数 `write_pgm_pixel_data()`

出现在列表 14.4 第 10 行的 `write_image()` 函数与 `read_pgm_pixel_data()` 有许多共同点，其实现如列表 14.8 所示。让我们详细查看细节。

第 3 行。在这里引入变量 `pam` 的原因与列表 14.5 的第 4 行相同。它不是必须的，但为了减少杂乱的简写。

第 4 行。在这里我们调用第 14.5 节描述的 `libnetpbm/pnm_allocrow()` 函数来为行数组分配内存。我们将一次读取一行图像，然后将结果拷贝到矩阵中。图 14.4 显示了行数组的表示。不需要检查——如果内存分配失败，`pnm_allocrow()` 将向 `stderr` 打印消息并退出程序。

第 5 行和第 6 行。我们调用 `array.h` `见第 8 章` 中的 `make_matrix()` 宏来分配一个双精度矩阵，并赋值给 `img->g`，以存储 `pam->height x pam->width` 的像素数据。`img->r` 和 `img->b` 成员用于 `PPM` 图像，因此不需要。我们将它们设置为 `NULL`，这样它们就可以传递给 `free_matrix()` 而不产生影响；参见第 14.8 节。

第 7 到 11 行。`for` 循环每次处理图像的一行。在每一步中，它都调用第 14.5 节描述的 `libnetpbm/pnm_readrow()` 函数将整行读入数组。因此，`row[j]` 指向 `i` 行 `j` 列的元组。由于这是 `PGM` 图像，元组长度为 1 `见图 14.4`；其第一个也是唯一的 元素由 `row[j][0]` 提供。我们将该值存储在 `img->g[i][j]` 中。

第 12 行。我们完成了读取。我们调用第 14.5 节描述的 `libnetpbm/pnm_freeprow()` 函数来释放第 4 行分配的内存。

备注 14.6。注意 `img->g[i][j]` 是 `double` 类型，而 `row[j][0]` 是 "sample" 类型，它是 `unsigned long` 的别名。在赋值时应用了 C 的自动转换规则。如果右侧是存储为 `double` 的整数，那么左侧将接收该整数的值。如果是非整数，其小数部分将被丢弃。例如，3.1 和 3.9 都被转换为 3；没有进行舍入。在到达此处之前，对图像采样值进行所有必要的舍入/处理是调用者的责任。特别是，调用者的责任是确保

## 14.9. 文件 `image-io-test-0.c`

列表 14.9：文件 `image-io-oc.c` 中 `free_image()` 的实现。

```c
void free_image(struct image *img)
{
    if (img != NULL) {
        free_matrix(img->r);
        free_matrix(img->g);
        free_matrix(img->b);
        free(img);
    }
}
```

样本值处于 0 到 M 的范围内，其中 M 是图像的最大样本值。在第 15 节小波在图像分析中的应用中，我们在调用 `write_pgm_pixel_data()` 之前处理了这些细节。这就是第 15.6.2 节中引入的 `clip_matrix()` 函数的目的。

第 8 行。第 14.5 节描述的函数 `pnm_writeppamrow()` 将图像的一整行的像素数据写入输出流。

第 10 行。在这里，`free()` 释放了之前在第 4 行分配的行向量相关的内存。

## 14.8.5 函数 `free_image()`

出现在列表 14.4 `第 124 页` 第 11 行的函数 `free_image()` 释放与“`struct image`”相关的内存资源。列表 14.9 显示的实现非常直观。它释放了以下内容：

- * 在 `read_pgm_pixel_data()` 或 `read_ppm_pixel_data()` 中分配的与矩阵 `img->r`、`img->g`、`img->b` 内存；参见第 126 页列表 14.6 的第 5 行。
- * 在 `read_image()` 中分配的与 `img` 结构相关的内存；参见第 124 页列表 14.5 的第 3 行。

与书中所有其他 `free-*` 函数以及标准库的 `free()` 一样，带有 `NULL` 参数调用 `free_image()` 是安全的。

备注 14.7。在列表 14.6 第 6 行将 `img->r` 和 `img->b` 指针赋值为 `NULL` 的意义。我们在 `array.h` 中的 `free_matrix()` 的实现是为了优雅地处理 `NULL` 参数。

## 14.9. 文件 `image-io-test-0.c`

列表 14.10 所示的文件 `image-io-test-0.c` 为测试 `image-io` 模块提供了驱动程序。它只需读取一个 `PGM` 或 `PPM` 图像 `纯格式或原始格式` 并不做更改地写入，但任何嵌入的注释会被丢弃。输入和输出文件的文件名从 `argv[1]` 和 `argv[2]` 获取。因此，它的调用方式如下

```bash
$ image-io-test-0 infile outfile
```

## 列表 14.10：完整显示的文件 `image-io-test.c` 为测试 `image-io` 模块提供了驱动程序。它读取一个 `PGM` 或 `PPM` 文件并不做更改地写入，嵌入的注释除外。输入和输出文件的文件名从 `argv[1]` 和 `argv[2]` 获取。

```c
#include <stdio.h>
#include "image-io.h"
int main(int argc, char **argv) {

    if (argc < 3) {
        fprintf(stderr, "Usage: %s outfile\n", argv[0]);
        fprintf(stderr, "Reads PGM or PPM from infile, ");
        // writes image to output\n
        return EXIT_FAILURE;
    }

    pm_init(argv[0], 0);
    struct image *img = read_image(argv[1]);
    fprintf(stderr, "image is %dx, depth=%d, maxval=%d\n",
           img->height, img->width);
    pm_max(img, (int)img->maxval);

    write_image(argv[2], img);
    free_image(img);
    return EXIT_SUCCESS;
}
```

第 14.7 节关于调用细节。以下是 `image-io-test.c` 的逐行描述：

第 5 行。我们期望程序带有两个参数调用。因此 `argc` 应该是 3 `参见第 4.7 节`。`argv[0]` 是程序名，`argv[1]` 是输入图像，`argv[2]` 是输出文件。如果 `argc` 不是 3，我们向 `stderr` 打印消息并退出。

第 11 行。如第 14.5 节所述，每个库程序预期调用 `pm_init()` 来初始化库。`pm_init()` 的第一个参数应该是程序名。第二个参数始终为零。

第 12 行。函数 `read_image()` `参见 14.8.1` 读取对应 `argv[1]` 的图像。当它返回时，所有内容都存储在 `img` 结构中。在 C99 中允许声明 `struct image` 但 C89 不允许。如果你想将代码改为 C89，请在顶部插入声明 `struct image *img;` 并当前行改为 `img = read_image(argv[1]);`

第 13 行。我们将图像的数据作为反馈给用户。`PGM` 图像的 `depth` 值为 1，而 `PPM` 图像为 3。

第 16 行。函数 `write_image()` `参见 14.8.3` 将 `img` 结构中的图像写入对应 `argv[2]` 的文件。

第 17 行。我们调用 `free_image()` `参见 14.8.5` 释放与图像相关的内存然后退出。

## 14.10 项目 I/O

**部分 14.1**。完成、编译并测试第 14.6 节的最小程序。

**部分 14.2**。在前面的节中，我提供了读写 `PGM` 图像的完整代码。添加处理 `PPM` 图像的功能来完成 `image-io` 模块。这需要实现 `read_ppm_pixel_data()` 和 `write_ppm_pixel_data()`；参见第 120 页列表 14.4。

**部分 14.3**。使用我在网站上的一些 `PGM` 和 `PPM` 图像编译并测试 `image-io-test-0`。例如：

```bash
$ image-io-test-0 matsura.pgm z0.pgm
image is 512x512, depth=1, maxval=255
```

程序读取 `matsura.pgm` 并写入新文件 `z0.pgm`。由于我们没有修改图像，这两个文件应该是相同的。你可以应用 Unix 工具 `cmp` 来验证文件是否确实相同：

```bash
$ cmp matsura.pgm z0.pgm
```

如果文件进行了比较，`cmp` 会打印差异字节的位置。如果文件相同，`cmp` 静默退出。

> 备注 14.4。`image-io-test` 的输入和输出文件并不是相同的。在图像格式描述中——例如第 14.3.2 节——注意可能会插入可选的注释和空格。我们的 `read_image()` 函数在读取时会丢弃注释。相同的图像不需要相同的文件，因为它们的头部部分可能不同。尽管如此，网站上的图像文件没有注释 `除了标记的那一个`，且空格符合 `libppm` 工具的标准；因此你的 `matsura.pgm` 和 `z0.pgm` 应该是相同的。如果不是，你的程序有 Bug。

**部分 14.4**。`[可选]` 写一个程序 `image-io-test-1.c`，将 `彩色` `PGM` 图像转换为 `灰度` `PGM` 图像。我建议你使用列表 14.10 中的 `image-io-test.c` 副本进行测试。在读取图像 `第 12 行` 和写入图像 `第 16 行` 之前：

```c
img->format = RGB_FORMAT;
img->depth = 1;
```

这会将图像输出设置为原始 `PGM`，图像深度设置为 1，因为 `PGM` 的像素值通过单个数字识别。现在，遍历图像，并在每个像素处：

```c
double avg = (img->r[i][j] + img->g[i][j] + img->b[i][j])/3.0;
img->g[i][j] = (int)(0.5 + avg);
```

在第一行，我们计算像素的红、绿、蓝值。平均值不一定是整数；然而，`PGM` 预期像素值为整数。因此，在第二行中，我们在赋值给 `img->g[i][j]` 之前将其转换为 `int`。注意将 `double` 转换为 `int` 会丢弃小数部分。加上 0.5 可以确保正确的四舍五入。例如，如果 `avg` 是 3.1，那么 0.5 + 3.1 是 3.6，在丢弃小数部分后减为 3。另一方面，如果 `avg` 是 3.9，那么 0.5 + 3.9 是 4.4，在丢弃小数部分后变为 4。

**部分 14.5**。`[可选]` RGB 值的直化似乎可行，但效果并不好。事实上，人眼对红、绿、蓝光度的敏感度并不相等。经验表明，对绿色分量赋予更大的权重会产生更自然的视觉。`Libppm` 的例程按照 77:150:29 的比例混合红、绿、蓝，尽管这不是硬性的快速事实。将 `image-io-test-1.c` 复制到 `image-io-test-2.c`，并使用以下平均公式：

```c
double avg = (77*img->r[i][j] + 150*img->g[i][j] + 29*img->b[i][j])/256.0;
```

**部分 14.6**。`[可选]` 图像查看程序 `Xv` 按照 20:32:150 的比例平均红、绿、蓝。将 `image-io-test-2.c` 复制到 `image-io-test-3.c`，并根据以下算法进行平均：

**部分 14.7**。`[可选]` 将 `image-io-test-0.c` 复制到 `image-io-test-4.c`。修改使其“旋转” `PPM` 图像的颜色。即将红色写入绿色矩阵，绿色写入蓝色矩阵，蓝色写入红色矩阵。查看生成的图像。

**部分 14.8**。`[可选]` 写一个程序文件 `image-io-test-5.c`，在图像的对角线上画一个“X”。对角线 $D_i$ 所在的

# Chapter 15

# Image analysis

Prerequisites: Chapters 7, 8, 13, 14

## 15.1 Introduction
