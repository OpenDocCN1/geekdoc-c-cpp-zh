
梯度为零），*隐含假设这些极小值确实存在！* 然而，在概率演算中，这样的极小值，甚至这样的转折点，可能不存在或难以轻易定位。启发式方法可能被用来定位任何存在且可用的极小值。

用于定位极小值的一些有用启发式方法，以及相应的用于最小化的 R 程序将在以下章节中讨论。

### 6.2.1 进化算法 (EA)

受自然选择过程启发的优化算法自 1950 年代以来就被使用，通常被称为进化算法。遗传算法就是其中一种方法，由 Holland 在 1960 年代发明。遗传算法通常对固定或可变长度的位串应用逻辑运算，以便对种群进行交叉、变异和选择。随着世代的不断演进，种群成员更有可能成为目标函数的极小值。遗传算法已被证明是全局优化的有用启发式方法，特别是对于组合优化问题。进化策略是另一种类型的进化算法。遗传算法通常对固定或可变长度的位串应用逻辑运算，以便对种群进行交叉、变异和选择。随着世代的不断演进，种群成员更有可能代表目标函数的极小值。

遗传算法是全局优化的有用启发式方法，特别是对于组合优化问题。

### 6.2.2 差分进化 (DE) 算法

在投资组合优化中，特别是在评估投资组合的等风险贡献时，另一种有用的方法是差分进化 (DE) 算法，由 Storn 和 Ulrich 于 1997 年提出，其应用由 Price 等人 (2006) 展示。它被认为是一种遗传算法，并且是一种无导数全局优化器。

`DEoptim` 对 DE 的实现动机是为了扩展 R 语言和统计计算环境（R Development Core Team 2009）中可用于全局优化的算法集合。R 能够快速原型化目标函数，访问用于统计建模的各种工具，并能够轻松生成定制的结果图表（在许多情况下，这使得使用 R 比使用 Java、MS Visual C++、Fortran 90 或 Pascal 等语言编写的程序更可取）。`DEoptim` 可在 http://CRAN.R-project.org/package=DEoptim 获取。

## 6.3 金融风险建模与投资组合优化

在金融工程的现实世界中，大多数私人投资者通过一个或多个“财务顾问”进行操作，而这些顾问又与“财富管理公司”合作。

以下是一个典型财务顾问的例子（加利福尼亚州纽波特海滩的 Crystal Cove Advisors），其通过大型专业组织进行投资（如加利福尼亚州圣地亚哥的 LPL Financial）。

### 6.3.1 财富管理中一个典型专业组织的例子

### 6.3.1.1 LPL（Linsco Private Ledger）Financial

来自维基百科（图 6.3）：

*LPL Financial 是美国最大的独立财务顾问组织之一。成立于 1989 年，通过*

| 项目 | 详情 |
|---|---|
| LPL Financial | |
| 类型 | 公开 |
| 交易代码 | NASDAQ: LPLA |
| 行业 | 金融服务 |
| 成立 | 1968 |
| 总部 | 75 State Street<br>Boston, Massachusetts |
| 关键人物 | Mark Casady, 主席兼首席执行官 |
| 收入 | ▲ US$4.37 billion (2014) |
| 员工人数 | 3,384 |
| 母公司 | LPL Financial Holdings Inc. |
| 网站 | www.lpl.com |

图 6.3 LPL Financial.

两家经纪公司合并 – **Linsco**（成立于 1968 年）和 **Private Ledger**（成立于 1973 年）– 此后 LPL 将其独立财务顾问人数扩展到超过 14,000 人。LPL Financial 的主要办公室设在
- Boston, MA,
- Charlotte, NC, and
- San Diego, CA

分别覆盖美国东部、南部和西部地区，以及其他相关地区。

大约 3500 名员工为财务顾问、金融机构以及技术、托管和清算服务订阅者提供支持，提供使能技术、全面清算和合规服务、实践管理计划和培训以及独立研究。

LPL Financial 顾问为客户提供多种金融服务，包括股票、债券、共同基金、年金、保险和按费用计费的计划。然而，LPL Financial **不** 开发自己的投资产品，从而使公司的投资专业人员能够提供表面上免受经纪商/交易商引发的利益冲突的金融服务。

LPL 的附加信息
- 1) 最新时间线
- 2) 一些重要统计数据
- 3) 外部链接

### 6.3.1.1.1 最新时间线

1989 年，LPL Financial 通过两家小型经纪公司 *Linsco* 和 *Private Ledger* 的合并成立。

2003 年，LPL Financial 收购了 Private Trust Company，该公司为全美 50 个州的高净值客户管理信托和家庭资产。

2004 年，LPL Financial 收购了 Phoenix Companies 的经纪商/交易商业务，这为 Phoenix 提供了通过 LPL Financial 网络销售其产品的机会。

2005 年，私募股权公司 Hellman & Friedman 和 Texas Pacific Group 收购了该公司 60% 的股份。

2006 年 8 月，LPL Financial 在收购 UVEST Financial Services 后扩大了其客户群，UVEST Financial Services 在全美为 300 多家地区和社区银行及信用合作社提供独立经纪服务。

2007 年 6 月，LPL Financial 完成了对 Pacific Select Group（又名 Pacific Life）旗下几家经纪商/交易商的收购，增加了 2000 名财务顾问。

2007 年 9 月，LPL Financial 和 Sun Life Financial 宣布了一项最终协议，根据该协议，LPL Financial 的一家附属公司从 Sun Life Financial 收购了 Independent Financial Marketing Group, Inc. (IFMG)。Sun Life Financial 是领先的国际金融服务组织。管理 IFMG 业务的 LPL Financial Institution Services 业务部门是全国向银行和信用合作社提供投资和保险服务的主要提供商。该交易于 2007 年 11 月完成。

2008 年 1 月 1 日，Linsco/Private Ledger Corp.（LPL Financial Services）将其品牌名称更改为“LPL Financial”。

2010 年 11 月 18 日，LPL Financial 的母公司 LPL Investment Holdings Inc. 在纳斯达克股票市场上市，股票代码为 LPLA。

2011 年，LPL Financial 收购了总部位于新泽西州的 Concord Capital Partners，该公司帮助信托公司自动化其内部投资管理活动的业务实践。

2012 年 1 月，LPL Financial 收购了总部位于 Rockville 的 Fortigent，该公司为注册投资顾问、银行和信托公司提供高净值解决方案和咨询服务。

2015 年 11 月，LPL Financial 宣布了其首个顾问在线工具套件认证，面向 Investment Support Services。

### 6.3.1.1.2 一些重要统计数据

关于 LPL Financial 的关键事实包括以下内容：
- 450 万个已资助账户
- 14,000 名 *财务顾问* 得到支持
- 大约 4500 名技术、托管和清算服务订阅者
- 大约 700 家金融机构合作伙伴
- $475 billion 的咨询和经纪资产

### 6.3.1.1.3 外部链接

- LPL Financial 网站
- LPL Financial 招聘网站

作为通过 LPL 为公众（收费）服务的典型独立“财务顾问”的例子，请考虑以下内容

### Crystal Cove Advisors

- Crystal Cove Advisors 是位于加利福尼亚州纽波特海滩的投资管理公司。其专业团队将为客户提供投资策略，重点关注 *在寻求盈利结果的同时限制风险*。它认为避免严重损失是提高长期回报的最佳方式。
