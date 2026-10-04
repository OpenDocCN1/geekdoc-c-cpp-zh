

速率的倒数，$\mu_X = 1/\lambda_e$，也是直观的。例如，当以约每分钟0.89辆的速度观察汽车时，注意汽车之间的平均等待时间大约为 $1/0.89 \approx 1.12$ 分钟。

因此，在当前示例中，你想要检验密度 $X \sim EXP(107/120)$。

```
R lambda.e <- 107/120
R lambda.e
[1] 0.8916667
```

假设一辆车刚刚经过个人的位置，你想找到他们必须等待超过两分半钟才能看到另一辆车的概率，换句话说，$Pr(X > 2.5)$。你可以使用 pexp 来做到这一点。

```
R 1-pexp(q=2.5,rate=lambda.e)
[1] 0.107681
```

这表明你有略高于10%的机会在下一辆车出现前观察到至少2分钟30秒的间隔。记住 p-函数的默认行为是从提供的值开始寻找累积的左侧概率，因此你需要从结果中减去1来找到上尾概率。你可以用以下方法找到等待时间少于25秒的概率，结果约为0.31：

```
R pexp(25/60,lambda.e)
[1] 0.310302
```

注意需要先将关注的值从秒转换为分钟，因为你已通过 $\lambda_e \approx 0.89$ 在后者的尺度上定义了 $f(x)$。

### The qexp Function

使用适当的分位数函数 qexp 来找到，例如，最短15%等待时间的截止点。

```
R qexp(p=0.15,lambda.e)
[1] 0.1822642
```

这表明关注的值约为0.182分钟，换句话说，大约 $0.182 \times 60 = 10.9$ 秒。

通常，你可以使用 rexp 生成任何特定指数分布的随机变体。

NOTE 很重要区分“指数分布”、“指数分布族”和“指数函数”。第一个指的是刚刚研究的密度函数，而第二个指的是概率分布的一般类，包括泊松、正态和指数分布本身。第三个是标准数学指数函数，指数族成员依赖于它，并且可以直接在 R exp 中访问。

## Exercise 16.5

- a. 位于新西兰北岛中部，普胡图间歇泉据说是最活跃的南半球间歇泉。假设它每年喷发平均3,500次。

  - i. 以随机变量 X 为连续喷发之间的时间建模的意图下，评估参数 $\lambda_e$ 关于天的时间尺度（平均每年365.25天以考虑闰年）。

  - ii. 绘制感兴趣的密度函数。喷发之间平均等待时间为多少天？

  - iii. 等待下一次喷发少于30分钟的概率是多少？

  - iv. 什么等待时间定义了最长的10%等待？将你的答案转换为小时。

- b. 你也可以使用指数分布来建模某些产品服务，或“时间到失效”类型的变量。假设某制造商的特定空调单元知道该产品平均使用11年后才需要维修。设随机变量 X 表示其中一个单元需要维修的时间，X 服从指数分布且 $\lambda_e=1/11$。

  - i. 公司对其单元提供五年全维修保修。随机选择的空调使用保修的概率是多少？

  - ii. 竞争对手对其竞争的空调单元提供六年保证，但知道其单元平均使用九年后才需要某种维修。利用该保修的机会是多少？

  - iii. 确定 (i) 中的单元和 (ii) 中的单元使用超过15年的概率。

## 16.2. Other Density Functions

有许多其他常用的概率密度函数用于涉及连续随机变量的各种任务。我们在此总结其中几个：

- 卡方分布对正态变量的平方和进行建模，并且通常与涉及正态分布数据的样本方差的操作相关。其函数为 dchisq、pchisq、qchisq 和 rchisq，并且与 t 分布（第16.2.3节）一样，它依赖于作为参数 df 提供的自由度。

- F 分布用于对两个卡方随机变量的比率进行建模，并且在例如回归问题（参见第20章）中有用。其函数为 df、pf、qf 和 rf，因为它涉及两个卡方值，它依赖于作为参数 df1 和 df2 提供的自由度对的指定。

- 伽马分布是指数分布和卡方分布的推广。其函数为 dgamma、pgamma、qgamma 和 rgamma，并且它依赖于作为参数 shape 和 scale 分别提供的“形状”和“尺度”参数。

- Beta 分布通常用于贝叶斯建模，并且具有实现的函数 dbeta、pbeta、qbeta 和 rbeta。它由两个“形状”参数 a 和 beta 定义，作为 shape1 和 shape2 提供。

特别是，你将在接下来的几章中遇到卡方和 F 分布。

在过去几节中你检查的所有常见概率分布中，我强调了执行“one-minus”操作以找到关于右上尾区域的概率或数量的必要性。这是因为 p- 和 q- 函数的累积性质——根据定义，处理的是下尾。然而，R 中大多数 p- 和 q- 函数都包含一个可选参数 lower.tail，其默认为 FALSE。因此，另一种选择是在任何相关函数调用中设置 lower.tail=TRUE，在这种情况下，R 将期望或返回特定的上尾区域。

NOTE

## Important Code in This Chapter

| Function/operator | Description | First occurrence |
|---|---|---|
| dinom | Binomial mass function | Section 16.1.2, p. 335 |
| pbinom | Binomial cumulative problems | Section 16.1.2, p. 336 |
| qbinom | Binomial quantiles function | Section 16.1.2, p. 337 |
| rbinom | Binomial random realizations | Section 16.1.2, p. 337 |
| dpois | Poisson functions | Section 16.1.3, p. 340 |
| ppois | Poisson cumulative problems | Section 16.1.3, p. 341 |
| rpois | Poisson random realizations | Section 16.1.3, p. 341 |
| dunif | Uniform density function | Section 16.2.1, p. 346 |
| punif | Uniform cumulative problems | Section 16.2.1, p. 346 |
| qunif | Uniform quantiles | Section 16.2.1, p. 346 |
| runif | Uniform random realizations | Section 16.2.1, p. 347 |
| dnorm | Normal density function | Section 16.2.2, p. 350 |
| pnorm | Normal cumulative problems | Section 16.2.2, p. 353 |
| qnorm | Normal quantiles | Section 16.2.2, p. 353 |
| rnorm | Normal random realizations | Section 16.2.2, p. 355 |
| qt | Student's t quantiles | Section 16.2.3, p. 358 |
| dt | Student's t density | Section 16.2.3, p. 358 |
| dexp | Exponential density function | Section 16.2.4, p. 359 |
| pexp | Exponential cumulative problems | Section 16.2.4, p. 361 |
| qexp | Exponential quantiles | Section 16.2.4, p. 361 |
| rexp | Exponential random realizations | Section 16.2.4, p. 361 |

Common Probability Distributions 363

# PART IV

STATISTICAL TESTING AND MODELING

# 17

# SAMPLING DISTRIBUTIONS AND CONFIDENCE

![](img/b2cfc85cbb129f60fe595a2bae074fe4_400_0.png)

在第15章和第16章中，你将概率分布的想法应用于随机变量被定义为某种感兴趣的测量或观察的例子。在本章中，你将把样本统计量本身视为随机变量来引入*抽样分布*的概念——一种用于解释在使用样本统计量估计总体参数时自然存在的变异性的概率分布。然后我将介绍置信区间的概念，它是对抽样分布中变异性的直接反映，以一种导致总体参数区间估计的方式使用。这将为第18章中的正式假设检验奠定基础。

## 17.1 Sampling Distributions

抽样分布就像任何其他概率分布一样，但它专门与作为样本统计量的随机变量相关联。在第15章和第16章中，我们假设我们知道相关示例分布的参数（例如，均值和标准差
*
