

在你达到信心阈值后，继续增加测试所产生的边际额外信心不值得付出努力。最好停止并专注于现有测试的质量和可维护性。

## 雪糕

图 5-11 显示了当测试金字塔完全倒置时会发生什么：顶部的不确定性云层已膨胀到庞大的程度，而几乎看不到单元测试。

![](img/f852e0a12c174e64d91a8e1a05146eab_210_0.png)

图 5-11 当测试的相对数量被倒置时，金字塔就变成了雪糕。

当大多数测试工作都是手动的时，这表明你有一个无法测试的代码库。应立即开始重构代码，使其本质上可测试。为了纳入此类工作，请结合使用黄金主技术（参见第 6 章“重构”）和看板服务等级（参见第 2 章“看板简介”）。

手动测试不如自动化测试可靠，因为执行测试脚本的人会出错。这种重复、单调的工作很快就会变得令人沮丧。努力自动化你能自动化的部分，以便在必要时可以廉价地重复手动测试。

## 测试象限

测试金字塔中涵盖的测试存在于不同的粒度，从粗粒度的用户界面测试到细粒度的单元测试。测试象限提供了测试的补充视角：它们适用于不同的利益相关者，并且出于不同的原因。

对于已经 somewhat 熟悉测试象限的读者来说——毕竟这是一个相当古老的概念——图 5-12 中呈现的版本看起来可能有所不同。软件顾问 Gojko Adzic 令人钦佩地刷新了测试象限，使其更符合当前的技术水平。该图经 Gojko Adzic 许可转载。

![](img/f852e0a12c174e64d91a8e1a05146eab_211_0.png)

图 5-12 测试象限有助于对不同测试类别的受众和目的进行分类。

与所有基于象限的模型一样，有两个轴需要考虑。在垂直轴上，讨论的是测试的预期受众：技术人员或业务。在水平轴上，讨论的是测试目的：期望验证（定量）与分析（定性）结果。

### 业务/定量

企业通常与其客户和客户签订服务水平协议（SLAs）。这些是企业必须遵守的正式、可量化的标准，否则企业需对客户提供某种形式的赔偿。可用性是常见的 SLA 指标，企业承诺以 99.9% 的正常运行时间保持服务可用。由于这可以衡量并且对业务有直接影响，因此针对此类标准的测试位于此象限。

### 业务/定性

主观关注点如可用性就存在于此象限。这里更强调所涉及的技术，而更强调软件对业务的影响。A/B 和多变量测试，允许通过实验评估组件的多个版本，是整个软件领域中出现的趋势。与其通过焦点小组测试用户更喜欢矢车菊蓝还是海洋蓝，不如对两种蓝色进行 A/B 测试并衡量转化提升的统计显著性。

### 技术/定量

单元测试位于此象限，集成测试也是如此。这些测试支持开发团队量化系统与其需求的符合程度。单元测试通过率、代码覆盖率和圈复杂度等统计数据表明系统的整体健康状况。

### 技术/定性

在这里，你关注的是可能没有可量化需求的架构能力。负载测试关注系统在各种负载下表现的资源使用情况。对于服务而言，这可能包括吞吐量统计和响应时间曲线，随着更多用户同时访问系统。评估系统的安全性也是一种定性活动；这是通过渗透测试来评估的。系统的攻击向量难以量化，因此需要更分析性的[content]

在你达到信心阈值后，继续增加测试所产生的边际额外信心不值得付出努力。最好停止并专注于现有测试的质量和可维护性。

## 雪糕

图 5-11 显示了当测试金字塔完全倒置时会发生什么：顶部的不确定性云层已膨胀到庞大的程度，而几乎看不到单元测试。

![](img/f852e0a12c174e64d91a8e1a05146eab_210_0.png)

图 5-11 当测试的相对数量被倒置时，金字塔就变成了雪糕。

