
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef unsigned long ub4;
typedef unsigned char u8;

static const ub4 crctab[256] = {
    0x00000000, 0x70703906, 0xe0e0612c, 0x909051ba, 0x0764dc41, 0xc748f8, 0xe96a35d5, 0x9e69a5a3,
    0xedeb8832, 0x97dc78a4, 0xe0d5e512, 0x97d2d9d8, 0x09b64c26, 0xf2eb17c3, 0xe7b82d07, 0xf9b0f9d1,
    0x01d1b7a6, 0xc6a6f207, 0xf2f97147, 0x48b4e1de, 0xa1ad6d74, 0xd6d4ae44, 0xc6a6f2bd, 0xb3d55c7,
    0x138c3b5, 0xc6a4b6c0, 0xfcd0f6cd, 0xc3d2ad01, 0xab13d59, 0x2930a5d, 0xe1401c5f, 0xc63066d9,
    0x0fa7f6d3, 0xb80d080f, 0x36e2b0c3, 0xa5620f8, 0xc290105e, 0x05d6041e, 0xa2677172, 0x3c06e4d1,
    0xa4b4d447, 0xa5a9b5b6, 0xb3a5b5a4, 0x55a5553, 0xf9b0cf90, 0xc32b0c6, 0xa4d5f7c5, 0xfcd0f6cd,
    0xc3d2ad015, 0x2930c4d9, 0x5e100e34, 0xc8c57810, 0xfdb06b16, 0x21b4f4b5, 0xf5f05808, 0xc606d9d2,
    0xb10e9294, 0xb9b0d9a5, 0x2202b9e2, 0xf5d102a2, 0xe67777d1, 0x764c1d9, 0x01db7106, 0x98d220c5,
    0xf5d102a2, 0xf1b18589, 0xa6b6b51f, 0x9fbf4ea5, 0xe3bbd431, 0xc78079c4, 0xe7f0f934, 0xa9609a88,
    0xe10e981e, 0x7f60adb, 0x08d3d2d, 0x9164c97, 0xe6635c01,
    0xb66b51f4, 0x1c2c612, 0x856538d8, 0xf262004e, 0x6c0695ed,
    0xb1b15a7b, 0x8208f4c1, 0x50cf457, 0x65bd09c6, 0xc1b2e950,
    0xb38beea, 0x7f98b27, 0x62c31d2, 0x15da24d9, 0xd3c7fc3,
    0x8d44c655, 0x40db2158, 0xa33551c6, 0xa3bc00c74, 0x44b3b0e2,
    0x92a7766a, 0x34d8057, 0xf6b1333, 0xd4c38f74, 0xa529d0b6,
    0xa34d9ef6, 0x88f7a6de, 0xb0d44a4, 0xa4042d73, 0x373031de5,
    0xa0a4c5f3, 0xd0dd7c79, 0x950871c3, 0xe230f724, 0xaeeb01b10,
    0xc9e20c8b, 0x7f59911, 0x5678b25, 0xb5f0b96, 0xc042011
};

/* 如何从多项式 0xed83 派生表中的值 */
void build_table() {
    ub4 i, j;
    for (i = 0; i < 256; i++) {
        j = i;
        for (int k = 0; k < 8; k++) {
            j = (j >> 1) ^ (j & 1 ? 0xed83 : 0);
        }
        crctab[i] = j;
    }
}

/* 哈希函数 */
ub4 crc(const void *key, ub4 len, ub4 hash) {
    ub4 i;
    const ub4 *k = key;
    for (hash = len, i = 0; i < len; ++i)
        hash = (hash >> 8) ^ crctab[hash & 0xff] ^ k[i];
    return hash;
}

/* 使用方法，尝试 -gcc crc.c -o crc; echo "hello" | ./crc */
int main() {
    char s[1000];
    while (gets(s)) printf("%.0lx\n", crc(s, strlen(s)));
    return 0;
}
```

我们只对 `crc()` 函数感兴趣。顺便说一下，注意 `for()` 语句中的两个初始化器：`hash=len`；C/C++ 标准允许这样做，当然。生成的代码在循环的初始化部分将包含两个操作。

让我们在 MSVC 开启优化 (/O) 时进行比较。为了简见，这里列出了 `crc` 函数，并附带我的注释。

```assembly
crc PROC

mov edx, DWORD PTR [esp-4]
xor ecx, ecx ; i 将存储在 ECX 中
mov eax, edx
test edx, edx
jbe SHORT $LN1@crc
push edi
push esi
mov esi, DWORD PTR [esp+4] ; esi = key
push edi

$LN1@crc:
; 使用字节操作，仅使用 32 位寄存器。通过地址 key+i
存入 EDI
movz edi, BYTE PTR [ecx+esi]
mov ebx, eax ; EBX = (hash = len)
and ebx, 255 ; EBX = hash & 0xff

