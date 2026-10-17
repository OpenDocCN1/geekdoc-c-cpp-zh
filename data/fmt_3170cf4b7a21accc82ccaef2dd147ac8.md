
> **备注 14.4.** 为什么 `struct image` 中的 $r, g, b$ 矩阵类型是 `double`？像素值数是 $0$ 到 $M$ 范围内的整数（通常 $M$ 为 $2^{15}-1$）。在 `unsigned char` 类型的矩阵中存储这些值不是更自然吗？在坏情况下，当 $M$ 为 $2^{16}-1 = 65535$ 时，`unsigned short int` 类型的矩阵就足够了。这些观察是有效的。然而，图像的存储类型取决于应用程序。我使用 `double` 存储是为了考虑到小波变换图像分析的应用，这是下一章的主题。我们用相应的小波变换覆盖图像矩阵，而那不再是整数矩阵。如果你的应用程序没有对图像进行此类操作，可以随时在 `image-io.h` 中将 `double` 改为 `unsigned char` 或 `unsigned short int`。

`image-io` 模块依赖 `xmlalloc` 模块（第 7 章）进行内存分配，依赖 `array.h` 头文件（第 8 章）构建矩阵。因此，遵循第 2 章的建议，项目目录将包含：

列表 14.2：`libnetpm-minimal.c` 文件提供了 libnetpm 函数的精简演示。它将一个 PGM 图像读入矩阵，在其上方画一条黑线，并将结果写入另一个 PGM 文件。对 libnetpm 函数的调用位于阴影背景中。

```
#include <stdio.h>
#include <pam.h>
#include <array.h>
int main(int argc, char **argv) {
    char *infile = "aya_matsuura.pgm";
    char *outfile = "zz.pgm";
    struct pam *pam;
    FILE *fp;
    double **matrix;
    tuple *row;
    int i, j;

    pnm_init(argv[0], 0);
    // read image header
    fp = pam_fopen(infile, PAM_STRUCT_SIZE(tuple));
    printf("image: %dx, %d\n", pam->width, pam->height);
    if (!pam->format == PGM_FORMAT || pam->format == RPGM_FORMAT) {
        fprintf(stderr, "Error, this demo handles PGM images only.\n");
        return EXIT_FAILURE;
    }

    make_matrix(a, pam->width, pam->height); // matrix to store image data
    row = pnm_allococrow(&pam); // tuplevector
    for (i = 0; i < pam->height; i++) {
        pmn_readpamrow(&pam, row);
        for (j = 0; j < pam->width; j++) { // copy tuple into matrix
            a[i][j] = row[j][0];
        }
    }

    pm_close(fp);
    for (i = 0; i < pam->height; i++) {
        a[i][j] = 0.0; // change pixels to black
    }

    // write image header
    fp = pam_open(outfile);
    pam->plainformat = pam->format == PGM_FORMAT; 
    pmn_writepaminit(&pam);

    for (i = 0; i < pam->height; i++) { // write data
        for (j = 0; j < pam->width; j++) {
            row[j][0] = a[i][j];
            pmn_writepamrow(&pam, row);
        }
    }

    pm_close(fp);
    free_matrix(a);
    frerow(row);
    return EXIT_SUCCESS;
}
```

列表 14.3：`image-io.h` 文件。

```c
#ifndef IMAGE_IO_H
#define IMAGE_IO_H
#include <pam.h>
struct image {
    struct pam;
    double **r;
    double **g;
    double **b;
};
struct read_image(char *filename, struct image *img);
void write_image(char *filename, struct image *img);
void free_image(struct image *img);
#endif /* IMAGE_IO_H */
```

```
$ cd image-io
$ ls -F
Makefile image-io image-test-3.c libnetpm-minimal.c
array.h image-test-4.c xmalloc.c
image-test-0.c image-test-5.c xmalloc.h
image-test-1.c image-io.c
image-test-2.c image-io.h
```

独立的 `image-io` 模块包含在 `image-io` 文件中。`image-test-{5}.c` 文件是演示各种功能的驱动程序，稍后会描述。它们编译为名为 `image-test-{5}` 的可执行文件。每个可执行文件带有两个参数调用：

```
$ image-test 0 outfile
```