当大多数测试工作都是手动的时，这表明你有一个无法测试的代码库。应立即开始重构代码，使其本质上可测试。为了纳入此类工作，请结合使用黄金主技术（参见第 6 章“重构”）和看板服务等级（参见第 2 章“看板简介”）。

手动测试不如自动化测试可靠，因为执行测试脚本的人会出错。这种重复、单调的工作很快就会变得令人沮丧。努力自动化你能自动化的部分，以便在必要时可以廉价地重复手动测试。

## 测试象限

测试金字塔中涵盖的测试存在于不同的粒度，从粗粒度的用户界面测试到细粒度的单元测试。测试象限提供了测试的补充视角：它们适用于不同的利益相关者，并且出于不同的原因。

对于已经 somewhat 熟悉测试象限的读者来说——毕竟这是一个相当古老的概念——图 5-12 中呈现的版本看起来可能有所不同。软件顾问 Gojko Adzic 令人钦佩地刷新了测试象限，使其更符合当前的技术水平。该图经 Gojko Adzic 许可转载。

![](img/f852e0a12c174e64d91a8e1a05146eab_211_0.png)

图 5-12 测试象限有助于对不同测试类别的受众和目的进行分类。

与所有基于象限的模型一样，有两个轴需要考虑。在垂直轴上，讨论的是测试的预期受众：技术人员或业务。在水平轴上，讨论的是测试目的：期望验证（定量）与分析（定性）结果。

### 业务/定量

企业通常与其客户和客户签订服务水平协议（SLAs）。这些是企业必须遵守的正式、可量化的标准，否则企业需对客户提供某种形式的赔偿。可用性是常见的 SLA 指标，企业承诺以 99.9% 的正常运行时间保持服务可用。由于这可以衡量并且对业务有直接影响，因此针对此类标准的测试位于此象限。

### 业务/定性

主观关注点如可用性就存在于此象限。这里更强调所涉及的技术，而更强调软件对业务的影响。A/B 和多变量测试，允许通过实验评估组件的多个版本，是整个软件领域中出现的趋势。与其通过焦点小组测试用户更喜欢矢车菊蓝还是海洋蓝，不如对两种蓝色进行 A/B 测试并衡量转化提升的统计显著性。

### 技术/定量

单元测试位于此象限，集成测试也是如此。这些测试支持开发团队量化系统与其需求的符合程度。单元测试通过率、代码覆盖率和圈复杂度等统计数据表明系统的整体健康状况。

### 技术/定性

在这里，你关注的是可能没有可量化需求的架构能力。负载测试关注系统在各种负载下表现的资源使用情况。对于服务而言，这可能包括吞吐量统计和响应时间曲线，随着更多用户同时访问系统。评估系统的安全性也是一种定性活动；这是通过渗透测试来评估的。系统的攻击向量难以量化，因此需要更分析性的方法。

测试象限表明，不同类别的测试各有不同。虽然本书主要关注单元测试实现和设计的低级细节，但你代码的适应性也依赖于拥有合适数量和合适类型的测试。

## 测试用于预防和治疗

迄今为止讨论的所有测试都涉及预防性测试。也就是说，提前投入精力以确保新功能按预期工作，并且没有现有功能被回归。

这是标准做法。但它并非没有成本。每项编写的测试都需要时间和精力。信心是测试的货币。需要牢记的等式是：

effort < confidence

如果你的努力没有产生所需的测试信心，它们就成本过高，你应该将精力集中在其他地方。当然，所有项目都有一个目标信心，以校准其对失败的容忍度。嵌入在起搏器中的软件需要的信心远高于为商业软件即服务解决方案提供动力的软件。遵循努力与信心的相关性，确保起搏器正确工作的努力因此要高得多。

但是，如果你不是在编写这种任务关键型软件，你有哪些选择来减少努力并增加信心？

图 5-13 显示了软件通常如何从开发到实时环境。

![](img/f852e0a12c174e64d91a8e1a05146eab_212_0.png)

