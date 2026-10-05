
以及 `ofstream` 对象。虽然不太方便，但 C 语言中简单直接的 `fread()`、`fwrite()` 接口要快得多，差异可达 100 倍。在 4.3.1 节中，我们将解释为什么速度上会有如此巨大的差异。

在 4.3.2 和 4.3.3 节中，我们研究了 DRAM 内存的延迟和带宽。在这节中，内核内核维护的页缓存（page cache）都起了重要作用。页缓存是维护在主内存中的磁盘缓存。DRAM 内存可以达到 TB 级，而页缓存可以占据该内存很大一部分。许多文件输入/输出是通过操作系统内核使用页缓存来服务的。为了获取磁盘延迟和带宽的真实情况，需要跳过页缓存，并意味着数百 GB 级的文件大小。

磁盘延迟在毫秒级，因此可能是 DRAM 内存延迟的 10⁶ 倍。磁盘带宽在数百 MB/s 数量级，这是典型计算机上 DRAM 带宽的千倍。然而，典型计算机的硬盘容量可以是 DRAM 容量的 100 倍甚至 1,000 倍。在硬盘容量方面，许多超级计算系统（以及高端工作站）并没有良好的平衡。为许多用户跨许多计算机提供一个公共文件系统的需求，意味着硬盘容量没有达到理想水平。

## 4.3.1 C 优于 C++

关于读写文件的编程技术，最简单的技巧往往最有价值。正如我们所展示的以及我们所解释的原因，C 接口可以比 C++ 接口快得多。

以下函数使用 C++ `ofstream` 从名为 `filename` 的文件中读取或向其写入一个 `double` 数组 `v[]`。

```cpp
void write_easy(double *, long len, const char *fname){
    ofstream ofile(fname);
    ofile<<scientific;
    ofile.precision(16);
    for(long i=0; i < len; i++)
        ofile<<v[i] << endl;
    ofile.close();
}
```

## 4.3 从磁盘读写和写入

```cpp
void read_easy(double *v, long len, const char *fname){
    ifstream infile(fname);
    for(long i=0; i < len; i++)
        infile >> v[i];
}
```

下方的 C 接口可以快 100 倍以上。

```cpp
#include <cstdio>
void write_direct(double *v, long len, const char *fname){
    FILE *fptr;
    fptr = fopen(fname, "w");
    fwrite((void *)v, len, sizeof(double), fptr);
    fclose(fptr);
}

void read_direct(double *v, long len, const char *fname){
    FILE *fptr;
    fptr = fopen(fname, "r");
    fread((void *)v, len, sizeof(double), fptr);
    fclose(fptr);
}
```

`FILE` 类型以及 `fopen()`、`fwrite()`、`fread()` 函数在第 1 行包含的 `stdio.h` 头文件中声明。第 5 行打开了一个文件用于写入，第 13 行打开了一个用于读取。

库函数 `fwrite()`（第 6 行）的接口非常简单。它的第一个参数是指向内存位置的指针。第二个参数是要写入的项数，第三个参数是每个项目的字节大小。最后一个参数是指向文件的指针。

库函数 `fread()`（第 14 行）具有相同的接口。它返回读取的项数，如果发生错误，该值可能小于请求的数量。按照我们通常的习惯，我们不检查错误情况。打开的文件使用 `fclose()` 关闭（第 7 行和 15 行）。

为什么 C++ 接口要慢 100 倍以上？有三个原因。

首先，C++ 接口在处理流时会产生额外的开销。

其次，C++ 接口在将 `double` 转换为 ASCII 格式时产生了开销。

第三，C++ 接口在读写时使用了缓冲区，相比之下，C 库直接以二进制格式操作。

## 4.3.2 磁盘延迟

磁盘延迟在毫秒级，因此可能是 DRAM 内存延迟的 10⁶ 倍。磁盘带宽在数百 MB/s 数量级，这是典型计算机上 DRAM 带宽的千倍。然而，典型计算机的硬盘容量可以是 DRAM 容量的 100 倍甚至 1,000 倍。在硬盘容量方面，许多超级计算系统（以及高端工作站）并没有良好的平衡。为许多用户跨许多计算机提供一个公共文件系统的需求，意味着硬盘容量没有达到理想水平。

## 4.3.3 磁盘带宽

```cpp
struct disk_latency {
    double fopen_cycles;
    double seek_cycles;
    double read_cycles;
    double close_cycles;
};

void latencydisk(const char *dir, int filenum, long pos, disk_latency &lat){
    char fname[20];
    sprintf(fname, "%s/file%d.dat", dir, filenum);
    Timestamp clk;
    FILE *fptr;
    clk.tick();
    fptr = fopen(fname, "r");
    lat.fopen_cycles = clk.toc();
    clk.tick();
    fseek(fptr, pos, SEEK_SET);
    lat.seek_cycles = clk.toc();
    double x;
    clk.tick();
    fread(&x, sizeof(double), 1, fptr);
    lat.read_cycles = clk.toc();
    clk.tick();
    fclose(fptr);
    lat.close_cycles = clk.toc();
}
```
