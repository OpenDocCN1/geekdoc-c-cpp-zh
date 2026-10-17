
L. Lattner and V. Wagner. LLVM: A compilation framework for long-term program analysis and transformation. In Proc. of the 20th International Symposium on Code Generation and Optimization, 75–86.

T. Sherwood, E. Preelman, G. Halvery, and B. Calder. Automatically characterizing large program behavior. In International Conference on Architectural Support for Programming Languages and Operating Systems, pp. 45–56, 2002.

M. L. Li, P. Ramachandran, K. Saabo, S. V. Ad, S. V. Ad, and Y. Zhou. Understanding the propagation of hard errors and implications for resilient system design. In International Conference on Architectural Support for Programming Languages and Operating Systems, 265–276, 2008.

P. Shivakumar, M. Kim, S. Keckler, B. Burger, and I. Vysys. Impact of technology trends on the soft error rate of logic. In Proc. of the 2002 International Conference on Data Systems and Networks, 385–398, 2002.

X. Li and D. Young. Application-level correctness and its impact on fault tolerance. In Proc. of the 13th International Symposium on High-Performance Computing Interfaces, 73–80, 2006.

T. May and M. Yba. Alpha-particle-induced soft errors in DRAM memories. IEEE Transactions on Electronics, 26(2):216–29, 1979.

J. Molsen, J. Kim, J. He, and F. Fallasch. Result sharing in cooperative multicore processors. In Proc. of the 37th International Symposium on Computer Architecture, 256–268, 2010.

J. C. Botmel, T. B. Gold, B. Falasi, and J. C. He. Cooperative multiprocessing. In Proc. of the 39th International Symposium on Computer Architecture, 223–235, 2006.

S. McCartin and D. M. Erot. Quantitative information flow as network capacity. In Proc. the SIGPLAN '08 Conference on Programming Language Design and Implementation, 195–203, 2008.

L. Lowe and T. Cheng. `SIB/S90 Enterprise Server G5` (dual in memory modules) provide single-bit correction and double-error-detection (`SEC-DED`) for each `DRAM` chip. To protect against entire `DRAM` chips requires the use of `chipkill`, which "spreads" a `DRAM` access across multiple uses and allows `ECC` to allow strong error resilience. The downside of `chipkill` is that it increases memory latency, requires more complex configurations, or increases the level of reliability, again, which increases cost. It is noted, that in systems that are highly sensitive to environmental factors, large-scale failures are more likely. Large installations have reported that system errors due to `DRAM` errors are 600 times more likely without `chipkill` [20]. Providing `chipkill` protection without reducing `DRAM` capacity requires the use of `ECC DRAM` configuration (which is defined in Section 2.2). These rows may consume 30% more memory capacity to achieve the same protection level.

通过在 `$4`、`$x8` 和 `$x16` 芯片之间更改配置。我们详细评估了每种配置，并讨论了其对性能的影响以及功耗和能量延迟积（`EDP`）的改进。性能由于有效数据丢失而下降，但在冗余信息方面有所提高。我们评估的应用来自 `SPEC CPU suite [2006]` 和 `PARSEC` 套件具有高内存访问需求，以及特定的微基准。

如果 `ECC DIMM` 允许，我们开发了一系列基于双层保护机制 [`33`, `48`] 的技术。灵活 `ECC` 的主要创新是根据用户或系统需求动态激活不同的错误保护级别。在双保护模式下，`ECC DIMM` 的效率在于仅对总冗余子集存储错误信息，从而降低了能耗。冗余仅在发生错误的极少数情况下需要，而且由于纠错信息与数据共享 `DRAM` 命名空间，我们可以通过移除额外的芯片来避免某些性能下降。灵活 `ECC DIMM` 的灵活性允许我们仅使用 `x8` 芯片，这在单层方案中是不可能的。我们证明了芯片的 `EDP` 可以提高 12%，并下降 1% 到 2%。我们还描述了一种使用映射在不同 `DIMM` 之间管理双层保护的机制。

