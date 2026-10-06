

# ISO/IEC 14882:2017(E)

```cpp
// 30.8.2.2, assign and swap
basic_stringbuf& operator=(const basic_stringbuf& rhs) = delete;
basic_stringbuf& operator=(basic_stringbuf&& rhs);
void swap(basic_stringbuf& rhs);
```

```cpp
// 30.8.2.3, get and set
basic_charT<T, traits, Allocator> str() const;
void str(const basic_charT<T, traits, Allocator>& s);
```

```cpp
protected:
// 30.8.2.4, overridden virtual functions
int _underflow() override;
int _pbckill(int type, const traits c=traits::eof()) override;
int _overflow(int type, const traits c=traits::eof()) override;
basic_stringbuf(const basic_charT* s, std::streamsize n) : override;

pos_type seekoff(seekoff type, ios_base::seekdir dir);
ios_base::openmode mode = ios_base::in | ios_base::out) override;
pos_type seekpos(pos_type sp, ios_base::seekdir dir);
ios_base::openmode mode = ios_base::in | ios_base::out) override;
```

```cpp
private:
ios_base::openmode mode; // exposition only
);

template <class charT, class traits, class Allocator>
void swap(basic_stringbuf<charT, traits, Allocator>& x,
          basic_stringbuf<charT, traits, Allocator>& y) {

}
```

- 1 类 class_string 派生自 basic_stringbuf，用于将可能的输入序列和可能的输出序列与一组任意字符序列关联起来。该序列可以从 class_string 类对象初始化，也可以作为 class_string 类对象提供。
- 2 为了阐述起见，此处此处维护的数据呈现形式如下：
  (2.1) ios_base::openmode，如果设置了 in，则表示输入序列可以读取，如果设置了 out，则表示输出序列可以写入。

## 30.8.2.1 basic_stringbuf constructors [stringbuf.cons]

```cpp
explicit basic_stringbuf(ios_base::openmode mode = ios_base::in | ios_base::out);
```

- 1 效果：构造一个 basic_stringbuf 类的对象，通过 basic_stringbuf()(30.6.3.1) 初始化该类，并使用 mode 初始化。
- 2 后置条件：str() == "";

```cpp
explicit basic_stringbuf(const basic_charT<T, traits, Allocator>& s,
ios_base::openmode mode = ios_base::in | ios_base::out);
```

- 3 效果：构造一个 basic_stringbuf 类的对象，通过 basic_stringbuf()(30.6.3.1) 初始化该类，并使用 mode 初始化。然后调用 str(s)。

```cpp
basic_stringbuf(basic_stringbuf&& rhs);
```

- 4 效果：从右值 rhs 移动内容。*this(eback(), gptr(), egptr(), rhs_pbase(), pptr(), eptr())* 中的序列指针是否获得 rhs 所拥有的值取决于实现。无论是否获得，构造后 *this 和 rhs 引用的缓冲区（如果有的话）*。rhs 的 opencode、本地状态以及任何其他状态都会被拷贝。

**后置条件：** 令 rhs_p 指向 rhs 在此构造之前的状态，rhs_a 指向 rhs 在此构造之后的状态。

- 5
  (5.1) str() == *this == rhs_p.str()
  (5.2) gptr() - eback() == rhs_p.gptr() - rhs_p.eback()
  (5.3) egptr() - eback() == rhs_p.egptr() - rhs_p.eback()
  (5.4) pptr() - pbase() == rhs_p.pptr() - rhs_p.pbase()
  (5.5) eptr() - pbase() == rhs_p.eptr() - rhs_p.pbase()
  (5.6) if (eback()) eback() != rhs_a.eback()
  (5.7) if (gptr()) gptr() != rhs_a.gptr()
  (5.8) if (egptr()) egptr() != rhs_a.egptr()
  (5.9) if (pbase()) pbase() != rhs_a.pbase()
  (5.10) if (eptr()) eptr() != rhs_a.eptr()
  (5.11) if (eptr()) eptr() != rhs_a.eptr()

## 30.2.2 Assign and swap

```cpp
basic_stringbuf& operator=(basic_stringbuf& rhs)
```

效果：移动赋值后，*this 拥有了从 rhs 移动时本应拥有的状态（见 30.8.2.1）。

返回：*this。

```cpp
void swap(basic_stringbuf& rhs);
```

效果：交换 *this 和 rhs 的状态。

```cpp
template <class charT, Traits, Allocator>
void swap(basic_stringbuf<charT, Traits, Allocator>& x,
     basic_stringbuf<charT, Traits, Allocator>& y);
```

效果：相当于 x.swap(y)。

## 30.2.3 Member functions

