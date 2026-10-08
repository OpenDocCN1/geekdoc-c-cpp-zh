

# 嵌入式 C 编码规范

```c
/*!
 * @brief 逐位计算字节数组的 CRC。
 * @param[in] p_message  指向待要计算 CRC 的数据字节数组的指针。
 * @param[in] n_bytes      数据数组中的字节数。
 * @return 数据数组的 CRC 结果。
 */
```

```c
crc_t
crc_slow(uint8_t const * p_message, int n_bytes)
{
    crc_t remainder = INITIAL_REMAINDER;

    // 执行模 2 除法，每次处理一个字节。
    for (int byte = 0; byte < n_bytes; ++byte)
    {
        // 将下一个字节带入余数中。
        remainder ^= (REFLECT_DATA(p_message[byte]) << (WIDTH - BITS_PER_BYTE));

        // 执行模 2 除法，每次处理一个位。
        for (int bit = BITS_PER_BYTE; bit > 0; --bit)
        {
            // 尝试除尽当前数据位。
            if (remainder & TOPBIT)
            {
                remainder = (remainder << 1) ^ POLYNOMIAL;
            }
            else
            {
                remainder = (remainder << 1);
            }
        }
    }

    // 最终余数为 CRC 结果。
    return (REFLECT_REMAINDER(remainder)) ^ FINAL_XOR_VALUE;
}
/* crc_slow() */
```

```c
/**
 * @brief 逐字节计算字节数组的 CRC。
 * @param[in] p_message 指向待计算 CRC 的字节数组的指针。
 * @param[in] n_bytes 数据数组中的字节数。
 * @return 数据数组的 CRC 结果。
 */
```

```c
crc_t
crc_fast(uint8_t const * p_message, int n_bytes)
{
    crc_t remainder = INITIAL_REMAINDER;

    // 使用多项式对消息进行除法，每次处理一个字节。
    for (int byte = 0; byte < n_bytes; ++byte)
    {
        uint8_t data = REFLECT_DATA(p_message[byte]) ^
                       (remainder >> (WIDTH - BITS_PER_BYTE));
        remainder = g_crc_table[data] ^ (remainder << BITS_PER_BYTE);
    }

    // 最终余数即 CRC。
    return {REFLECT_REMAINDER(remainder)} ^ FINAL_XOR_VALUE;
}
/* crc_fast() */
```

# 参考文献

- [Barr] Barr, Michael. “Programming Embedded Systems in C and C++.” O’Reilly, 1999.
- [C90] “ISO/IEC9899:1990, Programming Languages – C,” ISO, 1990.
- [C99] “ISO/IEC9899:1990, Programming Languages – C,” ISO, 1999.
- [CERT-C] Seabord, Robert C. “The C Coding Standard, Second Edition.” Pearson, 2014.
- [Harbison] Harbison III, Samuel P. and Guy L. Steele, Jr. “C: A Reference Manual, Fifth Edition.” Prentice Hall, 2002.
- [Hatton] Hatton, Les. “C: Developing Software for High-Integrity and Safety-Critical Systems.” McGraw-Hill, 1994.
- [Holub] Holub, Allen I. “Enough Rough to Shoot Yourself in the Foot: Rules for C and C++ Programming,” McGraw-Hill, 1995.
- [IEC6508] “Functional Safety of Electrical/Electronic/Programmable Electronic Safety-Related Systems,” International Electromechanical Commission, 1998-2000.
- [Koenig] Koenig, Andrew. “C Traps and Pitfalls.” Addison-Wesley, 1988.
- [Loudon] Loudon, Kyle. “C++ Pocket Reference.” O’Reilly, 2003.
- [MISRA-C] “MISRA C:2012 Guidelines for the use of the C language in critical systems,” MISRA, March 2013.
- [MISRA-C++] “MISRA C++ Guidelines for the use of the C++ language in critical systems,” MISRA, June 2008.
- [Prinz] Prinz, Peter and Ulla Kirch-Prinz. “C++ Pocket Reference.” O’Reilly, 2003.
- [Sutter] Sutter, Herb and Andrei Alexandrescu. “C++ Coding Standards: 101 Rules, Guidelines, and Best Practices.” Pearson, 2005.
- [Uwano] Uwano, H., Nakamura, M., Monden, A., and Matsumoto, K. “Analyzing Individual Performance of Source Code Review Using Reviewer’s Eye Movement,” Proceedings of the 2006 Symposium on Eye Tracking Research & Applications, San Diego, March 27-29, 2006.