此外，低成本方案为不使用 `ECC DIMM` 的用户提供了纠错能力。我们提出了一种根据需要存储冗余信息并通过架构接口将其与数据关联的方法。内存控制器对每次 `DRAM` 读取或写、或对一组数据和 `ECC` 执行访问。我们证明，这种方法平均使 `DRAM` 性能降低 6% 到 9%，最多不超过 10% – 25%，由于使用的 `DRAM` 芯片更少而降低了功耗。总体而言，通过使用 `x8` 和 `x16` `DIMM`，系统可以提升高达 12%。

我们的主要贡献如下：

- 我们提出了一种用于 `ECC` 保护虚拟化的通用架构，以及从数据映射到冗余信息的映射方法。
- 我们为 `DRAM` 开发了双层保护，并展示了如何使用各种配置提高系统可靠性并降低系统功耗。
- 我们提供了一种灵活的纠错机制，能够根据应用、用户和系统需求调整错误保护级别。
- 我们描述了如何在非 `ECC DIMM` 系统中使用保护功能，而无需更改数据，并使用不同的保护级别和配置评估了对性能和功耗的影响。

本文的其余部分结构如下：第 2 节介绍了内存系统和 `DRAM` 纠错的背景；第 3 节详细介绍了架构、操作系统要求以及保护方案；第 4 节介绍了我们的评估；第 5 节讨论了相关工作；第 6 节总结全文。

## 2. 背景

在本节中，我们简要描述现代内存系统和错误保护技术，包括 `chipkill` 纠错。我们讨论了基于 `DDR` 的现代系统，因为包括高端服务器设备在内的绝大多数计算平台。本文重点关注 `DDR DIMM`。

### 2.1 内存系统

现代计算机向程序员隐藏了设计内存系统所需的复杂性。虚拟内存抽象了内存系统的每个细节（包括位置和虚拟映射），并提供了一个平的地址空间。然而，物理内存是由芯片组成的，每个芯片有多个模块。在本节的其余部分中，我们简要回顾了从 `DRAM` 芯片到内存模块的内存系统结构，因为它们与 2.2 节相关。关于内存系统的更多描述可参见参考文献。

单个 `DIMM` 具有地址/输入引脚、位数据引脚以及数据大小。单个 `DRAM` 芯片具有原生数据宽度（分别为 `x2`、`x4`、`x8` 或 `x16`），多个芯片协同工作形成更宽的数据范围。例如，64 位数据宽度可以通过八个 `x8` 或四个 `x16` `DRAM` 组成。内存控制器是可以独立控制每个芯片的逻辑设备，因为所有 `DIMM` 都是按秩排列的。

### 2.2 内存纠错

内存系统故障的主要来源是错误和设备故障。传统的内存错误保护在整个内存上统一使用 `ECC`。我们讨论了常用的单位错误纠正和双位错误检测（`SEC DED`）方案，该方案使用 `ECC` 实现更强的 `chipkill` 纠错，并讨论了它与现代方法的关系。

`SEC DED` 代码 [`17`] 通常每 64 位数据使用 8 位 `ECC`。具有 72 位数据宽的 `ECC-DIMM` 与 2.2 节中解释的 `ECC DIMM` 不同。`ECC DIMM`（同样在 2.2 节中解释）允许灵活的保护。灵活 `ECC DIMM` 的灵活性允许我们仅使用 `x8` 芯片，这在单层方案中是不可能的。我们证明了芯片的 `EDP` 可以提高 12%，并下降 1% 到 2%。我们还描述了一种使用映射在不同 `DIMM` 之间管理双层保护的机制。

## 虚拟 ECC 架构

灵活 `ECC` 的主要创新是根据用户或系统需求动态激活不同的错误保护级别。在双保护模式下，`ECC DIMM` 的效率在于仅对总冗余子集存储错误信息，从而降低了能耗。冗余仅在发生错误的极少数情况下需要，而且由于纠错信息与数据共享 `DRAM` 命名空间，我们可以通过移除额外的芯片来避免某些性能下降。灵活 `ECC DIMM` 的灵活性允许我们仅使用 `x8` 芯片，这在单层方案中是不可能的。我们证明了芯片的 `EDP` 可以提高 12%，并下降 1% 到 2%。我们还描述了一种使用映射在不同 `DIMM` 之间管理双层保护的机制。