xor edi, ebx (EDI=EDI^EBX)
; 此操作使用了每个寄存器的所有 32 位
; 其他位 (8-31) 总是会被清零，所以没问题
; 这些位被清零是因为对于 EDI，是通过上面的 MOVZ 指令完成的
above
; EBX 的高位是通过 AND EBX, 255 指令清零的 (255 = 0xff);

xor edi, ebx
EAX=>>8; 从哪里产生的 24-31 位将被清零
shr eax, 8;

EAX=E:crctab[EDI*4] - 从 crctab[] 表选择第 EDI 个元素
xor eax, DWORD ptr _crctab[edi*4]
inc ecx             
ret
```

606

```cpp
uint32_t form_IP(uint8_t ip1, uint8_t ip2, uint8_t ip3, uint8_t ip4)
{
    return (ip1<<24) | (ip2<<16) | (ip3<<8) | ip4;
}
```

```cpp
void print_as_IP(uint32_t a)
{
    printf("%d.%d.%d.%d\n",
        (a>>24)&0xFF,
        (a>>16)&0xFF,
        (a>>8)&0xFF,
        (a&0xFF));
}
```

```cpp
// bit=31..0
uint32_t set_bit(uint32_t input, int bit)
{
    return input|(1<<bit);
}
```

```cpp
uint32_t form_netmask(uint8_t netmask_bits)
{
    uint32_t netmask=0;
    uint8_t i;

    for (i=0; i<netmask_bits; i++)
        netmask=set_bit(netmask, 31-i);

    return netmask;
}
```

```cpp
void calc_network_address(uint8_t ip1, uint8_t ip2, uint8_t ip3, uint8_t ip4, uint8_t netmask_bits)
{
    uint32_t netmask=form_netmask(netmask_bits);
    uint32_t ip=form_IP(ip1, ip2, ip3, ip4);
    uint32_t net_adr;

    printf("netmask=%s\n",
        print_as_IP(netmask);

    net_adr=ip&netmask;

    printf("network address=%s\n",
        print_as_IP(net_adr);
}
```

```cpp
int main ()
{
    calc_network_address(10, 1, 2, 4, 24); // 10.1.2.4, /24
    calc_network_address(10, 1, 2, 4, 8); // 10.1.2.4, /8
    calc_network_address(10, 1, 2, 4, 25); // 10.1.2.4, /25
    calc_network_address(10, 1, 2, 4, 26); // 10.1.2.4, /26
}
```

如果你发现任何拼写错误、错误或有任何建议，请随时给我留言：我的邮件。谢谢！

## 3.9.1 `calc_network_address()` 函数是最简单的：它只需将主机地址与子网掩码进行与（AND）运算，从而得到网络地址。

列表 3.10：优化 MSVC 2012 /Ob0

```asm
ip1$ = 8          size = 1
ip2$ = 12         size = 1
ip3$ = 16         size = 1
ip4$ = 20         size = 1
netmask_bits$ = 24  size = 1
calc_network_address PROC
    push edi
    push DWORD PTR _netmask_bits$[esp]
    push form_mask
    call OFFSET $63045 ; 'netmask='
    mov eax, edi
    call DWORD PTR _imp_prinf
    push edi
    call _print_as_IP
    push OFFSET $63046 ; 'network address='
    call DWORD PTR _imp_prinf
    push ip4$[esp+16]
    push DWORD PTR ip3$[esp+20]
    push DWORD PTR ip2$[esp+24]
    push DWORD PTR ip1$[esp+28]
    call _form_IP
    and eax, edi ; network address = host address & netmask
    push eax
    call _print_as_IP
    add esp, 36
    pop edi
    pop ebp
    ret 0
calc_network_address END
```

在第 22 行，我们看到了最重要的 AND 运算——在这里计算了网络地址。

## 3.9.2 `form_IP()` 函数仅仅是将所有 4 个字节放入一个 32 位的值中。

`form_IP()` 的实现通常如下：

这里是通常的写法：

- 为返回值分配一个变量。将其设置为 0。
- 取第四个（最低位）字节，对该字节进行或（OR）运算并返回该值。现在返回值包含了该第 4 字节。
- 取第三个字节，将其向左移 8 位。你将得到一个类似 `0x0000bb00` 的值，其中 `bb` 是它的第三个字节。对结果值和返回值进行或运算。到目前为止返回值包含了 `0x000000aa`，所以对值进行或运算将产生一个类似 `0x0000bbaa` 的值。
- 取第二个字节，将其向左移 16 位。你将得到一个类似 `0x00cc0000` 的值，其中 `cc` 是它的第二个字节。对结果值和返回值进行或运算。到目前为止返回值包含了 `0x0000bbaa`，所以对值进行或运算将产生一个类似 `0x00ccbbaa` 的值。
- 取第一个字节，将其向左移 24 位。你将得到一个类似 `0xdd000000` 的值，其中 `dd` 是它的第一个字节。对结果值和返回值进行或运算。到目前为止返回值包含了 `0x0000bbaa`，所以对值进行或运算将产生一个类似 `0xccbbaa` 的值。

这是未优化的 MSVC 2012 代码：

列表 3.11：未优化的 MSVC 2012