图 5-13 软件可以在到达实时环境之前部署到多个环境进行测试。

随着流程的每个阶段，你对软件功能正确性和鲁棒性的信心都在增加。通过在不同范围和不同环境中[content]

在你达到信心阈值后，继续增加测试所产生的边际额外信心不值得付出努力。最好停止并专注于现有测试的质量和可维护性。

## 雪糕

图 5-11 显示了当测试金字塔完全倒置时会发生什么：顶部的不确定性云层已膨胀到庞大的程度，而几乎看不到单元测试。

![](img/f852e0a12c174e64d91a8e1a05146eab_210_0.png)

图 5-11 当测试的相对数量被倒置时，金字塔就变成了雪糕。

当大多数测试工作都是手动的时，这表明你有一个无法测试的代码库。应立即开始重构代码，使其本质上可测试。为了纳入此类工作，请结合使用黄金主技术（参见第 6 章“重构”）和看板服务等级（参见第 2 章“看板简介”）。

手动测试不如自动化测试可靠，因为执行测试脚本的人会出错。这种重复、单调的工作很快就会变得令人沮丧。努力自动化你能自动化的部分，以便在必要时可以廉价地重复手动测试。

## 测试象限

测试金字塔中涵盖的测试存在于不同的粒度，从粗粒度的用户界面测试到细粒度的单元测试。测试象限提供了测试的补充视角：它们适用于不同的利益相关者，并且出于不同的原因。

对于已经 somewhat 熟悉测试象限的读者来说——毕竟这是一个相当古老的概念——图 5-12 中呈现的版本看起来可能有所不同。软件顾问 Gojko Adzic 令人钦佩地刷新了测试象限，使其更符合当前的技术水平。该图经 Gojko Adzic 许可转载。

![](img/f852e0a12c174e64d91a8e1a05146eab_211_0.png)

图 5-12 测试象限有助于对不同测试类别的受众和目的进行分类。

与所有基于象限的模型一样，有两个轴需要考虑。在垂直轴上，讨论的是测试的预期受众：技术人员或业务。在水平轴上，讨论的是测试目的：期望验证（定量）与分析（定性）结果。

### 业务/定量

企业通常与其客户和客户签订服务水平协议（SLAs）。这些是企业必须遵守的正式、可量化的标准，否则企业需对客户提供某种形式的赔偿。可用性是常见的 SLA 指标，企业承诺以 99.9% 的正常运行时间保持服务可用。由于这可以衡量并且对业务有直接影响，因此针对此类标准的测试位于此象限。

### 业务/定性

主观关注点如可用性就存在于此象限。这里更强调所涉及的技术，而更强调软件对业务的影响。A/B 和多变量测试，允许通过实验评估组件的多个版本，是整个软件领域中出现的趋势。与其通过焦点小组测试用户更喜欢矢车菊蓝还是海洋蓝，不如对两种蓝色进行 A/B 测试并衡量转化提升的统计显著性。

### 技术/定量

单元测试位于此象限，集成测试也是如此。这些测试支持开发团队量化系统与其需求的符合程度。单元测试通过率、代码覆盖率和圈复杂度等统计数据表明系统的整体健康状况。

### 技术/定性

在这里，你关注的是可能没有可量化需求的架构能力。负载测试关注系统在各种负载下表现的资源使用情况。对于服务而言，这可能包括吞吐量统计和响应时间曲线，随着更多用户同时访问系统。评估系统的安全性也是一种定性活动；这是通过渗透测试来评估的。系统的攻击向量难以量化，因此需要更分析性的方法。

测试象限表明，不同类别的测试各有不同。虽然本书主要关注单元测试实现和设计的低级细节，但你代码的适应性也依赖于拥有合适数量和合适类型的测试。

## 测试用于预防和治疗

迄今为止讨论的所有测试都涉及预防性测试。也就是说，提前投入精力以确保新功能按预期工作，并且没有现有功能被回归。