此外，低成本方案为不使用 `ECC DIMM` 的用户提供了纠错能力。我们提出了一种根据需要存储冗余信息并通过架构接口将其与数据关联的方法。内存控制器对每次 `DRAM` 读取或写、或对一组数据和 `ECC` 执行访问。我们证明，这种方法平均使 `DRAM` 性能降低 6% 到 9%，最多不超过 10% – 25%，由于使用的 `DRAM` 芯片更少而降低了功耗。总体而言，通过使用 `x8` 和 `x16` `DIMM`，系统可以提升高达 12%。

![](img/03d0eb09047dbcab29ca9be26a1a08a3_413_0.png)

## 3.1 缓存-DRAM 接口

缓存从 `DRAM` 系统获取请求，并有助于提高虚拟 `ECC`（`Virtual ECC`）的性能。由于物理数据包含 `ECC` 信息，我们可以减少 `ECC` 带宽占用；然而，只有当内存控制器需要将数据写入 `DRAM` 时才会访问 `ECC`。例如，当连接到末级缓存（`LLC`）时，冗余信息存储在 `LLC` 中。`LLC` 维护缓存一致性，并由内存控制器保持数据更新。虚拟 `ECC` 不需要对现有的缓存架构进行重大更改，额外的硬件仅提供维护和写回虚拟缓存行的能力。

![](img/03d0eb09047dbcab29ca9be26a1a08a3_413_1.png)

### 3.1.1 两层 ECC

图 3 显示了我们在内存系统配置之上的两层虚拟 `ECC`，该配置中，末级缓存连接到两个带有专用 `ECC` 的 `DRAM` 秩（`rank`）。我们使用 `ECC` 来检测数据错误，但在没有 `T2EC` 额外信息的情况下无法纠正它们。`T2EC` 映射到数据芯片上，使得数据及其相关的 `T2EC` 位于不同的 `DRAM` 秩中。

下节描述了场景 3 中的操作：当 `LLC` 发生未命中时，缓存未命中后，数据突发传输及其相关的 `T2EC` 从内存中获取，并对任何检测到的无法立即纠正的错误进行错误检测。然而，与传统的层级结构相比，驱逐脏行并写回 `DRAM`（`Q`）需要额外的操作。

内存控制器更新与驱逐行相关的 `T2EC` 信息，这从数据地址开始到 `ECC` 地址（`EA`）的位置（③）。如果翻译后的 `EA` 已经在 `LLC` 中，则直接将其置于。通过这种方式，我们不需要从内存获取 `ECC` 信息，因为只有在检测到错误时才会读取 `T2EC`。在写操作时，先前的信息就失效了。我们计算 `T2EC` 并将其写入 `LLC`。`LLC` 行包含虚拟 `T2EC` 数据。使用我们的编码方案，`T2EC` 长度为 16–28 位，需要的额外位非常少。在发生 `ECC` 错误时，虚拟 `ECC` 使用 `LLC` 行来存储掩码值。然后我们在 `LLC` 中的 `T2EC` 行中发现错误，因为没有第三层冗余，且来自其他 `DRAM` 秩保护了 `T2EC` 信息。如 (V) 所示，行的操作不能覆盖 `DRAM` 中的 `T2EC` 数据。为了实现这一点，我们使用位向量加密每个 `MSHR`，内存控制器利用它来与内存控制器进行通信。

### 3.1.2 与非 ECC DIMM 的虚拟 ECC 接口

