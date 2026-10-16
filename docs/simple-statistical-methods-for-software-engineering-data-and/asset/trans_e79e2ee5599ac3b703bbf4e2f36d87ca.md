

缺陷被标记为返工或质量差的成本是质量成本框架的显而易见的影响。然而，这些指标是作为缺陷年龄研究的一部分报告的，而不是 COQ 研究。缺陷的生命周期比正式框架更贴近人们。测试人员认为 COQ 是高级管理人员的一个更大指标。

在其他地方，质量成本也在测试过程中计算。COQ 使用三个组成部分：预防、鉴定和失败。失败意味着对测试用例的返工和重新测试，鉴定是指评审，而预防包括培训和缺陷预防工作。

创建缺陷年龄指标的目标是通过发现缺陷年龄与缺陷成本之间的关系来建立成本模型。

> > 最重要的质量指标是失败成本。
> >
> > — **Crosby**

设计人员不希望将缺陷成本视为失败成本，但测试人员这样认为。尽管存在争议，缺陷年龄指标已成为潜在指标。存在一种工程概念，即缺陷年龄反映产品可靠性。缺陷年龄越小，可靠性越高。项目团队努力减少缺陷年龄。

创建缺陷年龄指标的另一个目的是检查缺陷修复成本的 1:10:100 规则。该规则指出，如果早期修复缺陷的成本为一美元，则后期修复的成本将呈指数级增长。根深蒂固的缺陷难以发现且修复成本高昂。数据显示，在该项目中，该规则为 1:2:4.2。当缺陷年龄增加时，成本没有急剧上升。

## Review Questions

- 1. How many metrics would you use in a test dashboard in a testing project?
- 2. What are the metrics that can be used in unit testing?
- 3. What are the metrics that can be used in smoke tests?
- 4. Suggest simple ways of assessing reliability of software before release.
- 5. What metric data will be used while making a decision about stopping testing?
- 6. Compare test effectiveness with test efficiency.
- 7. Mention the names of two commonly used S curves in testing.
- 8. Relate defect age to the cost of testing. In your opinion, what would be the expression for such a relationship?

## Exercises

- 1. Develop a minimum set of metrics you would maintain for a testing agency who provides testing services to software developing companies.
- 2. Develop a risk metrics system for risk-based testing in a software development project.
- 3. Suggest a matrix format for checking requirement traceability with test cases.
- 4. Develop a metric system to be used for managing test automation.
- 5. Develop a template for a one monthly test report based on metric data. Mention the names of metrics and the charts you would use.

## References

- 1. V. Nguyen, V. Pham and V. Lam, *Test Case Point Analysis: An Approach to Estimating Software Testing Size*. http://csse.usc.edu/csse/TECHRPTS/2007/usc-csse-2007-737/usc-csse-2007-737.pdf.
- 2. N. Patel, M. Govindarajan, S. Maharana and S. Ramdas, *Test Case Point Analysis*, White Paper Version 1.0, Cognizant Technology Solutions, April 11, 2001.
- 3. K. A. Jha and J. D. Cem Kaner, *Bugs in the Brave New Unwired World: A Failure Mode Catalog of Risks and Bugs in Mobile Applications* (personal communication). Copyright © 2003.
- 4. C. Kaner, Risk-based testing: Some basic concepts, *QA Managers Workshop*, April 2008.

## Suggested Readings

Kaur, A., B. Suri and A. Sharma, Software testing product metrics—A survey, *Proceedings of National Conference on Challenges & Opportunities in Information Technology (COIT-2007)*, RIMT-IET, Mandi Gobindgarh, March 23, 2007.

Kelly, D. P. and R. S. Oshana, Improving software quality using statistical testing techniques, *Information and Software Technology*, 42, 801–807, 2000.

Nirpal, P. B. and K. V. Kale, A brief overview of software testing metrics, *International Journal on Computer Science and Engineering*, 3(1), 204–211, 2011.

Poore, J. H. and C. J. Trammell, *Application of Statistical Science to Testing and Evaluating Software Intensive Systems*. Available at http://sqrl.eecs.utk.edu/papers/199905_cjt_hmc.pdf.

Prabhakar, J. Test execution through metrics, *STEP-AUTO Conference*, Bangalore, Test Management, September 19, 2007.

