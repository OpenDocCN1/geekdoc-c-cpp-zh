

```
    return ptr1+3;
}
```

答案：当调用 test() 时，有 ptr1 = arr，因此指针 ptr1+1 指向 arr[1]。因此，语句 *(ptr1+1) = 10; 使 arr[1] 等于 10。类似地，有 ptr2 = arr+3，因此 ptr2 指向 arr[3]。因此，语句 *(ptr2-1) = 20; 使 arr[2] 等于 20。由于 ptr1 指向 arr，表达式 ptr1+3 返回指向 arr[3] 的指针。因此，arr[3] 变为 30。结果，程序显示：1 10 20 30

## C.11.35 编写一个函数，该函数接收一个整数作为参数（例如 N），并根据公式 F(N) = F(N-1) + F(N-2) 计算斐波那契数列的第 N 项，其中 F(0) = 0，F(1) = 1。编写一个程序，读取一个 2 到 40 之间的整数 N，并使用该函数显示第 N 项。

```
#include <stdio.h>

unsigned int fib(int num);

int main(void)
{
    int num;

    do
    {
        printf("Enter a number between 2 and 40: ");
        scanf("%d", &num);
    } while(num < 2 || num > 40);

    printf("F(%d) = %u\n", num, fib(num));
    return 0;
}

unsigned int fib(int num)
{
    unsigned int term1, term2, sum;

    term1 = 1;
    term2 = 0;
    while(num > 1)
    {
        sum = term1 + term2;

        term2 = term1;
        term1 = sum;
        num--;
    }
    return sum;
}
```

### 注释
已知 F(N) = F(N-1)+ F(N-2)，前几项为 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ... 例如，F(7) = 13，它是 F(6) 与 F(5) 之和。为了计算某一项的值，我们将最近一次的和存入 term1，而将前一次的和存入 term2。

## C.11.36 下列程序的输出是什么？

```c
#include <stdio.h>

double *f(double ptr[]);

int main(void)
{
    int i;
    double a[8] = {0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8};

    printf("%.1f\n", *f(f(f(a))));
    for(i = 0; i < 8; i++)
        printf("a[%d] = %.1f\n", i, a[i]);
    return 0;
}

double *f(double ptr[])
{
    (*ptr)++;
    return ptr+2;
}
```

**答案：** f() 调用按从内到外的顺序执行。第一次调用 f() 时，有 ptr = a = &a[0]。因此，语句 (*ptr)++; 等价于 a[0]++;，并且 a[0] 变为 1.1。

返回值 a+2 在第二次调用中作为参数使用，因此 f(f(a)) 转换为 f(a+2)。因此，a[2] 变为 1.3。类似地，返回值 a+4 在第三次调用中作为参数使用，a[4] 变为 1.5。由于最后一次调用 f() 返回 a[6] 的地址，因此使用 * 运算符显示其值，即 0.7。结果，a 的内容为 1.1 0.2 1.3 0.4 1.5 0.6 0.7 0.8

## C.11.37 编写一个函数，该函数接收一个字符串作为参数，并显示其中包含多少个数字（0-9）、多少个以小写字母（a-z）开头的单词，以及多少个以大写字母（A-Z）开头的单词。编写一个程序，读取一个少于 100 个字符的字符串并调用该函数。

有两个限制。第一个是在函数内部使用指针表示法，第二个是使用 ctype.h 中的函数。请阅读附录 C 中 ctype.h 函数的说明，并选择合适的函数。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int read_text(char str[], int size, int flag);
void parse_str(char str[]);
```

```
int main(void)
{
    char str[100];

    printf("Enter text: ");
    read_text(str, sizeof(str), 1);
    parse_str(str);
    return 0;
}