这是标准做法。但它并非没有成本。每项编写的测试都需要时间和精力。信心是测试的货币。需要牢记的等式是：

effort < confidence

如果你的努力没有产生所需的测试信心，它们就成本过高，你应该将精力集中在其他地方。当然，所有项目都有一个目标信心，以校准其对失败的容忍度。嵌入在起搏器中的软件需要的信心远高于为商业软件即服务解决方案提供动力的软件。遵循努力与信心的相关性，确保起搏器正确工作的努力因此要高得多。

但是，如果你不是在编写这种任务关键型软件，你有哪些选择来减少努力并增加信心？

图 5-13 显示了软件通常如何从开发到实时环境。

![](img/f852e0a12c174e64d91a8e1a05146eab_212_0.png)

图 5-13 软件可以在到达实时环境之前部署到多个环境进行测试。

随着流程的每个阶段，你对软件功能正确性和鲁棒性的信心都在增加。通过在不同范围和不同环境中[content]
After you reach your confidence threshold, the marginal extra confidence generated by continuing to add tests is not worth the effort. It is better to stop and focus on the quality and maintainability of the existing tests.

## The snowcone

Figure 5-11 shows what happens when the test pyramid becomes fully inverted: the cloud of uncertainty at the top has grown to gargantuan proportions, and there are almost no unit tests in sight.

![](img/f852e0a12c174e64d91a8e1a05146eab_210_0.png)

FIGURE 5-11 When the relative quantities of tests are inverted, the pyramid becomes a snowcone.

When the majority of testing effort is manual, this indicates that you have an untestable codebase. Work should begin promptly to refactor the code so that it is inherently testable. To factor in such work, use a combination of the golden master technique (see Chapter 6, "Refactoring") and Kanban's class of service (see Chapter 2, "Introduction to Kanban").

Manual tests are not as reliable as automated tests because of the fallibility of the person executing the test script. Such repetitive, monotonous work quickly becomes demotivating. Work to automate what you can so that the manual tests can be cheaply repeated whenever necessary.

## The testing quadrant

The testing covered in the testing pyramid exists at different granularities, from coarse-grained user interface tests to fine-grained unit tests. The test quadrant provides a complementary view of tests: they are applicable to different stakeholders and for different reasons.

To readers who are already somewhat familiar with the testing quadrant—after all, it is quite an old idea—the version presented in Figure 5-12 might look different. Software consultant Gojko Adzic admirably refreshed the testing quadrant to make it more relevant to the current state of the art. This figure is reproduced with the permission of Gojko Adzic.

![](img/f852e0a12c174e64d91a8e1a05146eab_211_0.png)

FIGURE 5-12 The testing quadrant helps categorize the audience and purpose of different test categories.

As with all quadrant-based models, there are two axes to consider. On the vertical axis, the intended audience of the tests is addressed: technologists or business. On the horizontal axis, the test purpose is addressed: expectation verification (quantitative) versus analytical (qualitative) outcomes.

### Business/Quantitative

Businesses tend to have service level agreements (SLAs) with their customers and clients. These are formalized, quantifiable standards with which the business must comply or be liable for providing the client some form of compensation. Availability is a common SLA criterion, whereby the business promises to keep a service available with 99.9% uptime. Because this is measurable and has a direct effect on the business, tests for these sorts of standards live in this quadrant.

### Business/Qualitative

Subjective concerns such as usability are found in this quadrant. The emphasis here is less on the technologies involved and more on the business impact of the software. A/B and multivariate testing, which allow for multiple versions of components to be evaluated through experimentation, are an emerging trend across the wider software spectrum. Rather than focus-group testing whether your users prefer cornflower blue or ocean blue, the two blues can be A/B tested and the statistical significance of conversion uplift can be measured.

### Technology/Quantitative

