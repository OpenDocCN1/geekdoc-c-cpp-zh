
## MSVC 与 GCC 的 `std::list` 实现差异

```assembly
lea ecx, DWORD PTR l$[esp+36]
mov DWORD PTR l$[esp+40], 0
```

```assembly
; 分配第一个元素
call ??$ynodeO$List_base_types@@@V@@$allocator@@@std@@@QPAU>>
std::List<base_types,std::allocator<>>::node(
mov eax, DWORD PTR _imp_int
mov ebx,
push OFFSET a86; 空列表:
mov dword [esp+32], ebx
call esi; 打印
lea eax, DWORD PTR [esp+32]
push ebx
call ??$dump_listvalYAXPAI@
mov esi,DWORD PTR [ebx]
add esp, 8
lea eax, DWORD PTR [esp+28]
push eax
push DWORD PTR [esi+4]
lea eax, DWORD PTR [esp+36]
push esi
mov dword ptr [esp+44], 1 ; 新节点的数据
mov dword ptr [esp+44], 2 ; 新节点的数据
; 分配 new_node
call ??$ynodeAAU$List_buy@@@V@@$allocator@@@std@@@QPAU>>
std::List<a,std::allocator<a>>::node(a,std::allocator<a> >): nodeode<a const &
mov ebx,DWORD PTR [esi+4]
mov eax,DWORD PTR [eax+4]
mov dword ptr [esp+28], 3 ; 新节点的数据
mov dword ptr [ecx],eax
```

```assembly
push OFFSET $SG40862 ; '3rd element: %d %d'
call edi ; printf
mov esi, DWORD PTR [esi+4] ; operator-: get ->prev pointer
push DWORD PTR [esi+12]
push DWORD PTR [esi+8]
push OFFSET $SG40864 ; '2nd element: %d %d'
call edi ; printf
mov eax, DWORD PTR [eax+4] ; operator-: get ->prev pointer
mov DWORD PTR [eax+12]
mov DWORD PTR [eax+8]
push OFFSET $SG40866 ; '1st element: %d %d'
call edi ; printf
add esp, 64
push OFFSET $SG40867 ; 'removing last element...'
call edi ; printf
mov edx, DWORD PTR [ebx+4]
add esp, 4
; prev=next?
; it is the only element, garbage one?
; if yes, do not delete it!
cmp edx, ebx
je SHORT $LN39main
mov eax, DWORD PTR [edx+4]
mov DWORD PTR [edx]
mov eax, DWORD PTR [ecx], eax
mov ecx, DWORD PTR [edx]
push eax
mov DWORD PTR [ecx+4], eax
call ??3@YXPAX@Z ; operator delete
add esp, 4
mov DWORD PTR l$[esp+32], 28
$LN39main:
lea eax, DWORD PTR l$[esp+28]
push eax
call 73@Dump_List@YXPAX@Z ; dump_val
mov eax, DWORD PTR [ebx]
add esp, 4
mov edx, DWORD PTR [ebx], ebx
mov DWORD PTR [ebx+4], eax
cmp eax, ebx
je SHORT $LN414main
$LN414main:
mov esi, DWORD PTR [eax]
push eax
call 73@YXPAX@Z ; operator delete
add esp, 4
mov eax, esi
cmp esi, ebx
jne SHORT $LL414main
$LN412main:
push ebx
call    ??@YAXPAX@Z; operator delete
add     esp, 4
xor     eax, eax
pop     edi
pop     esi
pop     ebx
add     esp, 16
ret     0
main ENDP
```

与 GCC 不同，MSVC 的代码通过 `Buynode` 函数在函数开头分配占位元素，该函数也用于分配其余的节点（GCC 的代码在本地栈上分配第一个元素）。

### 列表 3.15：完整输出

- **空列表：**
  Myhead=0x0033C258 Size=0
  ptr=0x0033C258 Next=0x0033C258 Prev=0x0033C258 x=6226002 y=4522072

