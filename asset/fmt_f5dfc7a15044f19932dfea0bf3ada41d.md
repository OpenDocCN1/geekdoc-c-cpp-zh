
```cpp
if (is_set) {
    printf("key=%d\n", *(int*)point_after_struct);
} else {
    struct map_pair *p=(struct map_pair*)point_after_struct;
    printf("key=%d value=[%s]\n", p->key, p->value);
};

if (traverse==false) {
    return;
}

if (n->M_left) {
    dump_tree_node(n->M_left, is_set, traverse, dump_keys_and_values);
}
if (n->M_right) {
    dump_tree_node(n->M_right, is_set, traverse, dump_keys_and_values);
};

const char * ALOT_OF_TABS="";
void dump_as_set(struct tree_node *n, bool is_set) {
    void *point_after_struct=(char*)n+sizeof(struct tree_node);
    if (is_set) {
        printf("%d\n", *(int*)point_after_struct);
    } else {
        struct map_pair *p=(struct map_pair*)point_after_struct;
        printf("%d [%s]\n", p->key, p->value);
    }

    if (n->M_left) {
        printf("%*s-----", tabs, ALOT_OF_TABS);
        dump_as(tabs+1, n->M_left, is_set);
    }
    if (n->M_right) {
        printf("%*s-----", tabs, ALOT_OF_TABS);
        dump_as(tabs+1, n->M_right, is_set);
    }
}
void dump_map_and_set(struct tree_struct *m, bool is_set) {
    printf("ptr=%0%x, M_key_compare=%0%x, M_header=%0%x, M_node_count=%d\n",
        m->M_key_compare, &m->M_header, m->node_count);
    dump_tree_node(m->M_header, is_set, true, true);
    printf("As a tree:\n");
    printf("root---\n");
}

int main() {
  // map
  std::map<int, const char*> m;
  m[10]="ten";
  m[20]="twenty";
  m[3]="three";
  m[101]="one hundred";
  m[12]="twelve";
  m[107]="one hundred seven";
  m[0]="zero";
  m[6]="six";
  m[99]="nine";
  m[51]="five";
  m[1]="eleven";
  m[1001]="one thousand";
  m[1010]="one thousand";

  printf("dumping m as map:\n");
  dump_map_and_set(&m, false);

  std::map<int, const char*>::iterator it=m.begin();
  printf("%s\n", it->second);
  dump_tree_node((struct tree_node*)it, false, true, false);
  it=m.end();
  printf("%s\n", it->second);
  dump_tree_node((struct tree_node*)it, false, true, false);

  // set
  std::set<int> s;
  s.insert(123);
  s.insert(456);
  s.insert(11);
  s.insert(100);
  s.insert(101);
  printf("dumping s as set:\n");
  dump_map_and_set((struct tree_struct*)&s, true);

  std::set<int>::iterator it2=s.begin();
  printf("%s\n", it2->second);
  dump_tree_node((struct tree_node*)it2, false, true, false);
  it2=s.end();
  printf("%s\n", it2->second);
  dump_tree_node((struct tree_node*)it2, false, true, false);
}
```

# 列表 3.11: GCC 4.8.1