程序从 `infile` 读取，以某些方式修改图像，并将修改后的图像写入输出。你可以自定义输入输出文件名，但 PGM 和 PPM 格式的图像习惯使用 `.pgm` 和 `.ppm` 扩展名。程序并不依赖文件名来确定图像格式，而是通过文件中嵌入的数字检测。

**备注 14.5.** 在第 14.5 节中 libnetpm 的 `pm_fopen()` 和 `pm_open()` 函数描述里，我们注意到这些函数将特殊名称 `"-"` 视为 `stdin` 或 `stdout` 的引用。因此，程序也可以调用：

```
$ image-test - outfile.pgm < infile.pgm
```

或者更简单：

```
$ image-test - < infile.pgm > outfile.pgm
```

这些在文件视为字节流的 Unix 或类 Unix 系统有效。在像 Windows 这样区分文本二进制文件的操作系统上，重定向可能会损坏原始图像。

列表 14.4：`image-io.c` 文件的 outline。

```c
#include <stdio.h>
#include <stdlib.h>
#include <array.h>
#include "image-io.h"
static void read_pgm_pixel_data(struct image *img) ...
static void read_ppm_pixel_data(char *filename, struct image *img) ...
static struct image read_image(char *filename) ...
static void write_pgm_pixel_data(struct image *img) ...
static void write_ppm_pixel_data(struct image *img) ...
void write_image(char *filename, struct image *img) ...
void free_image(struct image *img) ...
```

列表 14.5：`read_image()` 函数的实现。

```c
struct image read_image(char *filename)
{
    struct image *img = xmalloc(sizeof(*img));
    struct pam *pam = &img;
    FILE *fp = pm_open(filename);
    prm_read_header(fp, pam, PAM, PGM_STRUCT_SIZE(type_tuple));
    if (pam->format == PGM_FORMAT || pam->format == RPGM_FORMAT)
        read_pgm_pixel_data(img);
    else if (pam->format == PPM_FORMAT || pam->format == RPPM_FORMAT)
        read_ppm_pixel_data(img);
    else {
        fprintf(stderr, "error: file '%s' contains neither\n                a PGM nor a PPM image\n", filename);
        exit(EXIT_FAILURE);
    }
    pm_close(fp);
    return img;
}
```

## 14.8 - image-io 模块的实现

列表 14.4 显示了 `image-io.c` 文件的 outline。我将提供处理 PGM 图像部分的细节。你将编写处理 PPM 图像的部分。

### 14.8.1 - `read_image()` 函数

出现在列表 14.4 第 7 行的 `read_image()` 函数接收一个现有图像文件的名称。它读取文件内容，为 `struct image` 结构及其成员分配内存，用图像数据填充该结构体，并返回该指针。如果过程中发生任何错误，它会向 `stderr` 打印诊断消息并调用 `exit` 杀死程序。列表 14.5 显示了我对 `read_pgm_image()` 的实现。它处理 PGM 和 PPM 图像，包括纯格式和原始格式。

## 14.8. image-io 模块的实现

让我们详细查看 `read_image()` 函数。

第 3 行。我们为“struct image” 分配内存，并将 `img` 设置为 pam 内存。当前函数的目的是从输入文件中读取数据，将这些信息存入该结构体，并将结构体的地址返回给调用者。

第 4 行。指针 `&img->pam` 在后续代码的很多地方都需要用到。到处都写 `&img->pam` 并没有错，但会让代码变得杂乱。在这里定义的 `pam` 变量是为了减少杂乱而使用的简写；这样做并不是必须的。

第 5 行。我们调用了第 14.5 节描述的 `libnetpbm/pm_open()` 函数来打开图像文件进行读取。我们本可以调用 C 标准的 `fopen()`，例如

```c
FILE *fp = fopen(filename, "r");
```

但正如第 14.5 节所述，`pm_open()` 提供了几个额外的有用功能。其，它将文件名 `"-"` 处理为对标准输入（stdin）的请求，如第 123 页示例 14.5 中的用法所示。其二，它会检查错误。如果无法打开请求的文件读取，它会向 stderr 打印消息并退出程序！因此，没有必要检查 `pm_open()` 调用的成功。

第 6 行。我们调用了第 14.5 节描述的 `libnetpbm/pnm_readinit()` 函数来读取图像头数据。第一个参数是流 `fp`，它是在上一行设置的。嵌入在“struct image”中的“struct pam”。该函数将用从图像头中提取的信息填充 `pam` 成员（参见列表 14.1）。第三个参数，正如第 14.5 节所述，始终是我展示的那个表达式。此外，正如那里提到过的样，如果你使用的是旧版本的 libnetpbm，可能需要将其更改为 `sizeof(struct pam)`。

