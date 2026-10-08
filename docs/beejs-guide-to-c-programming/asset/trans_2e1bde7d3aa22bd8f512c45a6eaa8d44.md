

```c
printf("struct t :%zu\n", alignof(struct t));
printf("max_align_t:%zu\n", alignof(max_align_t));
}
```

在我系统上的输出如下：

- char : 1
- short : 2
- int : 4
- long : 8
- long long : 8
- double : 8
- long double : 16
- struct t : 16
- max_align_t : 16

就是这些。对齐！

# 索引

- 布尔非 (NOT), 16
- != 不等运算符, 15
- 单引号, 87
- VLA 函数原型, 216
- 间接运算符, 31–32
- 乘法运算符, 12
- 赋值运算符, 13
- 加法运算符, 13
- ++ 增增运算符, 14–15
- 赋值运算符, 15
- , 逗号运算符, 15
- 减法运算符, 13
- 递减运算符, 14–15
- 赋值运算符, 13
- -> 箭头运算符, 52
- 变长参数, 179–180
- / 除法运算符, 13
- /= 赋值, 13
- < 小于运算符, 15
- << 左移, 178
- <= 赋值, 178
- <= 小于等于运算符, 15
- = 赋值运算符, 12
- == 等于运算符, 15
- > 大于运算符, 15
- >= 大于等于运算符, 15
- >> 右移, 178
- >== 赋值, 178
- ? 三元运算符, 13–14

# null 指令, 141
## 拼接, 136
## 字符串化, 135
## define 指令, 6, 127–133
## vs const, 127

# #if elif 指令, 129
## else 指令, 129
## endif 指令, 128–129
## error 指令, 139

# #if @ 指令, 130
# #if defined 指令, 130
## if 指令, 129–130
## ifdef 指令, 128–129
## ifndef 指令, 128–129

# #include 指令, 6, 126
- 本地文件, 126
- #line 指令, 140
- #pragma 指令, 139–140
- #非标准 pragma, 139
- #undef 指令, 131
- #warning 指令, 129
- % 取模运算符, 13
- %= 赋值运算符, 13
- & 取地址运算符, 29–30
- && 按位与, 177
- &= 赋值运算符, 177
- && 布尔与, 16
- ^ 按位异或, 177
- ^= 赋值, 177
- _Alignas 限定符, 302
- _Alignof 运算符, 302–303
- _Atomic 类型限定符, 289–290
- _Atomic 类型指定, 290
- _Complex 类型, 248
- _Complex_I 宏, 249
- _Exit() 函数, 205
- _Generic 关键字, 232–235
- _Imaginary 类型, 249
- _Imaginary_I 宏, 249
- _return 函数指定, 301
- _Pragma 运算符, 140
- _Thread_local 存储类, 112, 271
- _DATE 宏, 131–132
- _FILE 宏, 131–132
- _LINE 宏, 131–140
- _STDC_ANALYZE 宏, 132
- _STDC_HOSTED 宏, 131
- _STDC_IEC 宏, 132, 248–249
- _STDC_IEC_55 宏, 132
- _STDC_ISO_864 宏, 132
- _STDC_LIB_EXT 宏, 133
- _STDC_MB_MIGHT_NEQ 宏, 132
- _STDC_NO_ATOMICS 宏, 232
- _STDC_NO_COMPLEX 宏, 248
- _STDC_NO_THREADS 宏, 233, 263
- _STDC_NO_VLA 宏, 233
- _STDC_UTF_16 宏, 132
- _STDC_UTF_32 宏, 201
- _STDC_UTF_32 宏, 132 (注：在源文件中重复)

