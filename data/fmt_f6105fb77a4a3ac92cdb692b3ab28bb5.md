
// `int_type` 是能够表示位掩码类型所有值的整数类型

`enum bitmask = int_type;`

`V_0 = 1 << 0`, `V_1 = 1 << 1`, `V_2 = 1 << 2`, `V_3 = 1 << 3`, \dots;

```
inline constexpr bitmask C_0(V_0);
```

```
inline constexpr bitmask C_1(V_1);
```

```
inline constexpr bitmask C_2(V_2);
```

```
inline constexpr bitmask C_3(V_3);
```

```
constexpr bitmask operator&(bitmask X, bitmask Y) {
    return static_cast<bitmask>(n        static_cast<int_type>(X) & static_cast<int_type>(Y));
}
```

```
constexpr bitmask operator|(bitmask X, bitmask Y) {
    return static_cast<bitmask>(n        static_cast<int_type>(X) | static_cast<int_type>(Y));
}
```

```
constexpr bitmask operator^(bitmask X, bitmask Y) {
    return static_cast<bitmask>(n        static_cast<int_type>(X) ^ static_cast<int_type>(Y));
}
```

```
constexpr bitmask operator-(bitmask X) {
    return static_cast<bitmask>(-(static_cast<int_type>(X)));
}
```

```
bitmask& operator&=(bitmask X, bitmask Y) {
    X = X & Y; return X;
}
```

```
bitmask& operator|=(bitmask X, bitmask Y) {
    X = X | Y; return X;
}
```

```
bitmask& operator-=(bitmask X, bitmask Y) {
    X = X - Y; return X;
}
```

- 3 这里，`C_0`, `C_1` 等名称代表此特定位掩码类型的位掩码元素。所有此类元素都有不同的值，非零值且对于任意对 `C_i` 和 `C_j`（当 `i \neq j`），`C_i & C_j` 为非零且 `C_i & C_j`

§ 20.4.2.1

©ISO/IEC 2017 – 版权所有

452

# ISO/IEC 14882:2017(E)

为 0。此外，值 0 用于表示空位图图，其中没有位掩码元素被设置。

+   4 下述术语适用于位掩码类型的对象和值：
+   (4.1) 在对象 `X` 中设置值 `Y` 是求值表达式 `X |= Y`。
+   (4.2) 在对象 `X` 中清除值 `Y` 是求值表达式 `X &= Y`。
+   (4.3) 在对象 `X` 中设置值 `Y` 是求值表达式 `X & Y` 结果非零。

### 20.4.2.1 字符序列 [character.seq]

+   1 标准库可能假设广泛使用遵循少数几个惯的字符和字符序列：
+   (1.1) 字母是基础字符集中的 26 个小写字母或 26 个大写字母。
+   (1.2) 小数点字符是用于在（单字节）字符序列和一种浮点类型的值之间转换的函数所使用的（单字节）字符。它在字符序列中表示分数部分的开始。它在第 21 至 33 节和附录 D 中用点‘·’表示，其值在程序执行过程中可以通过调用 `locale(int, const char*)`，¹⁶² 或通过更改一个 `Locale` 对象（如第 25.3 和 30 节所述）而改变。
+   (1.3) 字符是一个可以声明为 `T[N]` 的对象 (11.3.4)，其中 `T` 是无符号或有符号字符 (6.9.1)，可选由 `const` 或 `volatile` 的任意组合修饰。数组的初始元素具有定义，直到包含一个由某些谓词确定的元素。字符序列可以由指向其第一个元素的指针 `S` 来定义。

### 20.4.2.1.5 字节字符串 [multibyte.strings]

+   1 多字节字符串，或称为 NTMS，是一种其最高对齐且具有定义内容的元素值为 0（终止空字符）的 NTMS；该序列中没有其他元素的取值为 0。¹⁶³
+   2 NTMS 的长度是终止空字符之前的元素个数。空赋值运算符的长度为 0。
+   3 NTMS 的值是包括终止空字符在内的元素值序列。
+   4 静态 NTMS 是具有静态存储生存期的 NTMS。

### 20.4.2.1.2 多字节字符串 [multibyte.strings]

+   1 多字节字符串，或称为 NTMS，是一种构成多字节字符序列的 NTMS，起始并结束于初始移位状态。¹¹⁶⁵
+   2 静态 NTMS 是具有静态存储生存期的 NTMS。

## 20.4.2.2 类内部的函数 [functions.within.classes]

+   1 为了说明之便，第 21 至 33 节和附录 D 不拷贝/构造成员、赋值运算符或（非虚）析构函数，其父类语义与可以默认生成的（15.1）相同。

¹⁶² 在 `<locale>` (25.5) 中声明。
¹⁶³ `<string>` (24.5) 中声明的函数操作的许多对象是字符序列或 NTMS。这些字符序列的大小由长度值限制，该值独立于字符序列维护。
¹⁶⁴ 像 "abc" 这样的字面量是一个 NTMS。
¹⁶⁵ 只包含基础执行字符集中字符的 NTMS 也是 NTMS。每个多字节字符由单个字节组成。

§ 20.4.2.2 ©ISO/IEC 2017 – 所有权利保留 453

# ISO/IEC 14882:2017(E)

被默认生成（15.1, 15.4, 15.8）。未规定此类函数的签名或虚析构函数是否可以默认生成。

为了说明之便，库将构造函数标记为 `EXPLIC`。这样的构造函数被条件声明为显式的或非显式的 (15.3.1)。注意：这通常由两个构造函数实现，其中至少参与重载。—— 备注；

+   该子类规定了适用于整个 C++ 标准库的要求。第 21 至 33 节和附录 D 规定了类的表示，并故意省略了类成员的规定 (12.2)。

为了说明之便，某些子节提供了私有成员的声明和语义要求，以满足第 21 至 33 节中指定的成员函数。如下：

```
// 仅用于说明
```