```cpp
basic_stringbuf<charT, Traits, Allocator> const();
```

返回：一个内容等于底层序列的 basic 对象。如果 basic_stringbuf 是仅以输入模式创建的，结果 basic_stringbuf 包含 [eback(), egptr()) 范围内的字符。如果创建 basic_stringbuf 时 ios_base::out 非零，则结果 basic_stringbuf 包含 [pbase(), eptr()) 范围内的字符，其中标记表示通过写入流、构造 stringbuf 或调用 str() 成员函数初始化的最后一个字符的位置。在所有未初始化的情况下，返回一个长度为零的 stringbuf。

```cpp
void str(const basic_string<char, Allocator>& s);
```

效果：将 s 拷贝到 stringbuf 底层序列并根据 mode 初始化输入和输出序列。

后置条件：如果 mode & ios_base::out 非零，pptr() 指向底层字符且 eptr() == pptr() + s.size()；如果 mode & ios_base::in 非零，pptr() == pptr() + s.size()。如果 mode & ios_base::in 非零，eback() 指向底层字符，且 gptr() == eback() 和 egptr() == eback() + s.size()。

## 30.8.2.4 Overridden functions

```cpp
int_type overflow();
```

返回：如果输入序列有位置，返回 traits::int_type(gptr())。否则返回 eof()。输入序列中已初始化的字符。

```cpp
int_type putback(int_type c) override;
```

效果：将指定的字符 c放入输出序列，如果可能，在以下三种情况之一发生：

- 如果 traits::eof(c) 返回 false 且输入序列有 putback 可，且 to_char_type(gptr()[-1]) 返回 true，将 gptr() - 1 赋值给 gptr()。返回：c。
- 如果 traits::eof(c) 返回 false 且输入序列有 putback 可，且 mode & ios_base::out 非零，pptr()。返回：c。
- 如果 traits::eof(c) 返回 true 且输入序列有 putback 可，将 gptr() - 1 赋值给 gptr()。返回：not_eof(c)。

返回：如上述，或返回 traits::eof() 表示失败。

备注：如果函数能在这些情况中的多种情况下成功，则未指定哪一种。

```cpp
int_type overflow(int_type c) override;
```

效果：将指定的字符 c 追加到输出序列，如果可能，在以下两种情况之一发生：

- 如果 traits::eof(c) 返回 false 且输出序列有写入位置，或函数可以提供写入位置（见下文），调用 sput(c)。通过返回产生信号。
- 如果 traits::eof(c) 返回 true，没有字符可追加。通过返回产生信号。

备注：函数的任何调用都可能改变可用写入位置的数量。返回：如上述，或返回 traits::eof() 表示失败。

函数仅在 (mode & ios_base::out) != 0 时才能提供写入位置。为了提供写入位置，函数会重新分配（或初始分配）一个具有足够容纳当前数组（如果有）加上至少一个额外写入位置的对象。

如果 (mode & ios_base::in) != 0，函数将读取指针 egptr() 到新写入位置之后。

```cpp
pos_type seekoff(off_type off, ios_base::seekdir dir,
    ios_base::openmode mode = ios_base::in | ios_base::out) override;
```

效果：如果可能，在控制的序列之一更改流位置，如表 115 所示。

| Conditions | 结果 |
|---|---|
| (which & ios_base::in) == ios_base::in | 输入序列 |
| (which & ios_base::out) == ios_base::out | 输出序列 |
| (which & ios_base::in | ios_base::out) == (ios_base::in | ios_base::out) and way == ios_base::beg \| ios_base::end | 输入和输出序列 |
| 其他 | 定位操作失败 |

对于序列的定位，如果其后续指针（egptr() 或 pptr()）为空指针，则定位操作失败。否则，函数按照表 116 所示确定 newoff。

| Condition | newoff 值 |
|---|---|
| way == ios_base::beg | 0 | 后续指针减去起始指针 (xnext xbeg)。 |
| way == ios_base::cur | |
| way == ios_base::end | 高标记指针减去起始指针 (high_mark - xbeg)。 |

如果 (newoff + off) < 0，或者如果 newoff + off 指向未定义的字符 (30.8.2.3)，则定位操作失败。否则，函数 xbeg + newoff + off 指向指针 next。

返回：pos_type(newoff)，由结果偏移量 newoff (off_type) 构造，存储流位置。如果定位操作失败，或构造的对象无法返回流位置，则返回值为 pos_type(off_type(-1))。

```cpp
pos_type seekpos(pos_type sp,
    ios_base::openmode mode = ios_base::in | ios_base::out) override;
```

效果：等同于 seekoff(off_type(sp), ios_base::beg, which)。

