
# 无线网络和移动计算

2: /* 首先接收一个长度为 len + 1 的 RBNS 数据帧 */
3: /* 然后将其转换为等价的二进制值 */
4: RBN 向量 recv_buf：数组 [0..len]；▷ 接收到的 RBNS 数据帧
5: 位向量 out_buf：数组 [0..len]；▷ 输出二进制帧
6: /* 接收数据帧 */
7: 调用 ReceiveRBNDataFrame(recv_buf, len);
8: 调用 ConvertRBNtoBinary(recvbuf, len, out_buf);
9:

10: /* out_buf 中的二进制数据为 len + 1 位。最高有效位（msb） */
11: /* 可以忽略，因为它始终为 0，只需返回低阶 len 位 */
13: end procedure

1: procedure RECEIVERBNDATAFRAME(INOUT recv_buf, IN len)
2: /* null 表示信道中无信号 */
3: /* time_slot[i] 指的是第 i 个时间槽 */
4: for i = 0 to len do
5: if time_slot[i] = null then
6: recv_buf[i] ← 0；▷ 信道在第 i 个时间槽期间为 null
7: else
8: recv_buf[i] ← time_slot[i]；▷ 在第 i 个时间槽中接收到 1 或 0
9: end if
10: end for
11: end procedure

1: procedure CONVERTRBNTOBINARY(IN recv_buf, IN len, INOUT out_buf)

2: /* 将接收到的 RBNS 数据帧转换为二进制数据 */
3: /* 最终的二进制数据将存放在 `out_buf` 中 */
4: **boolean** `runflag : false;`
5: `runflag ← false;`  ▷ 用于解码 1 的连续段
6: **for** `i = 0` **to** `len` **do**
7: &nbsp;&nbsp;&nbsp;&nbsp;**repeat**
8: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**if** `recv_buf[i] = 1` **then**
9: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**if** `runflag = false` **then**
10: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`runflag ← true;`
11: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`out_buf[i] ← 1;`  ▷ 第 i 位输出 1
12: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**else**
13: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`out_buf[i] ← 0;`  ▷ 规则 2 的减少结果
14: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**end if**
15: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**end if**
16: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**if** `recv_buf[i] = 1` **then**
17: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**if** `runflag = true` **then**
18: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`out_buf[i] ← 0;`  ▷ 第 i 位输出 0
19: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`runflag ← false;`  ▷ 1 的连续段结束
20: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**else**
21: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`out_buf[i] ← 1;`  ▷ 单独的 1
22: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**end if**
23: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**end if**
24: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**if** `recv_buf[i] = 0` **then**
25: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**if** `runflag = true` **then**
26: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`out_buf[i] ← 1;`  ▷ 处于 1 的连续段内
27: else
28: out_buf[f] ← 0;
29: end if
31: until runflag = false;
32: end for
33: end procedure

作为上述软件实现的替代方案，也可以设计一个简单的硬件电路，实现二进制到 RBNS 串行转换。设 RBN 数字 \(b_i^{rbn}\)（\(0 \leq i \leq n\)）对应给定二进制数的位 _b_i_，可用两位 _x_(_i_) 和 _y_(_i_) 表示，其中 _x_(_i_) 为最高有效位。RBN 数字的编码为：0 用 00，1 用 01，\(\bar{1}\) 用 10，并用 _a_、_b_、_c_、_d_、_e_、_f_ 分别表示 _b_<sub>_i_+2</sub>、_b_<sub>_i_+1</sub>、_b<sub>i</sub>_、_b_<sub>_i_-1</sub>、_b_<sub>_i_-2</sub>、_b_<sub>_i_-3</sub>。

图 8.6 展示了一个代表性硬件电路，用于计算 _x_(_i_) 和 _y_(_i_)，其中 _b_<sub>-3</sub>、_b_<sub>-2</sub>、_b_<sub>-1</sub>、_b<sub>n</sub>_、_b_<sub>_n_+1</sub> 初始化为 0。该电路可用于 **pipelined** 传输方案，即 (_i_+1) 位的转换与第 _i_ 个 RBNS 符号的传输重叠进行。

