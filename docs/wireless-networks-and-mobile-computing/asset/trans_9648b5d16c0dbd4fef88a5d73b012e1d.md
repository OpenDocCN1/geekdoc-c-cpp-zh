
- [10] K. Nakano 和 S. Olariu，“自组网的随机初始化协议”，*IEEE Trans. Parallel Distributed Systems*，第 11 卷，第 749–759 页，2000 年。

- [11] K. Nakano 和 S. Olariu，“无线网络的统一领导者选举协议”，*IEEE Trans. Parallel and Distributed Systems*，第 13 卷，第 516–526 页，2002 年。

- [12] K. Nakano 和 S. Olariu，“无线网络领导者选举协议综述”，*Proc. Intl. Symp. on Parallel Architectures, Algorithms, and Networks (I-SPAN)*，第 71–76 页，2002 年 5 月。

- [13] K. Sinha、S. Ghose 和 P. K. Srimani，“移动自组网的快速确定性广播与闲聊算法”，*J. Parallel Distributed Computing*，第 68 卷第 7 期，第 922–938 页，2008 年 7 月。

- [14] K. Sinha 和 P. K. Srimani，“基于广度优先遍历的移动自组网广播与闲聊算法”，*Proc. 6th International Workshop on Distributed Computing (IWDC)*，计算机科学讲义 3326，Springer，第 459–470 页，2004 年 12 月。

- [15] K. Sinha 和 P. K. Srimani，“自组网的确定性广播与闲聊算法”，*J. Supercomputing* 第 37 卷第 2 期，第 115–144 页，2006 年。

- [16] M. Chrobak、L. Gasieniec 和 W. Rytter，“无线网络中的快速广播与闲聊”，*Proc. 41st IEEE Symp. Found. of Computer Science*，第 575–581 页，2000 年。

- [17] A. E. F. Clementi、A. Monti 和 R. Silvestri，“轮询调度是无线网络容错广播的最优方案”，*Proc. 9th Annual European Symp. on Algorithms*，第 452–463 页，2001 年。

- [18] 网络模拟器，http://www.isi.edu/nsnam/ns，2006 年。

- [19] Bonn 移动性与网络套件，http://web.informatik.uni-bonn.de/IV/bonet/BonMotion.htm，2006 年。

- [20] T. Clausen、P. Jacquet、A. Laouiti、P. Muhlethaler、A. Qayyum 和 L. Viennot，“优化的链路状态路由协议”，*Proc. IEEE INMIC*，巴基斯坦拉合尔，2001 年 12 月。

- [21] C. E. Perkins 和 P. Bhagwat，“面向移动计算机的高度动态目的序号距离矢量路由（DSDV）”，*Computer Communications Review*，第 24 卷，第 234–244 页，1994 年 10 月。

- [22] M. R. Pearlman 和 Z. J. Haas，“确定区域路由协议的最佳配置”，*IEEE J. Selected Areas in Communications*，第 17 卷，第 1395–1414 页，1999 年 8 月。

- [23] D. B. Johnson 和 D. A. Maltz，“真正无缝的无线与移动主机联网：自适应无线与移动联网的协议”，*IEEE Personal Communications*，第 3 卷，第 34–42 页，1996 年 2 月。

- [24] C. E. Perkins 和 E. M. Royer，“自组网按需距离矢量路由”，*Proc. 2nd IEEE Workshop on Mobile Computing Systems and Applications*，第 90–100 页，1999 年。

- [25] V. Park 和 S. Corson，“时间顺序路由算法（TORA）第 1 版功能规范”，*Internet Draft*，draft-ietf-manet-tora-spec-01.txt，1998 年 8 月 7 日。

## 第 6 章

### 无线局域网

- 6.1 引言 ..... 321
- 6.1.1 关联问题 ..... 323
- 6.1.2 不同的关联策略 ..... 324
- 6.1.2.1 最强信号优先（SSF）关联 ..... 325
- 6.1.2.2 基于最大效用的关联 ..... 326
- 6.1.2.3 最大最小公平（MMF）分配 ..... 327
- 6.1.2.4 最轻负载优先（LLF） ..... 327
- 6.1.2.5 最小最大负载均衡分配 ..... 328
- 6.1.2.6 基于链路速率和吞吐量的关联 ..... 328
- 6.1.2.7 基于 RSSI 和带宽的关联 ..... 329
- 6.1.2.8 无线接入技术关联 ..... 329
- 6.2 AP 的布置与信道分配 ..... 329
- 6.3 练习 ..... 330
- 参考文献 ..... 331

无线局域网（*WLAN*）通过无线电波而非线缆基础设施来提供与位置无关的网络访问。

### 6.1.2 不同的关联策略