# 索引

## 符号

- + 递减运算符 21
- 减法/单负运算符 21
- ! 逻辑取反运算符 21
- != 不等于运算符 21, 39
- # 预处理器标记符 21
- % 模运算符 21
- & 地址/按位与运算符 21
- && 逻辑与运算符 11, 21
- * 乘法/指针运算符 21
- + 加法/单加运算符 5, 21
- ++ 递增运算符 21
- . 成员运算符 21
- , 逗号运算符 21, 51
- $ 终止符 22
- / 除法运算符 21
- //, /* 注释符 17
- [ ] 下标运算符 21
- ^ 按位异异运算符 21, 35
- { } 大括号 1, 10, 54
- ( ) 圆括号 21, 44
- | 按位或运算符 21, 35
- || 逻辑或运算符 11, 21
- < 小于运算符 21
- << 左移运算符 21, 35
- <= 小于等于运算符 21
- =, +=, -=, *=, %, &=, ^=, <<= 赋值运算符 21
- = 等运算符 21
- -> 成员运算符 21
- > 大于运算符 21
- >= 大于等于运算符 21
- >> 右移运算符 21, 35
- ? 三元运算符 21
- - 按位取反运算符 21, 35

## A

- 缩写 12, 57-58
- abort() 函数 55
- 缩术语 12, 57-58
- 算法 18
- 对齐 23, 25, 27
- 匿名声明 33
- 架构 1, 2
- 数组下标 21
- 数组 48, 50, 54
- 汇编语言 8
- assert() 函数 17, 46
- 赋值表达式 52, 54
- 赋值运算符 21, 23
- 假设 18, 19
- 异步 45, 47, 49
- auto 自动存储类 14

## B

- 二进制数据 35
- 二进制运算符 21
- 位域 35, 37-38
- 位排序 37-38
- 按位运算符 35
- 空行 18, 23, 24
- 块代码 10, 23, 24
- bool 类型 39
- 布尔值 8, 39, 49
- 大括号 1, 10, 54
- break 语句 25, 53
- 总线 37
- 编译器优化 16
- 编译时检查 34, 38
- 复合语句 10
- 条件编译 17
- const 常限定符 15-16
- 常量 30, 31, 35, 36, 54, 56
- continue 语句 14
- 控制流 14
- 耦合 16, 30

## D

- 数据类型 30, 31, 33-39
- 调试输出 17
- 默认标签 25, 52-53
- 缺陷跟踪 2
- #define 指令 8, 15, 30, 44
- 延迟循环 15, 19
- 合约设计 18
- 设计评审 2
- 偏离 6
- 设备驱动程序 8, 31
- do-while 语句 10, 54
- 双精度 36
- double 类型 36
- Doxygen 工具 18, 20

## C

- C 运行时 50
- C 标准库 29, 40, 48, 59
- C++ 7, 8, 17, 29, 48
- C++ 风格注释 17, 18
- C90 3, 34, 39
- C99 3, 8, 34, 35, 36, 39, 44, 48, 50
- 引用传递 15
- 调用栈 46
- char 字符 28
- case 标签 25, 53
- 强制转换 13, 39
- char 类型 34, 51
- 代码美化 22, 26
- 代码比对 6, 9
- 代码评审 2, 5
- 逗号运算符 21, 51
- 被注释掉的代码 17
- 注释 3, 6, 8, 17-20, 24, 31, 32, 42, 45
- 通信协议 31
- 比较 35, 56

