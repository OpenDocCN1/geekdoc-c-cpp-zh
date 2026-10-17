
# 21.5.1.2 使用 CubeMX 配置闪存器接口

CubeMX 简化了访问闪存器（TCM/AXI）、ART™ 加速器以及 `Cortex-M7` L1 缓存的总线配置。通过进入引脚视图部分并点击 `Cortex-M7` 项，配置这些参数，如图 21.7 所示。

![](img/9ef247bc7328ae96d937b3818a681558_585_0.png)

图 21.7：CubeMX 中的 `Cortex-M7` 配置视图

请注意，在编写本章时（2021 年 10 月），生成的链接脚本是错误的，因为它没有像上段所示那样指定不同的 LMA 和 VMA 地址。

# 22. 启动过程

在第 20 章中，我们看到复位异常的处理程序对应于第一个例程。复位异常的处理程序通过使用表 21.7 和 21.8 中报告的基地址对 `.text`、`.bss` 和 `.data` 区域的地址进行重映射，这显然是链接脚本的工作。

然而，这种操作无法通过更改链接脚本内部 `FLASH` 区域的起始地址来轻松完成。这是因为前面提到的，不允许通过 `TCM` 接口进行写模式的访问。这意味着 `ST-LINK` 调试器或任何等效调试器都无法使用地址范围 `0x0020 0000 - 0x002F FFFF` 加载程序。为了解决这一局限性，我们需要将 VMA 地址范围与 LMA 分离开，就像我们对 `.data` 区域所做的那样。例如，下面的链接脚本片段显示了如何执行此操作。

```c
/* 指定内存区域 */
MEMORY {
  ITCM_FLASH (rx): ORIGIN = 0x00200000, LENGTH = 1024K
  AXI_FLASH (rx): ORIGIN = 0x08000000, LENGTH = 1024K
  RAM (rwx): ORIGIN = 0x20000000, LENGTH = 320K
}

/* 定义输出段 */
SECTIONS {
  /* 启动代码进入第一个 FLASH */
  .isr_vector :
    = ALIGN(4);
    KEEP(*(.isr_vector)) /* 启动代码 */
    = ALIGN(4);
  } ITCM_FLASH AT:AXI_FLASH
}
```

```c
/* 程序代码和其他数据进入 FLASH */
.text :
{
    = ALIGN(4);
    (.text)      /* .text 段（代码） */
    (*text*)     /* .text* 段（代码） */

    KEEP (*.init)
    KEEP (*.fini)

    = ALIGN(4);
    .etext = .;    /* 在代码结束定义全局符号 */
} ITCM_FLASH->AXI_FLASH
```

```c
/* 常量数据进入 FLASH */
.rodata :
{
    = ALIGN(4);
    (.rodata)    /* .rodata 段（常量、字符串等） */
    (.rodata*)   /* .rodata* 段（常量、字符串等） */
    = ALIGN(4);
} ITCM_FLASH->AXI_FLASH
```

如你所见（第 17、31 和 40 行），VMA 地址（即 CPU 用于取指程序代码的地址）被映射到 `ITCM-FLASH` 接口，而 LMA 地址范围（即用于在闪存器中存储程序的地址范围）映射到 `AXI` 接口，这允许以写模式访问闪存器。