## Chapter 9

## Agile Metrics

敏捷指标的目的和特点与《敏捷宣言》相呼应。

> Individuals and interactions over processes and tools.
> 
> Agile Manifesto

适当的敏捷指标设计和实施可以增加价值并实现敏捷的软件开发方式。

### BOX 9.1 ANALOGY: DECIBELS

人耳将声波转化为音频信号。当声波强度增加十倍时，人耳的反应增加 1 点。当声强增加一百倍时，人耳记录的强度为 2 点。反应是对数式的。声级以分贝为单位测量，本质上是声波强度的对数。

| Sound Intensity | Relative Response of Ear |
|---|---|
| 10 | 1 |
| 100 | 2 |
| 1000 | 3 |
| 10,000 | 4 |
| 100,000 | 5 |

耳朵能够轻松处理和响应极其宽广的声强范围。

地震强度也以对数刻度即里氏震级表示。当地震力在里氏震级上增加一点时，实际释放的能量增加 10 倍。

故事点与这些对数刻度相似。故事点可以容纳广泛的实际软件规模，并以个位数呈现。

## Classic Metrics: Unpopular Science

经典软件指标已成为不受欢迎的科学，至少在某些方面是这样，因为软件工程的演变。一些严格的指标使真相变得难以获取，而设计不良的指标则成了面具；它们不是揭示真相，而是隐藏真相。模糊的指标使情况更糟，因为它们存在多种解释。大多数经典指标都不是直接的。

例如，工作量差异很少基于实际花费的工作量，而是基于允许的数字。工程师一天可能花费 14 小时，但被要求只输入 8 小时，因为这是可计费的金额，客户不为加班付费。在这种情况下，指标助长了虚伪，正是它试图打击的邪恶。用户需要“理解”隐藏的背景并猜测隐藏的含义。

在受服务水平协议管辖的业务中，进度差异毫无意义，但仍在指标计划中提及。数字被输入以填补报告；项目中的任何人都不会认真对待此类指标报告。

生产率指标和企业对生产率的目标是永恒冲突的来源。所有任务类别都设定了共同目标，无视底层工程原则和流程能力的差异。在这种情况下，没有人相信生产率数据。

这已将许多组织推入这种自毁局面。因为审计人员坚持要求数据良好作为流程控制良好的证据，人们会删除“异常值”——以及真相。指标数据中的错误被消除，破坏了学习的可能性。

*压力要求指标以完全非科学的方式呈现生活的完美图景。*

*指标在被滥用时，建立了完美的幻觉和科学迷信。*

也有例外。确实存在指标使用者，但他们太少，无法扭转对指标的舆论。

![](img/2f042205c6c0e14747f198ed8f9c9f40_151_0.png)

![](img/2f042205c6c0e14747f198ed8f9c9f40_151_1.png)

> I believe in metrics, not politics.

**Narayana Murthy**
*Chairman, Infosys*

![](img/2f042205c6c0e14747f198ed8f9c9f40_151_2.png)

### BOX 9.2 MEDICAL ANALOGY: MRI SCAN AND PULSE READING

医生要求对头部进行 MRI 扫描以治疗头痛。他想排除可能的病因：脑部血栓。MRI 扫描是一种昂贵且复杂的程序。医生正在进行因果分析。扫描结果正常，医生继续追查头痛的其他原因，费用由患者通过试错承担。最后，患者的头痛仍未治愈。

患者决定接受自然疗法治疗。熟练的医生读取他的脉搏，了解问题，并建议一个月进行理疗锻炼和瑜伽。患者痊愈了。

敏捷指标类似于读取脉搏。数据便宜、简单、快速；解决方案是自我修复。脉搏读数对训练有素的医生来说比 MRI 扫描揭示更多。

## Two Sides of Classic Metrics

尽管存在诸多问题，经典指标仍有所裨益。人们学会了使用数字，至少在他们想使用时，首先通过模仿最佳实践，后来通过获得的能力。经典指标一直具有巨大的潜力（尽管未被充分利用）。那些遵循个人软件流程（PSP）指标的组织确实受益：他们减少了缺陷。Humphrey 关于数据驱动纪律的愿景