void parse_str(char s[])
{
    int dig, uplet_wrd, lowlet_wrd;

    dig = uplet_wrd = lowlet_wrd = 0;
    while(*s != '\0')
    {
        while(isspace(*s)) /* Skip the whitespace characters until a word begins. */
            s++;
        if(*s == '\0')
            break;
        /* We check if the word begins with a digit or letter.*/
        if(isdigit(*s))
            dig++;
        else if(isupper(*s))
            uplet_wrd++;
        else if(islower(*s))
            lowlet_wrd++;
        s++;
        if(*s == '\0')
            break;
        while(isspace(*s) == 0) /* Skip the characters of the word; check only for digits. */
        {
            if(isdigit(*s))
                dig++;
            s++;
            if(*s == '\0')
                break;
        }
    }
    printf("UL:%d LL:%d DG:%d\n", uplet_wrd, lowlet_wrd, dig);
}
```

## C.11.38 根据我们的经验，我们经常在“实现通信协议”领域使用 C 语言。例如，我们将向你展示一种创建网络数据帧的方法。在此之前，先介绍一些理论：

位于同一个 Internet 协议（IP）本地网络中的两台计算机 A 和 B，如果双方都知道彼此的物理地址，就可以通信。物理地址称为介质访问控制（MAC）地址。例如，当 A 需要与 B 通信时，它必须知道 B 的 MAC 地址。为了获知该地址，A 应向本地网络发送一个 MAC 帧，其中包含一条称为 ARP_Request 的特殊消息。当 B 收到这个 MAC 帧后，会用另一个 MAC 帧回复 A，其中包含另一条称为 ARP_Reply 的特殊消息。ARP_Reply 包含 B 的 MAC 地址。这样，A 就获知了 B 的 MAC 地址，因此它们可以通信。

编写一个程序，读取 A 的 MAC 地址以及 A 和 B 的 IP 地址，并创建一个包含 ARP_Request 消息的 MAC 帧。程序应按行显示 MAC 帧的内容，其中每行应包含 16 个字节，以十六进制格式表示。MAC 地址由六个八位组（字节）组成，应以 x.x.x.x.x.x 的形式输入（每个 x 是 [0, 255] 范围内的整数）；IP 地址由四个八位组组成，应以 x.x.x.x 的形式输入。图 11.2 显示了 MAC 帧的格式：

- a. 将前导码字段的前七个八位组设置为 85，第八个八位组设置为 171。
- b. 将 MAC 目的地址的六个八位组设置为 255。
- c. 将 MAC 源地址的六个八位组设置为 A 的 MAC 地址。
- d. 将类型字段的第一个八位组设置为 8，第二个八位组设置为 6。
- e. 将 CRC 字段的四个八位组设置为 1。

图 11.3 描绘了 ARP_Request 消息的格式。

- a. 硬件类型字段的长度为两个八位组。第一个八位组为 0，第二个八位组为 1。
- b. 协议类型字段的长度为两个八位组。第一个八位组为 8，第二个八位组为 6。
- c. 硬件长度字段的长度为一个八位组，值为 6。
- d. 协议长度字段的长度为一个八位组，值为 4。
- e. 操作字段的长度为两个八位组。
- f. 将目标硬件地址的六个八位组设置为 0。
- g. 将目标协议地址的四个八位组设置为 B 的 IP 地址。

```
#include <stdio.h>

void Build_Frm(int MAC_src[], int IP_src[], int IP_dst[]);
void Show_Frm(unsigned char pkt[], int len);

int main(void)
{
    int MAC_src[6], IP_src[4], IP_dst[4];
```

![](img/b8da5dcf9ba7f1fad5213c453d095246_375_0.png)

图 11.2
MAC 帧结构。

| 硬件类型 | 协议类型 |
|---|---|
| 硬件长度 | 协议长度 | 操作 请求 1，应答 2 |
| 发送方硬件地址（例如：以太网为 6 字节） |  |
| 发送方协议地址（例如：IP 为 4 字节） |  |
| 目标硬件地址（例如：以太网为 6 字节）（在请求中不填写） |  |
| 目标协议地址（例如：IP 为 4 字节） |  |

图 11.3
ARP 分组结构。

```
printf("Enter src MAC (x.x.x.x.x.x): ");
scanf("%d.%d.%d.%d.%d.%d", &MAC_src[0], &MAC_src[1], &MAC_src[2], &MAC_src[3], &MAC_src[4], &MAC_src[5]);

printf("Enter src IP (x.x.x.x): ");
scanf("%d.%d.%d.%d", &IP_src[0], &IP_src[1], &IP_src[2], &IP_src[3]);

printf("Enter dst IP (x.x.x.x): ");
scanf("%d.%d.%d.%d", &IP_dst[0], &IP_dst[1], &IP_dst[2], &IP_dst[3]);
Build_Frm(MAC_src, IP_src, IP_dst);
return 0;
}

void Build_Frm(int MAC_src[], int IP_src[], int IP_dst[])
{
unsigned char pkt[54] = {85, 85, 85, 85, 85, 85, 85, 171}; /* Initialize the first eight octets of the frame and make zero the rest. */
int i, j;

for(i = 8; i < 14; i++) /* Broadcast MAC address. It is a special address used in Ethernet technology to broadcast the frame. */
pkt[i] = 255;
for(i = 14, j = 0; j < 6; i++, j++)
pkt[i] = MAC_src[j]; /* MAC source. */

pkt[20] = 8; /* Type. */
pkt[21] = 6;

pkt[22] = 0; /* Hardware Type. */
pkt[23] = 1;

pkt[24] = 8; /* Protocol Type. */
pkt[25] = 6;
```