## E

- else 语句 10, 24, 42, 52
- 空语句 10
- 行尾注释 17, 18
- 文件结束 24
- #endif 指令 17, 30
- enum 关键字 33
- 枚举类型 33
- 等于运算符 (==) 3, 56
- 等效性测试 36, 56
- 异常情况 1, 14
- exit() 函数 55
- extern 存储类 30

## I

- #if 指令 17, 23
- if 语句 10, 21, 24, 52
- #ifdef 指令 23
- #ifndef 指令 17, 30
- 实现定义行为 3, 35, 38
- #include 指令 30, 31
- 头文件 31
- 缩进 6, 10, 18, 25, 27, 53

## F

- false 常量 39, 40, 38
- 文件路径 31
- 定点数数学 36
- 固定宽度整数类型 3, 34
- float32_t 类型 36
- float64_t 类型 36
- float128_t 类型 36
- 浮点 36
- 流程图 18
- for 语句 10, 21, 22, 54
- 换行符 28, 42
- 函数原型 31, 47
- 函数 3, 15, 16, 20, 30, 40, 42, 43, 45, 46
- 函数类宏 44

## INFINITY

- INFINITY 常量 36
- inline 关键字 40, 44, 48
- inline 函数 8, 44
- instruction 指针 55
- int 类型 34
- int_t 类型 34
- int16_t 类型 34, 35
- int32_t 类型 3, 34
- int64_t 类型 34
- 中断 15, 46, 47
- 中断服务例程 15, 46, 47
- isfinite() 宏 36
- ISO C 3, 8, 13, 35, 38

## G

- 缺陷 16
- 全局作用域 30
- 全局变量 15, 16, 30, 47, 48, 50
- GNU 缩进工具 22
- goto 语句 4, 14, 55

## J

- 跳转 14, 55

## K

- K&R C 48

## H

- 对象句 49
- 硬件故障 1
- 模板 3
- 头文件 29, 30, 31, 32, 42

## L

- 遗留代码 5, 6
- limits.h 36

## P

- 换行符 28
- 填充字节 37
- 行宽 25
- 参数 15, 20, 21, 42, 44
- 圆括号 11, 21, 44
- 局部变量 8, 50
- 外设 37
- long 类型 34
- 外设驱动程序 31
- long long 类型 34
- longjmp() 函数 55
- 指针 15, 21, 48, 50, 54
- 循环 24, 45, 54
- 计数器 15, 19, 48, 54
- 指针变量 48
- 指针指针变量 48
- 可移植性 1, 2, 3, 34, 38, 49

## M

- #pragma 指令 8
- 宏、预处理器 30, 31, 40, 44
- 优先级规则 11
- 魔术数字 54
- main() 函数 29, 45
- 预处理器保护 30
- malloc() 函数 52
- 内存映射 I/O 15
- 私有函数 31, 42
- MISRA 4, 5, 35
- 过程 30, 40-47
- 进程 45
- 模块 3, 6, 15, 18, 20, 29-32, 40, 55
- 原型 30, 31, 47
- 公共数据类型 33
- 公共函数 31, 40, 42

## N

- 命名规范 4, 21, 29, 33, 40, 48

## R

- NAN 常量 26
- 可读性 2, 24, 43, 50, 54
- NDEBUG 常量 17
- 寄存器 存储类限定符 4, 14
- 嵌套注释 17
- 寄存器 15-16, 33, 37, 47, 49
- 嵌套 if 块 52
- 关系运算符 39
- 网络 37
- 可靠性 1, 3, 34, 49
- 非打印字符 28
- 要求 1
- NULL 常量 50, 52, 56
- 返回语句 13, 21, 42, 43, 44
- RTOS 45

## O

- 操作系统 45, 47
- 运算符优先级 11
- 优化、编译器 16, 19