```
dumping m as map:
ptr=0x0028FE3C, M_key=0x0420, M_parent=0x0028FE40, M_node_count=7
ptr=0x007A4988, M_left=0x007A4C00, M_parent=0x0028FE40, M_right=0x007A4B80, M_color=1, key=10
ptr=0x007AC60, M_left=0x007A4BE0, M_parent=0x007A4988, M_right=0x007A4C60, M_color=1, key=1
ptr=0x007A4BE0, M_left=0x00000000, M_parent=0x007A4C00, M_right=0x00000000, M_color=1, key=0
ptr=0x007A4C60, M_left=0x007A4B40, M_parent=0x007A4C00, M_right=0x007A4C20, M_color=0, key=5
ptr=0x007A4B40, M_left=0x007ACE0, M_parent=0x007A4C60, M_right=0x00000000, M_color=1, key=3
ptr=0x007A4C60, M_left=0x00000000, M_parent=0x00000000, M_right=0x00000000, M_color=0, key=2
ptr=0x007A4C00, M_left=0x00000000, M_parent=0x007A4C0, M_right=0x007A4D00, M_color=1, key=6
ptr=0x007A4D00, M_left=0x00000000, M_parent=0x007A4C20, M_right=0x00000000, M_color=0, key=9
ptr=0x007A4B80, M_left=0x007A49A8, M_parent=0x007A4988, M_right=0x007A4BC0, M_color=0, key=100
ptr=0x007A49A8, M_left=0x007ABA00, M_parent=0x007A49B8, M_right=0x007A4C40, M_color=0, key=20
ptr=0x007ABA00, M_left=0x007A4C80, M_parent=0x007A49A8, M_right=0x00000000, M_color=1, key=12
ptr=0x007A4C00, M_left=0x00000000, M_parent=0x007ABA00, M_right=0x00000000, M_color=0, key=11
ptr=0x007A4C40, M_left=0x00000000, M_parent=0x007A49A8, M_right=0x00000000, M_color=0, key=99
ptr=0x007A4BC0, M_left=0x007A4B80, M_parent=0x007A4B80, M_right=0x007A4CA0, M_color=0, key=107
ptr=0x007A4B60, M_left=0x00000000, M_parent=0x007A4BC0, M_right=0x00000000, M_color=1, key=101

As a tree:
root---
10 [ten]
      1 [one]
        0 [zero]
          5 [five]
            3 [three]
              6 [six]
              9 [nine]
      100 [one hundred]
        20 [twelve]
          11 [eleven]
            90 [ninety-nine]
        107 [one hundred seven]
          101 [one hundred]
            1001 [one thousand]
              1010 [one thousand]
m.begin():
ptr=0x007A4BE0, M_left=0x00000000, M_parent=0x007A4CB0, M_right=0x00000000, M_color=1, key=zero
m.end():
ptr=0x0028FE40, M_left=0x007A4BE0, M_parent=0x007A4988, M_right=0x007A4CC0, M_color=0

dumping s as set:
ptr=0x0028FE20, M key compare=0x8, M header=0x0028FE24, M node_count=6
ptr=0x007A1E80, M_left=0x01D5D890, M_parent=0x0028FE24, M_right=0x01D5D850, M_color=1, key=1011
ptr=0x01D5D890, M_left=0x01D5D870, M_parent=0x007A1E80, M_right=0x01D5D880, M_color=1, key=1012
ptr=0x01D5D870, M_left=0x00000000, M_parent=0x01D5D890, M_right=0x00000000, M_color=0, key=100
ptr=0x0028FE40, M_left=0x007A4B80, M_parent=0x007A49A8, M_right=0x007A4BC0, M_color=0, key=1001
ptr=0x01D5D850, M_left=0x007A4B80, M_parent=0x007A4B80, M_right=0x007A4CA0, M_color=1, key=101
```

```cpp
struct tree_node M_header;

size_t M_node_count;

const char* ALOT_OF_TABS="\t\t\t\t\t\t\t\t";

void dump_as_tree(int tabs, struct tree_node *n) {

    void *point_after_struct=(char*)n+sizeof(struct tree_node);

    printf("%d\n", (int*)point_after_struct);

    if (n->M_left) {

        printf("%.s-------", tabs, ALOT_OF_TABS);

        dump_as_tree(tabs+1, n->M_left);

    }

    if (n->M_right) {

        printf("%.s-------\

dump map and set ((struct tree_struct *)(void*)&s);

        printf("\n");

    }

};
```

# 列表 3.121: GCC 4.8.1

