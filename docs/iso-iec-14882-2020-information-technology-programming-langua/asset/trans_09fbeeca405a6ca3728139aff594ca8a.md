

```cpp
streamsize alsize;                 // exposition only
void* (*palloc)(size_t);            // exposition only
void (*pfree)(void*);               // exposition only
};
}
```

`strstreambuf` 类将输入序列（可能还有输出序列）与某个 `character` 数组类型的对象相关联，该数组对象的元素存储任意值。该数组对象具有若干属性。

> *[注 1：* 为了便于说明，这些属性表示为位掩码类型（此处记为 T1）`strstate` 的元素。这些元素包括：
>
> - (2.1) — **已分配**，当动态数组对象已被分配时设置，因此该对象将由 `strstreambuf` 对象的析构函数释放；
> - (2.2) — **常量**，当数组对象具有 const 元素时设置，因此不能写入输出序列；
> - (2.3) — **动态**，当数组对象按需分配（或重新分配）以容纳长度可变的字符序列时设置；
> - (2.4) — **冻结**，当程序已请求不更改、不重新分配或不释放数组对象时设置。
>
> — *注结束*]

> *[注 2：* 为了便于说明，维护的数据在此表示如下：
>
> - (3.1) — `strstate strmode`，与 `strstreambuf` 对象关联的数组对象的属性；
> - (3.2) — `int alsize`，动态数组对象的建议最小大小；
> - (3.3) — `void* (*palloc)(size_t)`，指向要调用的用于分配动态数组对象的函数；
> - (3.4) — `void (*pfree)(void*)`，指向要调用的用于释放动态数组对象的函数。
>
> — *注结束*]

`strstreambuf` 类的每个对象都有一个*可定位区域*，由指针 `seeklow` 和 `seekhigh` 界定。如果 `gnext` 是空指针，则可定位区域未定义。否则，`seeklow` 等于 `gbeg`，且 `seekhigh` 要么是 `pend`（如果 `pend` 不是空指针），要么是 `gend`。

### D.13.2.2 `strstreambuf` 构造函数

```cpp
explicit strstreambuf(streamsize alsize_arg);
```

**效果：** 使用 `streambuf()` 初始化基类。此函数的后置条件见表 148。

表 148：`strstreambuf(streamsize)` 的效果

| 元素 | 值 |
| --- | --- |
| `strmode` | `dynamic` |
| `alsize` | `alsize_arg` |
| `palloc` | 空指针 |
| `pfree` | 空指针 |

```cpp
strstreambuf(void* (*palloc_arg)(size_t), void (*pfree_arg)(void*));
```

**效果：** 使用 `streambuf()` 初始化基类。此函数的后置条件见表 149。

表 149：`strstreambuf(void* (*)(size_t), void (*)(void*))` 的效果

| 元素 | 值 |
| --- | --- |
| `strmode` | `dynamic` |
| `alsize` | 未指定的值 |
| `palloc` | `palloc_arg` |
| `pfree` | `pfree_arg` |

```cpp
int pcount() const;
```

**效果：** 如果输出序列的下一指针 `pnext` 是空指针，则返回零。否则，返回数组对象当前有效长度，即下一指针减去输出序列的起始指针，`pnext - pbeg`。

### D.13.2.4 `strstreambuf` 重写的虚函数

```cpp
int_type overflow(int_type c = EOF) override;
```

**1 效果：** 尽可能以以下两种方式之一将 `c` 指定的字符追加到输出序列：

- 1. 如果 `c != EOF`，并且输出序列具有可用的写入位置或函数创建了一个可用的写入位置（如下所述），则将 `c` 赋给 `*pnext++`。返回 `(unsigned char)c`。
- 2. 如果 `c == EOF`，则没有要追加的字符。返回一个不同于 `EOF` 的值。

**2** 返回 `EOF` 表示失败。

**3 备注：** 该函数可以在任何调用后改变可用写入位置的数量。

**4** 为使写入位置可用，函数重新分配（或首次分配）一个数组对象，其元素数量 `n` 足够容纳当前数组对象（如果有），加上至少一个额外的写入位置。除此之外，具体提供多少个额外写入位置未作规定。如果 `palloc` 不是空指针，函数调用 `(*palloc)(n)` 来分配新的动态数组对象；否则，它求值表达式 `new charT[n]`。无论哪种情况，如果分配失败，函数返回 `EOF`；否则，它在 `strmode` 中设置 `allocated`。

**5** 要释放一个先前存在的、首元素地址为 `p` 的动态数组对象：如果 `pfree` 不是空指针，函数调用 `(*pfree)(p)`；否则，它求值表达式 `delete[] p`。