同样，接收到的 RBNS 数字也可以通过硬件电路串行转换，如图 8.7 所示。线条 _R_<sub>0</sub>、_R_<sub>1</sub> 以及 \(R_\bar{1}\) 假设为逻辑 1 电平。

图 8.6 展示了一个代表性硬件电路，用于计算 _x_(_i_) 和 _y_(_i_)，其中 _b_<sub>-3</sub>、_b_<sub>-2</sub>、_b_<sub>-1</sub>、_b<sub>n</sub>_、_b_<sub>_n_+1</sub> 初始化为 0。该电路可用于 **pipelined** 传输方案，即 (_i_+1) 位的转换与第 _i_ 个 RBNS 符号的传输重叠进行。

图 8.7 展示了一个代表性硬件电路，用于计算 _x_(_i_) 和 _y_(_i_)，其中 _b_<sub>-3</sub>、_b_<sub>-2</sub>、_b_<sub>-1</sub>、_b<sub>n</sub>_、_b_<sub>_n_+1</sub> 初始化为 0。该电路可用于 **pipelined** 传输方案，即 (_i_+1) 位的转换与第 _i_ 个 RBNS 符号的传输重叠进行。

我们现在作出以下观察：

**观察 1.** 通过在传输二进制数据时应用减少规则 1 和 2，可确保传输数据中不出现 $\overline{1}\overline{1}$、$1\overline{1}$ 和 $\overline{1}1$ 这三种数字模式。

**观察 2.** 若原始二进制数据帧为 _n_ 位，RBNS 编码后的帧大小可达 _n+1_ 个 RBNS 数字。

**观察 3.** 编码和解码过程需要从最低有效位扫描到最高有效位，这可以便利地与 **pipelined** 的串行传输和接收同步进行。

因此，可以看出，从二进制到 RBNS 以及从 RBNS 到二进制的硬件转换逻辑复杂度极低。因此，由于编码和解码逻辑带来的延迟和能耗增加，远远不足以显著影响该方案所带来的能耗节约。

# 8.3.2  RBNSiZeComm 通信协议

RBNSiZeComm 通信协议仅包含两个步骤：

1. 使用减少规则 1 和 2 将二进制数据帧重新编码为 RBNS。
2. 发送 RBNS 数据帧，仅在 1 和 \(\bar{1}\) 位上驱动非零电压，而在 0 位上保持静默。

为了区分信道中没有信号和正在进行传输中的 0 位，需要在数据传输开始时发送 *start of transmission* 信号，在数据帧结束时发送 *end of transmission* 信号。

# 8.3.3  能耗节约分析

我们首先计算在应用减少规则 1 后，长度为 \(n\) 的二进制字符串中非零数字的平均个数。为此，我们先统计所有长度为 \(n\) 的由 0、1 组成的字符串中，长度为 \(k\)（\(1 \leq k \leq n\)）的 1 的连续段（即 \(R_k\)）出现的总次数。

我们用 \(R_k\) 表示长度为 \(k\) 的 1 的连续段。显然，两个相邻的 \(R_{k_1}\) 和 \(R_{k_2}\)（\(1 \leq k_1, k_2 \leq n\)）在位串中必须至少被一个 0 分隔。为了便于计数，我们在每个 \(R_k\) 前面附加一个 0，记作 \(y_k\)，并用 \(y_0\) 表示单独的 0。每个 \(y_k\)（\(0 \leq k \leq n\)）的长度为 \(k+1\)。下面介绍两种求解此计数问题的方法：一种是利用生成函数，另一种是利用递推关系。

## 8.3.3.1  生成函数方法

为了求所有长度为 \(n\) 的二进制字符串中 \(R_k\)（\(1 \leq k \leq n\)）出现的总次数，我们首先计算恰好有 \(i_k\) 个 \(y_k\) 的字符串数量，记为 \(N_n^{i_k,k}\)。也就是说，我们只考虑长度为 \(n+1\) 的位串，其中恰好包含 \(i_k\) 个 \(y_k\)。我们需要将整数 \(n+1\) 按有序方式拆分，使得恰好有 \(i_k\) 个长度为 \(k+1\) 的块。每一种有序拆分对应一个唯一的长度为 \(n\) 的位串（因为考虑了前置的 0）。