- **3个元素的列表：**
  Myhead=0x0033C258 Size=3
  ptr=0x0033C258 Next=0x0033C288 Prev=0x0033C2A0 x=6226002 y=4522072
  ptr=0x0033C288 Next=0x0033C270 Prev=0x0033C258 x=3 y=4
  ptr=0x0033C270 Next=0x0033C2A0 Prev=0x0033C288 x=1 y=2
  ptr=0x0033C270 Next=0x0033C2A0 Prev=0x0033C270 x=5 y=6
  节点位于：
  ptr=0x0033C288 Next=0x0033C270 Prev=0x0033C258 x=3 y=4
  节点位于 `.end`：
  ptr=0x0033C258 Next=0x0033C288 Prev=0x0033C2A0 x=6226002 y=4522072

- **让我们从头开始：**
  第1元素：3 4
  第2元素：1 2
  第3元素：5 6
  位于 `.end()` 的元素：6226002 4522072

- **让我们从尾开始：**
  位于 `.end()` 的元素：6226002 4522072
  第3元素：5 6
  第2元素：1 2
  第1元素：3 4

- **删除最后一个元素：**
  Myhead=0x0033C258 Size=2
  ptr=0x0033C258 Next=0x0033C288 Prev=0x0033C270 x=6226002 y=4522072
  ptr=0x0033C288 Next=0x0033C270 Prev=0x0033C258 x=3 y=4
  ptr=0x0033C270 Next=0x0033C2A0 Prev=0x0033C270 x=5 y=6

## std::forward_list

与 `std::list` 相同，但它是单链表，即节点只有一个 `next` 字段。它的内存占用更小，但不支持反向遍历。如果你发现错误或建议，请随时联系。

## std::vector

我们定义的 `std::vector` 是对 POD（Plain Old Data）数组的安全封装。在内部，它与 `std::string` 相似：它有一个指向分配缓冲区末尾的指针。数组元素在内存中是连续的，就像普通数组一样。堆分配的缓冲区可以比数组大。C++ 有一个新方法 `.data()`，返回缓冲区的指针，就像 `std::string` 的 `.c_str()`。MSVC 和 GCC 的实现相似，但结构字段略有不同，这里是适用于两种编译器的代码。这是 `std::vector` 结构的输出：

```cpp
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <functional>

struct vector_of_ints {
    // MyFirst:
    int *MyFirst;
    int *MyLast;
    int *Myend;
    // GCC 结构相同，但名称为：
    // start, finish, end
};

void dump(vector_of_ints *in) {
    printf("*MyFirst=%p, *MyLast=%p, *Myend=%p\n", in->MyFirst, in->MyLast, in->Myend);
    size_t size=(in->MyLast-in->MyFirst);
    size_t capacity=(in->Myend-in->MyFirst);
    printf("size=%zu, capacity=%zu\n", size, capacity);
    for (size_t i=0; i<size; i++) {
        printf("element %zu: %d\n", i, in->MyFirst[i]);
    }
}

int main() {
    std::vector<int> c;
    dump((vector_of_ints*)(void*)&c);
    c.push_back(1);
    dump((vector_of_ints*)(void*)&c);
    c.push_back(2);
    dump((vector_of_ints*)(void*)&c);
    c.push_back(3);
    dump((vector_of_ints*)(void*)&c);
    c.push_back(4);
    dump((vector_of_ints*)(void*)&c);
    c.reserve(6);
    dump((vector_of_ints*)(void*)&c);
    c.push_back(5);
    dump((vector_of_ints*)(void*)&c);
    c.push_back(0);
    printf("%d\n", c.at(5)); // at[5], 带边界检查
    printf("%d\n", c[8]); // operator[1], 不带边界检查
}
```

GCC 内部：http://gcc.gnu.org/on/libstdc++/libstdc++-4.4/013.html

如果你发现错误或建议，请随时联系。谢谢！

这是在 MSVC 中编译的输出：

```
Myfirst=00000000, Myend=00000000
size=0, capacity=0
Myfirst=0051CF48, Myend=0051CF4C, Myend=0051CF4C
size=1, capacity=1
element 0: 1
Myfirst=0051CF58, Myend=0051CF60, Myend=0051CF60
size=2, capacity=2
element 0: 1
element 1: 2
Myfirst=0051C278, Myend=0051C284, Myend=0051C284
size=3, capacity=3
element 0: 1
element 1: 2
element 2: 3
Myfirst=0051C290, Myend=0051C2A0, Myend=0051C2A0
size=4, capacity=4
element 0: 1
element 1: 2
element 2: 3
element 3: 4
Myfirst=0051B180, Myend=0051B194, Myend=0051B198
size=5, capacity=6
element 0: 1
element 1: 2
element 2: 3
element 3: 4
element 4: 5
Myfirst=0051B180, Myend=0051B198, Myend=0051B98
size=6, capacity=6
element 0: 1
element 1: 2
```