当存在多个 *APs* 时，某个 *STA* 对 *AP* 的选择会严重影响其自身及其他 *STA* 的性能。关联策略是一种算法，*STA* 基于该算法与其覆盖范围内的 *AP* 建立关联。众多研究者开展了广泛研究，基于不同的度量与目标来寻找 *STAs* 与 *APs* 之间可行的关联。Kumar 等人 [2] 研究了 *STAs* 与 *APs* 之间的最优关联策略，目标是最大化关联吞吐量，但通过假设 *APs* 的频率规划合理而忽略了同信道干扰。许多研究者提倡负载均衡以优化性能。已有研究 [3, 6, 5] 表明，基于接收信号强度指示（*RSSI*）测量的传统关联方式可能因不同 *APs* 间的负载分布不均而导致较差的用户体验。为解决该问题，一些 *AP* 接入控制机制被提出 [5, 6]。Bejerano 等人 [3] 提出了一种同时考虑负载均衡与公平性的关联模型，其中包含一个复杂的集中式 *AP* 关联机制。

与传统的 *RSSI* 不同，有人提出了一种启发式方法，帮助用户根据已与该 *AP* 关联的用户数以及平均 *RSSI* 来选择要关联的 *AP* [4]。

Vasudevan 等人 [7] 提出了一种 *AP-STA* 关联策略，该策略基于某个 *STA* 在与该 *AP* 关联后可能获得的带宽。在用户关联到某个 *AP* 之前，它会通过被动测量估计相邻 *APs* 的潜在带宽，并选择潜在带宽最高的 *AP* 进行连接。

在 [12] 中，提出了一种 *AP* 关联策略。在某个 *STA* 关联到 *AP* 之前，它会计算所有 *STAs* 的最小吞吐量。该 *STA* 找到其关联 *AP*，使得所有 *STAs* 的最小吞吐量最大化。

在 [9] 中，AP 选择被建模为二部图中的多对一匹配问题，以最大化所有 AP 的总负载。

另一种关联策略 [10] 考虑了某个 STA 在加入某个 AP 之前的吞吐量退化。该度量是提供给新 STA 的吞吐量与已关联到相关 AP 的 STA 平均传输时间的加权和。

下面我们在各种 MAC 调度策略下再描述几种关联策略。

#### 6.1.2.1 最强信号优先（SSF）关联

最强信号优先（SSF）是最简单的关联策略之一，它基于由接收信号强度指示（RSSI）测得的最高信噪比这一度量。根据该策略，一个 STA 与它能接收到最强信号的 AP 关联。如 [4] 所述，获取该度量的过程很简单。STA 扫描区域内每个 AP 的可用信道，并监听信标帧或探测响应帧。视国家/地区而定，每个 AP 可能有 1 到 14 个信道。STA 会存储信标帧或探测响应帧的 RSSI 以及其他相关信息（例如，加密是否开启）。扫描过程结束后，如果所选 AP 还能满足其他要求（通常是扩展服务集标识（ESSID）、有线等效保密（WEP）加密），STA 会选择具有最大 RSSI 的 AP。当 RSSI 低于预定义阈值时，STA 将离开该 AP。该过程基于“所选 AP 的服务质量最佳”这一前提。然而，该过程的结果是：许多站点连接到少数几个 AP，而邻近的 AP 却处于空闲状态。这种由负载分布不均导致的 AP 过载将引起性能下降 [3, 6, 5]。

#### 6.1.2.2 基于最大效用的关联

Kumar 等人 [2] 研究了其覆盖范围内 $STAs$ 与 $APs$ 之间的最优关联策略，其中寻找最优关联策略被视为该问题的基于最大效用的表述。作者指出，一个 $STA$ 以某个物理比特率与一个 $AP$ 关联，最终这种关联将产生一个取决于所采用的特定 $MAC$ 调度的 $STA$ 吞吐量。他们使用两种 $MAC$ 调度技术，即随机轮询和比例公平接入，来计算单个关联的吞吐量。根据随机轮询接入，与同一个 $AP$ 关联的 $STAs$ 集合获得相等的个体吞吐量。如果有 $m_j$ 个 $STAs$ $i_1,i_2,\ldots,i_{m_j}$ 与 AP $j$ 关联，且它们以速率 $r_{i_pj}$（$1 \leq p \leq m_j$）关联，则 AP $j$ 服务的所有 $STAs$ 获得的总上行吞吐量为：

$$\frac{m_j}{\displaystyle\sum_{p=1}^{m_j}\frac{1}{r_{i_pj}}}.$$

该 $STA$ 从 AP $j$ 获得的个体吞吐量可表示为

$$t_j=\frac{1}{\displaystyle\sum_{p=1}^{m_j}\frac{1}{r_{i_pj}}}.$$

为了公平分配用户吞吐量，他们使用对数效用函数表示网络总吞吐量，如下所示：

$$\sum_{j=1}^{n}m_j\ln(t_j).$$

基于这些事实，当 $STAs$ 与范围内的 $APs$ 关联，使得所获得的对数和
