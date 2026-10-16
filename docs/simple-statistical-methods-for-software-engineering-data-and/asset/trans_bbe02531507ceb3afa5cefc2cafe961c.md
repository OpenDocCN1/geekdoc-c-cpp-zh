

并且被视为业务需求。如果质量提高，维护成本将会下降，客户将受益；但预防性维护必须付费。

## 生产率

生产率可以用不同的方式表达。我们建议使用人月人均 EFP 指标。该指标最终控制维护成本；有助于成本控制。

对于衡量缺陷修复生产率，每人月修复数量可以作为一个基本指标。

衡量生产率很直接，但从贡献因素估算生产率则不然。如果指标包含估算（从更广泛的意义上说是合理的预期），那么使用 COCOMO 等模型也可能在我们的范围内。

## 修复时间 (TTR)

这是由缺陷跟踪工具自动收集的指标。如果想改进缺陷修复流程，对其进行优化并实现卓越，可以收集诸如（1）复现时间、（2）分析和设计时间以及（3）实现和测试时间等子流程指标。这些子流程指标可以通过快速调查获得。缺陷跟踪工具可能无法收集子流程指标。此类调查不定期进行，以获取改进流程的信息。完全有可能在更细粒度的层面上收集指标，如果成本由预期收益证明的话，可以分别衡量分析时间和设计时间。可以更进一步，应用精益技术，如价值流图分析、等待时间分析和空闲时间分析。该指标将有助于使运营更高效。

最重要的是，在组织达到高度成熟并且人们自愿提供“个人”数据之前，通常不会选择子流程指标进行常规数据收集。然而，无论粒度如何，缺陷修复时间都是软件工程中最有效、最美妙的指标之一。

### BOX 7.3 THE QUEUE

缺陷形成一个队列，客户等待修复。客户满意度随着响应时间和质量的提高而增加；两者都依赖于人力资源。当资源利用率为 100% 时，客户满意度低于最佳水平。当资源利用率为 90% 时，客户满意度会提高。寓意：必须保持一定的人力储备以提高客户满意度，二者之间存在权衡。维护组织保留缓冲资源，并在资源利用率低于 100% 的情况下运营，因为失去客户满意度的成本更高。

## Backlog Index

该指数衡量积压队列中缺陷的百分比，并代表维护项目中的运营挑战。

## 缺陷分类

分类是分类数据。为了更好地理解缺陷，它们在缺陷跟踪数据库中被分类。典型字段有来源、原因、触发因素、类型和解决方案。可以添加更多；可考虑使用 ODC。定期分析缺陷在各种分类中的分布是对问题的良好揭示。

## 修复质量

缺陷修复可能存在问题。缺陷可能重新打开并导致返工和延迟。可以衡量首次修复正确的缺陷修复百分比。返工可以衡量以控制成本。

## 重构指标

为了通过重构提高软件质量并降低维护成本，我们衡量耦合度和圈复杂度。耦合度衡量模块之间的数据流。圈复杂度衡量模块结构中的复杂性。

## 可靠性

在维护下的产品可靠性可以从“故障强度”计算得出，即每月报告的缺陷数量。从该指标，我们可以判断产品是正在恢复还是崩溃。累积发现缺陷的时间序列图称为 *可靠性增长曲线*，可作为可靠性的视觉表示。平均故障间隔时间也可以计算。

## 基于指标的仪表板

我们将考虑构建用于管理软件维护的图形仪表板的七个主要指标。其他指标数据可以以表格记录的形式呈现。用于图形展示的指标选择完全取决于维护团队。Stark 使用以下指标 [6]：

- 1. Backlog
- 2. Cycle time
- 3. Reliability
- 4. Cost per delivery

- 3. Self-regulation—a system evolution process is self-regulating with distribution of product and process measures close to normal.
- 4. Conservation of organizational stability (invariant work rate)—the average effective global activity rate in a system is invariant over product lifetime.
- 5. Conservation of familiarity—a system evolves all associated with it; developers, sales personnel, and users, for example, must maintain mastery of its content and behavior to achieve satisfactory evolution. Excessive growth diminishes that mastery. Hence, the average incremental growth remains invariant as the system evolves.
- 6. Continuing growth—the functional content of a system must be continually increased to maintain user satisfaction over its lifetime.
- 7. Declining quality—the quality of a system will appear to be declining unless it is rigorously maintained and adapted to operational environment changes.
- 8. Feedback system evolution processes constitute multilevel, multiloop, and multiagent feedback systems and must be treated as such to achieve significant improvement over any reasonable base.

## 复习问题

- 1. What is the most important metric in adaptive (enhancement) maintenance?
- 2. What is the most important metric in corrective maintenance?
- 3. What is the most important metric in perfective maintenance?
- 4. Which among the previously mentioned three metrics is the toughest to collect?
- 5. If you were to design a dashboard for a support project and if you were asked to limit the number of metrics to just seven, which seven would you choose?

## 练习

- 1. Develop a metrics list for a support project if the adaptive–corrective–perfective maintenance task ratio is 3:10:2.
- 2. Develop a metrics list for an exclusive support contract for the perfective maintenance of software with an express goal of improving maintainability.

## 参考文献

- 1. NESMA, Function Point Analysis for Software Maintenance Guidelines, Version 2.2.1, Professional Guide of the Netherlands Software Metrics Users Association, Netherland 2009.
- 2. NC State University Communication. Available at http://agile.csc.ncsu.edu/SEMaterails/MaintenanceRefactoring.pdf.
- 3. C. V. S. R. Syavasya, An approach to find out at which maintainability metric, software maintenance cost is less, *International Journal of Computer Science and Information Technology*, 3(4), 4599–4602, 2012, ISSN:0975–9646.
- 4. *Journal of Software Maintenance and Evolution: Research and Practice*, John Wiley & Sons, Ltd.
- 5. V. Zeithaml, A. Parasuraman and L. Berry, *Delivering Quality Service*, Simon and Schuster, 1990.
- 6. G. E. Stark, *Measurements to Manage Software Maintenance*, Technical Note, The MITRE Corporation, Colorado Springs, CO, July 1979.

## 建议阅读

Aczel, A. D. and J. Sounderpandian, *Complete Business Statistics*, McGraw-Hill, London, 2008.

Available at http://www.refactoring.com/.

Available at http://wiki.java.net/bin/view/People/SmellsToRefactorings.

## 第 8 章

## 软件测试指标

第 1 章和第 5 章中讨论的指标的广泛益处同样适用于软件测试。虽然测试是完整生命周期的一个部分，但它已成为一种独特类型的项目，具有其自身独特的目标。测试是为了发现缺陷并提高产品质量而进行的。任何项目的三个目标，即更快、更好、更便宜，也适用于测试。指标将有助于推动测试达到更高水平。

## 项目指标

测试项目指标的定义与任何项目中的指标定义完全相同，具有相同的含义和目的。项目指标有助于节约项目资源并使其得到最佳利用。项目指标跟踪需求变更，并在需求变更威胁项目时帮助采取纠正措施。项目指标也有助于满足客户。

## 进度偏差

在测试项目中，按时交付很重要。随着测试里程碑的完成，衡量时间和进度偏差将为团队提供反馈，以努力满足交付计划。

## 工作量偏差

在预算工作量内完成测试是下一个关注点。工作量偏差指标将有助于控制测试成本。

