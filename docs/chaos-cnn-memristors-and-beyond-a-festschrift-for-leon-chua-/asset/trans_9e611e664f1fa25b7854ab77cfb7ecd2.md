

图 13. 等效于图 11 电路的忆阻器电路。

图 14. 与图 13 电路相关的线性电阻电路结构。

相关线性电路结构表示在图 14 中。显然，所有具有图 14 中任一结构的线性电阻电路都有唯一解。这也可以通过定理 3 的准则轻松确认。因此，图 13 的电路在状态变量 q 中具有全局状态方程。在这种简单情况下，它可以显式写出：

dq/dt = E / (R + R(q)) (13)

这清楚地显示了在此上下文中使用本构关系 (6) 而不是 (2) 的优势，因为每个忆阻器只有一个潜在状态变量。

### 示例 4
忆阻器电路中没有忆阻器电荷全局状态方程的最简单示例之一表示在图 15 中。

为简单起见，假设 R(q) 对所有 q 严格为正。然后只有一个相关的线性电阻电路结构，我们已在示例 1 中遇到过。正如我们已展示的，该结构有一对共轭树，但也有电阻的非平凡部分均匀定向。因此，我们怀疑图 15 的电路在忆阻器电荷中没有全局状态方程。

再次，在这种简单情况下，我们可以进行直接分析。我们通过仅使用辅助电流 i1 来走捷径，已考虑到

图 15. 一个没有忆阻器电荷全局状态方程的简单忆阻器电路。

零电流的零化器和基尔霍夫电流定律。考虑到零化器的零电压和基尔霍夫电压定律，我们可以写出

E + R1 i1 = R(q) i  
R2 i1 = R3 i (14)

求解 i：

i = E / (R(q) - (R1 R3)/R2) (15)

因此状态方程应为

dq/dt = E / (R(q) - (R1 R3)/R2) (16)

显然，在 (16) 右端分母消失的 q 值处，状态方程甚至在局部也不存在，并且这些 q 值不定义解。在所有其他 q 值处，状态方程在局部存在且 q 确定一个解。

实际上，通过讨论 (16) 右端的符号，可以理解解的定性行为。假设在忆阻器的原始本构关系 (2) 中，函数 g 是 S 型函数（图 16，左）。其导数出现在本构关系 (6) 中，表示在图 16，右。我们假设线性电阻使得 R1 R3 / R2 位于 R(q) 的最小值和最大值之间（图 16，右）。这给出了图 17 中 (16) 右端作为 q 的函数的定性图以及解在 q 轴上的运动方向。

因此，可以得出关于解的定性行为的以下结论：

- 从 q1 或 q2 开始的解不存在，因为相应的忆阻器电流是无限的。即使我们接受 q 的无限导数，解在 q2 中也不存在，在 q1 中也不唯一（观察方向

它们必须被消除以获得全局状态方程。我们给出了一个简单的例子，将其与忆阻器的不同描述联系起来。否则，我们在此并未追求约简过程，这是一个典型的、相当复杂的微分代数系统问题。此外，还有停滞点的危险，即电路变量的特殊值，即使对于其他所有值它们都能确定解，也无法确定解。我们也给出了一个具有这种奇异行为的忆阻器电路的简单示例。未检测到的停滞点可能导致数值模拟的错误结论。停滞点可以通过用合适的寄生电容补全电路模型来消除。知道它们的存在不仅能带来更好的电路模型，还能指示奇异行为，例如解中的跳变 [5]。

## 参考文献

- [1] Chua, L. O. (1971). Memristor — the missing circuit element. *IEEE Transactions on Circuit Theory, CT-18*(5), 507–519.
- [2] Chua, L. O., & Alexander, G. R. (1971). The effects of nonlinear reactances on nonlinear networks. *IEEE Trans. on Circuit Theory*, 520.
- [3] Fosséprez, M., & Hasler, M. (1990). Resistive circuit topologies that admit several solutions. *Int. J. Circuit Theory and Applications*, 18, 625–638.
- [4] Hasler, M. (1986). Non-linear non-reciprocal resistive circuits with a structurally unique solution. *Int. J. Circuit Theory and Applications*, 14, 237–262.
- [5] Hasler, M., & Neirynck, J. (1986). *Nonlinear Circuits*. Boston: Artech House.
- [6] Hasler, M., Marthy, C., Oberlin, A., & de Werra, D. (1994). A discrete model for studying existence and uniqueness of solutions in nonlinear resistive circuits. *Discrete Applied Mathematics*, 169–184.
- [7] Nielson, R. O., & Willson, A. N. (1984). A fundamental result concerning the topology of transistor circuits with multiple equilibria. *Proc. IEEE*, 68, 196–208.
- [8] Nishi, T., & Chua, L. O. (1984). Non-linear op-amp circuits: existence and uniqueness of the solution by inspection. *Int. J. Circuit Theory and Applications*, 12, 145–173.
- [9] Nishi, T., & Chua, L. O. (1984). Topological criteria for nonlinear resistive circuits containing controlled sources to have a unique solution. *IEEE Trans. Circuits and Systems, CAS-31*, 722–741.
- [10] Willson (ed.), A. N. (1974). *Nonlinear Networks*. New York: IEEE Press.

## 第 43 章
## 忆阻网络的解析分析

TORSTEN SCHMIDT, WILLI NEUDECK, UTE FELDMANN 和 RONALD TETZLAFF

*电气与计算机工程系,*  
*德累斯顿工业大学，德累斯顿，德国*

在过去几年中，许多忆阻器的技术实现在概念上和实践上都已实现。忆阻器背后的理论也得到了扩展，但主要针对忆阻器，而较少针对包含忆阻器的电路，后者由于忆阻器的非线性和动态性往往难以分析。单忆阻器网络的理论正是本文的目标。基于非线性网络的多线性理论和 Volterra 级数表示，获得了单忆阻器电路的一般描述。

- 1. 引言 .................................................... 529
- 2. 单忆阻器的行为 .............................. 530
- 3. 多线性方法 ....................................... 531
  - 3.1. 多线性 ................................................ 531
  - 3.2. 扩展到忆阻器 ................................... 531
  - 3.3. CM 电路 .................................................. 533
- 4. 通过 Volterra 级数方法对单忆阻器电路的一般描述 ........ 535
  - 4.1. Volterra 级数方法 ............................... 535
  - 4.2. 单忆阻器电路理论 ....................... 536
  - 4.3. 示例 ................................................... 537
- 5. 结论 ...................................................... 538
- 参考文献 .......................................................... 539

## 1. 引言

忆阻器这一具有记忆的特殊电阻的理论概念首次由 Leon O. Chua 于 1971 年发表 [4]。但对忆阻器的科学兴趣一直有限。这在 2008 年的一封致《自然》的信中突然改变。Strukov *et al.* [13] 观察到某些具有薄半导体层的纳米器件可以描述为忆阻器。此后，忆阻器在国际电气工程师、物理学家和生物学家的研究社区中获得了广泛关注。最近的研究主要集中于超高密度 VLSI 电阻式随机存取存储器（ReRAM）的实现。关于忆阻器的当前主要研究领域如图 1 所示，但可以假设未来将开辟出更多有趣的领域。

在过去几年中，不同忆阻器类型的许多技术实现已