第 7 行。此处程序根据图像类型进行分支。“struct pam”结构中的 `format` 成员编码了刚刚从输入流中读取的图像类型（“struct pam”的细节请见第 14.5 节）。如果图像是 PGM 类型，我们调用 `read_pg_pixel_data()` 来读取像素数据。如果图像是 PPM 类型，我们调用 `read_ppm_pixel_data()` 来读取像素数据。这些函数稍后会描述。如果图像是其他类型——可能是 PBM 或 PAM——那么我们就打印一条消息说我们未准备好处理该类型并退出程序。

第 16 行和第 17 行。我们完成了图像读取；因此我们关闭输入流并将 `img` 返回给调用者。第 14.5 节描述的 `pm_close()` 函数是 C 标准 `fclose()` 的封装——它会检查 `fclose()` 的状态，并在发生错误时调用 `exit()`。

> ⁴我之前从未提到过 PAM 格式，之后也再也不会处理它。PAM 是一种“可适应”格式，从这个意义上说，任何 PBM、PGM 或 PPM 图像都可以呈现为 PAM 图像。如果你想了解更多关于该格式的信息，需要阅读 Netlib 的文档。

## 列表 14.6：函数 read_pgm_pixel_data() 的实现。

```c
1 static void read_pgm_pixel_data(struct image *img)
2 {
3     struct pam *pam = &img->pam;
4     tuple *row = pnm_allocpamrow(pam);
5     make_matrix(img->g, pam->height, pam->width);
6     img->r = NULL;
7     for (int i = 0; i < pam->height; i++) {
8         pnm_readprow(pam, row);
9         for (int j = 0; j < pam->width; j++) {
10            img->g[i][j] = row[j][0];
11        }
12    pnm_freeprow(row);
13 }
```

### 14.8.2 - 函数 read_pgm_pixel_data()

出现在列表 14.6 第 5 行的 `read_pgm_pixel_data()` 函数读取 PGM 图像的像素数据。其实现如列表 14.6 所示。让我们详细查看细节。

第 3 行。在这里引入变量 `pam` 的原因与列表 14.5 的第 4 行相同。它不是必须的，但为了减少杂乱的简写。

第 4 行。在这里我们调用了第 14.5 节描述的 `libnetpbm/pnm_allocrow()` 函数来为行数组分配内存。我们将一次读取一行图像，然后将结果拷贝到矩阵中。图 14.4 显示了行数组的表示。不需要检查——如果内存分配失败，`pnm_allocrow()` 将向 stderr 打印消息并退出程序。

第 5 行和第 6 行。我们调用了 `array.h`（见第 8 章）中的 `make_matrix()` 宏来分配一个双精度矩阵，并赋值给 `img->g`，以存储 (pam->height x pam->width) 的像素数据。`img->r` 和 `img->b` 成员用于 PPM 图像，因此不需要。我们将它们设置为 `NULL`，这样它们就可以传递给 `free_matrix()` 而不产生影响；参见第 14.8 节。

第 7 到 11 行。`for` 循环每次处理图像的一行。在每一步中，它都调用第 14.5 节描述的 `libnetpbm/pnm_readrow()` 函数将整行读入数组。因此，`row[j]` 指向 i 行 j 列的元组。由于这是 PGM 图像，元组长度为 1（见图 14.4）；其第一个（也是唯一的）元素由 `row[j][0]` 提供。我们将该值存储在 `img->g[i][j]` 中。

第 12 行。我们完成了读取。我们调用第 14.5 节描述的 `libnetpbm/pnm_freeprow()` 函数来释放第 4 行分配的内存。

### 14.8.3 - 函数 write_image()

出现在列表 14.4 第 10 行的 `write_image()` 函数接收一个文件名和一个“struct image”。它以 PGM 或 PPM 图像的形式写入命名文件。如果指定的文件不存在，则创建它。如果存在，则进行覆盖。如果过程中发生任何错误，它会向 stderr 打印诊断消息并退出程序。列表 14.7 显示了 `write_image()` 的实现。

## 列表 14.7：函数 write_image() 的实现。