如所示，在 `main()` 之前没有分配缓冲区。在第一次调用 `push_back()` 之后，分配了一个缓冲区。然后，每次 `push_back()` 调用，数组的大小和容量都会增加。但缓冲区地址的改变是一项昂贵的操作，因为 `push_back()` 会重新分配内存。`reserve()` 方法可以预留足够的内存，从而避免这种频繁的重新分配。`at()` 带边界检查，而 `operator[]` 则不带。这展示了 `std::vector` 结构在索引越界时会抛出 `std::out_of_range` 异常，而 `operator[]` 则不会。

```assembly
lea ecx, DWORD PTR _c[ebp]
call ?push_back@$std@@allocator@Hstd@std@@QAEX$$QAHZ;
std::vector<int,std::allocator<int>>::push_back
lea edx, DWORD PTR __c[ebp]
push edx
call ?7dump@@YPAUvector_of_ints@@@Z; dump
add esp, 4
push 6
lea ecx, DWORD PTR __c[ebp]
call ?reserve@$vector@HV?$allocator@Hstd@std@@QAEXI@;
std::vector<int,std::allocator<int>>::reserve
lea edx, DWORD PTR __c[ebp]
push edx
call ?7dump@@YPAUvector_of_ints@@@Z; dump
add esp, 4
mov edx, DWORD PTR T2[ebp], 5
lea eax, DWORD PTR T2[ebp]
push edx
lea ecx, DWORD PTR __c[ebp]
call ?push_back@$vector@HV?$allocator@Hstd@std@@QAEX$$QAHZ;
std::vector<int,std::allocator<int>>::push_back
lea edx, DWORD PTR __c[ebp]
push edx
call ?7dump@@YPAUvector_of_ints@@@Z; dump
add esp, 4
mov edx, DWORD PTR T1[ebp], 6
lea eax, DWORD PTR T1[ebp]
push edx
lea ecx, DWORD PTR __c[ebp]
call ?push_back@$vector@HV?$allocator@Hstd@std@@QAEX$$QAHZ;
std::vector<int,std::allocator<int>>::push_back
lea edx, DWORD PTR __c[ebp]
push edx
call ?7dump@@YPAUvector_of_ints@@@Z; dump
add esp, 4
push 5
lea ecx, DWORD PTR __c[ebp]
call ?7add@$vector@HV?$allocator@Hstd@std@@QAEAHI@;
std::vector<int,std::allocator<int>>::at
mov edx, DWORD PTR [eax]
push OFFSET SG552650 ; '%d'
call DWORD PTR _imp_printf
add esp, 8
mov eax, 8
shl eax, 2
mov ecx, DWORD PTR _c[ebp]
mov edx, DWORD PTR [ecx+eax]
push OFFSET SG552651 ; '%d'
call DWORD PTR _imp_printf
add esp, 8
lea ecx, DWORD PTR __c[ebp]
call ?7Tidy@$vector@HV?$allocator@Hstd@std@@IAEXXX;
std::vector<int,std::allocator<int>>::Tidy
```

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

```assembly
xor  eax, eax
mov  esp, ebp
pop  ebp
ret  0
main ENDP
```

我们看到了 `.at()` 方法是如何检查边界并在出错时抛出异常的。最后一个 `printf()` 的数字直接从内存中取出，没有任何任何更改。

人们可能会问，为什么不像在 `std::string` 中那样使用 `size` 和 `capacity` 变量呢？据这样做是为了更快的边界检查。

GCC 生成的代码通常几乎相同，但 `.at()` 方法是内联的（inline）：

### Listing 3.117: GCC 4.8.1 - -fno-inline-small-functions -O1

```assembly
main proc near
push  ebp
mov  esp, esp
mov  edi, esp
push  esi
push  ebx
and  esp, 0xFFFFFF0h
sub  esp, 20h
mov  dword ptr [esp+14h], 0
mov  dword ptr [esp+18h], 0
mov  dword ptr [esp+1Ch], 0
```