# 索引
- _STDC_VERSION 宏, 131–132
- __TIME 标识符, 131–132
- _atomic_time() Windows, 260
- _putenv() 函数, 124
- 按位或, 177
- 赋值, OR, 206
- 布尔或, 177
- 反斜杠转义, 158–161
- ' 单引号, 158–159
- \123 进制值, 161
- ? 问号, 159–160
- Unicode 转义, 161, 191
- 警报, 159
- 退格, 159–160
- v 换页符, 159
- 换行, 175
- 回车, 160
- \t 制表符, 161
- Unicode 转义, 161, 191
- 垂直制表符, 159
- \x12 十六进制值, 161
- 反斜杠, 159
- 按位非, 177
- 八进制, 93
- 二进制, 93
- 十六进制, 93
- abort() 函数, 206
- 加法运算符, + 加法
- alignas 指定符, 302
- aligned_alloc(), 80–81
- 对齐, 301–303
- alignof(), 302–303
- arg 参数, 118–120
- argv 参数, 03, 13
- 初始化器, 36–38
- 数组, 35–43
- 作为指针, 40
- 获取长度, 36
- 索引, 35–36
- 修改函数, 41–42
- 多维, 39
- 多维初始化, 237–239
- 越界, 38
- 传递给函数, 40–43
- static_cast 在参数列表中, 236–237
- 类型限定符, 236
- 零长度, 146
- cctime() 函数, 259
- atex() 函数, 204
- 原子变量, 282–297
- acquire, 286–287, 295
- acquire/release, 295
- 赋值和运算符, 288
- 标志, 292
- 编译的, 282
- 消费, 285
- 栅栏, 290–291
- 无锁, 294–295
- 内存顺序, 294–295
- 指针, 293–294
- 释放, 295
- release, 286–287, 295
- 顺序一致性, 277–288, 294
- 结构体和联合, 292–293
- 同步, 284
- 同步库函数, 288–292
- atomic_bool, 299
- atomic_BOOL_LOCK_macro, 291
- atomic_char, 290
- atomic_char_t, 299
- atomic_CHAR_T_LOCK_macro, 291
- atomic_char32_t, 290
- atomic_CHAR32_T_LOCK_macro, 291
- atomic_CHAR_LOCK_macro, 291
- atomic_fetch_explicit(), 294
- atomic_flag_t, 292
- atomic_flag_clear(), 292
- atomic_FLAG_INIT, 292
- atomic_flag_test_and_set(), 292
- atomic_int, 283
- atomic_intmax_type, 290
- atomic_INT_LOCK_macro, 291
- atomic_ptr, 250
- atomic_is_free(), 291
- atomic_long, 289
- atomic_long_type, 289
- atomic_LONG_LOCK_macro, 291
- atomic_long_t, 289
- atomic_ullong_type, 289
- atomic_ulong_type, 289
- atomic_ushort_type, 289
- atomic_wchar_type, 289
- ATOMIC_WCHAR_LOCK_macro, 291
- auto 存储类, 108–109
- 原子变量, 74
- char32_t_type, 201
- 字符集, 190–191
- 基础, 190–191
- 执行, 190, 191
- 源, 190, 191
- cimag() 函数, 250, 252
- cimagf() 函数, 250
- cimagl() 函数, 250
- clang 编译器, 8
- clog() 函数, 252
- CMPLX 宏, 248–250, 252
- CMPLX() 宏, 290
- clbreak, 281
- Bell, 见运算符
- 按位操作, 177–178
- bool_type, 13
- 布尔与, 见 && 运算符
- 布尔非, 见 !运算符
- 布尔运算符, 16
- 布尔或, 见 || 运算符
- 布尔类型, 12–13
- break 语句, 21–23
- cnd_destroy() 函数, 277–280
- cnd_init() 函数, 277–280
- cnd_signal() 函数, 277–280
- cnd_t_type, 277–280
- cnd_timedwait() 函数, 280
- cnd_wait() 函数, 277–280
- 命令参数, 117–120
- 比较运算符, 15
- 复数, 6
- complex double_type, 249
- complex float_type, 249
- complex long_type, 249
- 复数数字, 248–252
- C 预处理器, 6
- c16str_t() 函数, 202
- c32str_t() 函数, 202
- C30PO, 24
- abs() 函数, 52
- cacos() 函数, 252
- casinh() 函数, 252
- catan() 函数, 252
- carg() 函数, 252
- calloc() 函数, 76–77
- cos() 函数, 57–252
- ccosh() 函数, 252
- cexp() 函数, 252
- case 语句, 21–22
- Carriage return, 见运算符
- Conditional compilation, 127–130
- Conditional Operators, 15
- correctness, 106–107
- Command arguments, 117–120
- Date and time, 257–262
- Dereferencing, 31–32
- Division operator, 见 /运算符
- difference, 262
- Data serialization, 60
- DBL_DECIMAL_DIG, 92
- DBL_DIG, 90
- DECIMAL_DIG, 92
- default label, 22
- EOF end of file, 55
- Escape sequences, 158–161
- Exit status, 121–123
- Exiting, 203–206
- EXIT_FAILURE macro, 121–122
- EXIT_SUCCESS macro, 121–122
- Environment variables, 123–125
- environ variable, 124
- enum keyword, 23
- enumerated types, 162–165
- File I/O, 53–60
- binary files, 57–59
- formatted input, 56–57
- Fixed width integers, 253–256
- Flow Control, 17–23
- float constant, 95
- Floating point constants, 95
- float type, 11
- for statement, 20–21
- FP_COMPRACT pragma, 139–140
- fopen() 函数, 54–55
- free() 函数, 75
- fwide() 函数, 196
- fprintf() 函数, 57–196
- fwrite() 函数, 57–58
- fscanf() 函数, 196
- FENV_ACCESS macro, 140
- getc() 函数, 54–55
- gets() 函数, 56
- getf() 函数, 196
- getw() 函数, 196
- getenv() 函数, 121, 196
- goto() 函数, 259
- Generic selectors, 223–235
- gcc compiler, 7–9, 116
- numbering order, 162–163
- multiline comments, 136–137
- while statement, 19–20
- with threads, 263
- with numeric values, 59–60
- with structs, 59–60
- line by line, 55–56
- text files, reading, 54
- text files, writing, 57
- FILE* type, 53–54
- main(), 203
- extern storage class, 110
- Fall through, 22–23
- false value, 13
- timeouts, 280
- spurious_wakeup, 278
- bailing out, 222
- break, 21–23
- continue, 221–222
- as, shell, 222, 221–228
- as labeled, 223
- statement, 220–228

# INDEX
- atomic_size_t_type, 290
- atomic_thread_fence(), 296
- atomic_uchar_type, 289
- atomic_uint_type, 289
- atomic_uint_fast8_t, 290
- atomic_uint_fast32_t, 290
- atomic_uint_fast64_t, 290
- atomic_uint_least16_t, 290
- atomic_uint_least32_t, 290
- atomic_uint_least64_t, 290
- atomic_uint_least8_t, 290
- atomic_intmax_type, 290
- atomic_uintptr_type, 289
- atomic_ullong_type, 289
- atomic_ulong_type, 289
- atomic_ushort_type, 289
- atomic_wchar_type, 289