```
123, 456 has been inserted

root---123

       R----456

11, 12 has been inserted

root---123

       L----12

       R-----

       R----456

100, 101 has been inserted

root---123

       L----12

       L----11

       R----100

       R----456

       R----1001

667, 1, 4, 7 has been inserted

root---12

       L----4

       L----1

       R----11

       L----7

       R----123

       L----100

       R----667

       L----456

       R----1001
```

## 3.21.5 内存

有时你可能会从 C++ 程序员那里听到“在栈上分配内存”和/或“在堆上分配内存”。

在栈上分配对象：

```cpp
void f()
{
    ...
    Class o=Class(...);
    ...
};
```

如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

对象的（或结构体的）内存分配在栈上，使用简单的 `SP` 偏移。内存会在函数退出时被释放，或者更准确地说，在作用域结束时——`SP` 回到其初始状态（与函数开始时相同），并且 `Class` 的析构函数会被调用。以同样的方式，C 中分配的结构体内存会在函数退出时释放。

在堆上分配对象：

```cpp
void f1() {
  ...
  Class *o=new Class(...);
}

void f2() {
  ...
  delete o;
}
```

这是 `malloc()` 的封装，而 `delete` 是 `free()` 的封装。由于内存块已在堆上分配，因此必须使用 `delete` 进行显式释放。在那个时刻正之前，`Class` 的析构函数会被自动调用。

哪种方法更好？在栈上分配非常快，适用于仅在当前函数使用的小型、短生命周期对象。

在堆上分配较慢，适用于跨越多个函数使用的长周期对象。此外，在堆上分配的对象容易发生内存泄漏，因为它们必须显式释放，但人们可能会忘记。

无论如何，这取决于个人喜好。

## 3.22 负数组索引

可以通过提供负索引来访问数组之前的空间，例如 `array[-1]`。

### 3.22.1 从末尾访问字符串

Python 语言允许从末尾访问数组和字符串。例如，`string[-1]` 返回最后一个字符，`string[-2]` 返回倒数第二个字符，以此类推。难以置信，但在 C/C++ 中也是可能的。

> 如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

```cpp
#include <string.h>
#include <stdio.h>

int main() {
    char *s="Hello, world!";
    char *s_end=s+strlen(s);
    printf("last character: %c\n", s_end[-1]);
    printf("penultimate character: %c\n", s_end[-2]);
}
```

它是行得通的，`s_end` 在字符串末尾始终有一个终止字节。如果字符串的大小发生变化，则必须更新 `s_end`。这个技巧很不可靠，再次强调，这只是负索引的演示。

### 3.22.2 从末尾访问某种块

让我们回想栈是如何向后增长的（第 91 页）。内存中某种块，你想要同时存储堆和栈，并且你不确定它们在运行时会增长多大。你有一个指向块起始位置的堆指针，然后你可以将栈指针设置为块的末尾（`heap + size_of_block`），然后你就可以像 `stack[-n]` 那样访问第 n 个元素。例如，`stack[-1]` 是第一个元素，`stack[-2]` 是第二个。

这将以相同的方式工作，就像我们从末尾访问字符串的技巧一样。你可以轻松检查结构是否有重叠：只需确保堆的最后一个元素的地址低于栈的最后一个元素的地址即可。遗憾的是，`-0` 不可行，因为补码允许表示零，因此它无法与正零区分来。这种方法在 Jim Gray 1993 年的《事务处理》（"The Tuple-Oriented File System"）第 75 页中也有提到。

### 3.22.3 数组从末尾开始

Fortran 和数学由于传统将第一个元素定义为 1。其他语言如 C/C++ 定义为 0。Dijkstra 认为后者更好。但程序员可能仍然带有 Fortran 的习惯，使用这个小技巧可以访问 C/C++ 的第一个元素索引：

> https://www.cs.utexas.edu/users/transcriptions/EWD31.html

如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

```cpp
#include <stdio.h>

int main() {
    int random_value=0x12334;
    unsigned char array[10];
    int i;
```