如果物理内存不提供 `ECC`，我们可以使用虚拟 `ECC` 来保护内存错误。在非 `ECC DIMM` 配置中，我们无法存储对齐的 `T2EC`，而是将所有冗余信息放在虚拟内存中（为了保持符号一致性，我们仍称为 `T2EC`）。该架构如图 4 所示。当在主内存（①）时，`ECC` 地址翻译单元位于 `EA`（②）和（⑤）处。`T2EC` 的 `LLC` 未命中将从主内存（2）获取 `T2EC`，因为在没有 `ECC DIMM` 的，信息用于检测错误而非纠正。在两层场景中，我们管理整个缓存的 `T2EC` 数据行以允许 `DRAM` 访问，并提高空间局部性以减少内存访问。当数据在插入 `ECC` 信息后返回缓存时，如果在写回（5）检测到错误，则 `PA` 传输到 `EA`（6）并在缓存中插入 `T2EC`。

关键点是使用虚拟 `ECC` 来减少开销并提高空间局部性。此类类型的细节见下文。配置总结在表 1 中。我们将在下一节中描述针对 `x4`、`x8` 和 `x16` 的情况。

## 表 1：基准系统 chillchip 的 DIMM 配置、[3] 中引入的用于改进功耗的非标准 DIMM MC-DIMMs 以及虚拟 ECC

| | 每个秩的数据 DIMR 数量 | 每个秩的 ECC DIMR 数量 | 秩组织 | 读取时的 T2EC 访问 | 写入时的访问 | 每条缓存行的 T2EC |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 基准 Chillchip | | | | | | |
| 基准 x4 | x32 | 4 | 2 个 ECC DIMMs | N | N | N/A |
| MC-DIMM (3 个 28 位通道和 4 个秩) | x32 | 12 | 2 个 MC-DIMMs | N | N | N/A |
| MC-DIMM x8 | x16 | 12 | 2 个 MC-DIMMs | N | N | N/A |
| MC-DIMM x16 | x16 | 12 | 2 个 MC-DIMMs | N | N | N/A |

## 虚拟 ECC

| | 每个秩的数据 DIMR 数量 | 每个秩的 ECC DIMR 数量 | 秩组织 | 读取时的 T2EC 访问 | 写入时的访问 | 每条缓存行的 T2EC |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| ECC x4 | x32 | | 1 个 ECC DIMM 和一个非 ECC DIMM | N | Y | 2B |
| ECC x8 | x16 | 12 | 2 个 ECC DIMMs | N | Y | 4B |
| 非 ECC x8 | x16 | 12 | 2 个非 ECC DIMMs | N | Y | 8B |
| 非 ECC x16 | x16 | 12 | 2 个非 ECC DIMMs | N | Y | 16B |

## 3.2 虚拟 ECC 配置

现在我们讨论假设基准系统的虚拟 `ECC` 配置。基准系统使用 `DDR2`，它具有代表性。我们也考虑针对 `DDR3` 的这些方案。

### 3.2.1 带有 ECC DIMM 的虚拟 ECC

传统方法使用 2.2 节解释的缓存秩错误码，结合分层保护和 `T2EC` 存储架构以确保效率。在两层保护中，第一层保护是基于 `TERC` 的缓存错误码，而 `T2EC` 是可以检测最多 2 个故障的代码。如果 `T2EC` 检测到单个错误，则使用每个秩三个芯片的 `x10` 位进行纠正。如果 `T2EC` 检测到两个错误，则可以使用每个秩四个芯片的 `x16` 位进行纠正（1）。

传统的缓存方案可以通过通过为 `T2EC` 添加第二个芯片符号来进一步增强：如果 `T2EC` 检测到两个错误（两个符号错误），缓存代码可以从两个芯片恢复数据。该方案的细节如表 2 所示。虽然类似的基准缓存不太可能，但以下

### 3.2.2 带有非 ECC DIMM 的虚拟 ECC

虚拟 `ECC` 的另一个优势是为使用非 `ECC DIMM` 的系统添加 `ECC` 保护。我们使用了基于 2 芯片符号里德-所伦（`RS`）码的方案来检测和纠正我们的错误，这种代码只要错误限制在单个芯片内，就可以允许任意数量。此类类型的细节如下

- 虚拟 `ECC` 的非 `ECC` 配置无法检测芯片故障。
- 推测性数据转发是可行的，但在我们的实验中并未显著提高性能。