Unit tests reside in this quadrant, as do integration tests. These tests support the development team in quantifying how closely the system meets its requirements. Statistics such as unit test pass percentage, code coverage, and cyclomatic complexity indicate the overall health of a system.

### Technology/Qualitative

Here you focus on architectural capabilities for which you might not have quantifiable requirements. Load testing focuses on the resource usage that a system exhibits under various amounts of load. For a service, this is likely to include throughput statistics and response time curves as more users concurrently access the system. Assessing the security of a system is also a qualitative activity; this is assessed through penetration testing. The attack vectors of a system are difficult to quantify, so a more analytical approach is needed.

The testing quadrant shows that there are different categories of each kind of test. Although this book primarily focuses on the low-level details of unit test implementation and design, the adaptability of your code also relies on having the right amount of the right type of tests.

## Testing for prevention and cure

All of the testing discussed so far has dealt with testing for prevention. That is, effort is expended up front to ensure that new functionality works as expected and that no existing functionality has been regressed.

This is standard practice. But it is not without cost. Every test written takes time and effort. Confidence is the currency of tests. The equation to bear in mind is this:

effort < confidence

If your efforts do not generate the requisite test confidence, they are too costly and you should focus your effort elsewhere. Of course, all projects have a target confidence that calibrates their tolerance for failure. The software embedded in a pacemaker requires far more confidence than that which powers a commercial software-as-a-service solution. Following the correlation of effort and confidence, the effort that can be expended to ensure the correct working of a pacemaker is thus much higher.

But, if you are not writing such mission-critical software, what are your options for reducing the effort and increasing the confidence?

Figure 5-13 shows how software typically makes its way from development through to a live environment.

![](img/f852e0a12c174e64d91a8e1a05146eab_212_0.png)

FIGURE 5-13 Software can be deployed to many environments for testing before reaching a live environment.

With each phase of the process, your confidence in the functional correctness and robustness of the software increases. By exercising the code at different scopes and in different environments, you generate feedback that the code is working or is broken. After the code is released and verified in a live environment, your confidence is at its highest. What if you could find a shortcut from development to live? Your confidence would increase dramatically, yet the effort required would be minimal.

> “But,” you say, “without those incremental increases in confidence, we would fail in live so much more!”

Good.

There should never be a fear of failure in software development. If your culture is to fear failure, you cannot innovate. Instead, embrace the fact that you will fail, that you will roll back some releases. Failure is a better teacher than success. What you must do is shift your focus from Mean Time Before Failure (MTBF) toward Mean Time To Recovery (MTTR).

MTBF is a great measurement for systems in which you require a high level of confidence. It shows that the system is robust and has been very rigorously exercised. But as you now know, that level of confidence is expensive and is anathema to innovation.

MTTR, however, not only allows for failure, it prepares for it. Consider the possibility that you have a system with an MTBF of 100 days and an MTTR of 1 day. Thus, in aggregate, every three years, the system is unavailable for a day.

Compare this with a system that has an MTBF of 10 days and an MTTR of 1 hour. This system fails 10 times as often as the last! However, when it fails, it is operable again in only one hour: twenty-four times faster than the other system.

System 1 has an uptime of 99.99%.

System 2 has an uptime of over 99.995%.

You are enabled to fail fast by focusing on MTTR. This lets you loosen your grip on MTBF and innovate faster.

## How do you decrease MTTR?

When a service fails in a live environment, you must do something with it to put it back in a workable state. But first, you need to know that it isn’t working. Through a mixture of logging and alerting, you can monitor the health of your systems.

Logging is passive. If logging was the only option available, there would be a lot of time wasted polling the logs to see if something was going wrong. This is infeasible for most systems, because they could generate so much logging data that trying to discern a failure would become nearly impossible.

Alerting is active. When logging is in place, you can set acceptable boundaries that a variety of metrics should stay inside. If a metric breaches one of the boundaries, alerting can generate an event that informs you to start looking at specific parts of the logs and to take action.