**6** 如果 `(strmode & dynamic) == 0`，或者 `(strmode & frozen) != 0`，则函数无法扩展数组（以更大的长度重新分配）来提供可用的写入位置。

**7 推荐做法：** 实现在决定额外提供多少个写入位置时应考虑 `alsize`。

```cpp
int_type pbackfail(int_type c = EOF) override;
```

**8** 尽可能以以下三种方式之一将 `c` 指定的字符放回输入序列：

- 1. 如果 `c != EOF`，输入序列有可用的放回位置，且 `(char)c == gnext[-1]`，则将 `gnext - 1` 赋给 `gnext`。返回 `c`。
- 2. 如果 `c != EOF`，输入序列有可用的放回位置，且 `strmode & constant` 为零，则将 `c` 赋给 `*--gnext`。返回 `c`。
- 3. 如果 `c == EOF` 且输入序列有可用的放回位置，则将 `gnext - 1` 赋给 `gnext`。返回一个不同于 `EOF` 的值。

**9** 返回 `EOF` 表示失败。

**10 备注：** 如果函数可以通过多种方式成功，具体选择哪种方式未作规定。该函数可以在任何调用后改变可用放回位置的数量。

```cpp
int_type underflow() override;
```

**11 效果：** 尽可能从*输入序列*中读取一个字符，而不使流位置越过该字符，如下所示：

- 1. 如果输入序列具有可用的读取位置，函数通过返回 `(unsigned char)*gnext` 表示成功。
- 2. 否则，如果当前写入下一指针 `pnext` 不是空指针且大于当前读取结束指针 `gend`，则通过将 `gend` 赋为一个大于 `gnext` 且不大于 `pnext` 的值来提供可用的读取位置。返回 `(unsigned char)*gnext`。
- 3. 返回 `EOF` 表示失败。

**备注：** 该函数可以在任何调用后改变可用读取位置的数量。

```cpp
pos_type seekoff(off_type off, seekdir way, openmode which = in | out) override;
```

**效果：** 尽可能按表 151 所示改变受控序列之一的流位置。

表 151：seekoff 定位

| 条件 | 结果 |
| --- | --- |
| `(which & ios::in) != 0` | 定位输入序列 |
| `(which & ios::out) != 0` | 定位输出序列 |
| `(which & (ios::in \| ios::out)) == (ios::in \| ios::out)` 且 `way == ios::beg` 或 `way == ios::end` | 同时定位输入序列和输出序列 |
| 否则 | 定位操作失败 |

对于要进行定位的序列，如果其下一指针是空指针，则定位操作失败。否则，函数按表 152 确定 `newoff`。

表 152：`newoff` 值

| 条件 | `newoff` 值 |
| --- | --- |
| `way == ios::beg` | `0` |
| `way == ios::cur` | 下一指针减去起始指针（`xnext - xbeg`） |
| `way == ios::end` | `seekhigh` 减去起始指针（`seekhigh - xbeg`） |

如果 `(newoff + off) < (seeklow - xbeg)` 或 `(seekhigh - xbeg) < (newoff + off)`，则定位操作失败。否则，函数将 `xbeg + newoff + off` 赋给下一指针 `xnext`。

**返回值：** 由结果偏移量 `newoff`（类型为 `off_type`）构造的 `pos_type(newoff)`，如果可能，存储结果流位置。如果定位操作失败，或构造的对象无法表示结果流位置，则返回值为 `pos_type(off_type(-1))`。

```cpp
pos_type seekpos(pos_type sp, ios_base::openmode which = ios_base::in | ios_base::out) override;
```

**效果：** 尽可能改变受控序列之一的流位置，使其与存储在 `sp` 中的流位置对应（如下所述）。

- 如果 `(which & ios::in) != 0`，定位输入序列。
- 如果 `(which & ios::out) != 0`，定位输出序列。
- 如果函数未定位任何一个序列，则定位操作失败。

对于要进行定位的序列，如果其下一指针是空指针，则定位操作失败。否则，函数从 `sp.offset()` 确定 `newoff`：

- 如果 `newoff` 是无效流位置、具有负值，或值大于 `(seekhigh - seeklow)`，则定位操作失败。
- 否则，函数将 `newoff` 与起始指针 `xbeg` 相加，并将结果存储在下一指针 `xnext` 中。

**返回值：** 由结果偏移量 `newoff`（类型为 `off_type`）构造的 `pos_type(newoff)`，如果可能，存储结果流位置。如果定位操作失败，或构造的对象无法表示结果流位置，则返回值为 `pos_type(off_type(-1))`。

