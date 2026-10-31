
## 应用概率演算用于
金融工程

本版首次出版于 2017 年

© 2017 John Wiley & Sons, Inc.

版权所有。未经许可，本出版物的任何部分不得以任何形式或任何方式复制、存储于检索系统或传输，包括电子、机械、影印、录音或其他方式，除法律允许外。有关如何获得本标题材料再使用许可的建议，请访问 http://www.wiley.com/go/permissions。

已根据法律断定 Bertram K C Chan 对本作品的作者身份的认定权。

## 注册办事处

John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030, USA

## 编辑部

111 River Street, Hoboken, NJ 07030, USA

有关我们全球编辑办公室、客户服务以及有关 Wiley 产品更多信息的详情，请访问 www.wiley.com。

Wiley 还以多种电子格式和按需印刷出版其书籍。标准印刷版中出现的某些内容可能在其他格式中不可用。

## 责任限制/免责声明

出版社和作者对本作品内容的准确性或完整性不作任何陈述或保证，并特别声明放弃所有保证；包括但不限于任何特定用途的适用性保证。本作品的销售是在理解出版社并未从事提供专业服务的假设下进行的。文中所含的建议和策略可能不适用于每种情况。鉴于持续的研究、设备修改、政府法规的变化以及与实验试剂、设备和器械使用相关的信息不断流动，读者应查阅并评估每个化学品、设备、试剂或器械包装说明书或说明中提供的信息，其中包括说明或使用指示的任何变化以及新增的警告和预防措施。仅因本作品中提及某个组织或网站作为引用和/或进一步信息的潜在来源，并不意味着作者或出版社认可该组织或网站可能提供的信息或其可能做出的建议。此外，读者应注意，本作品中列出的网站在作品撰写时与阅读时之间可能已更改或消失。任何促销性陈述均不得创设或延长对本作品的任何保证。出版社或作者均不对由此产生的任何损害承担责任。

## 美国国会图书馆出版物编目数据

Name: Chan, B. K. C. (Bertram Kim-Cheong), author. Title: Applied probabilistic calculus for financial engineering : an introduction using R / by Bertram K.C. Chan. Description: Hoboken, NJ : John Wiley & Sons, Inc., 2017. | Includes bibliographical references and index. | Identifiers: LCCN 2017024496 (print) | LCCN 2017037530 (ebook) | ISBN 9781119388081 (pdf) | ISBN 9781119388043 (epub) | ISBN 9781119387619 (cloth) Subjects: LCSH: Financial engineering—Mathematical models. | Probabilities. | Calculus. | R (Computer program language) Classification: LCC HG176.7.C43 2017 (print) | DDC 332.01/5192-dc23LC record available at http://lccn.loc.gov/2017024496

封面图片：(Top Image) © kWaIGon/Gettyimages; (Bottom Image) © da-kuk/Gettyimages

封面设计由 Wiley 完成

由 Thomson Digital, Noida, India 采用 10/12 pt WarnockPro-Regular 排版

谨献给上帝的荣耀和我的另一半

Marie Nashed Yacoub Chan

## 目录

前言 XIII

关于配套网站 XV

- 1 金融工程导论 1
- 1.1 什么是金融工程？ 1
- 1.2 本书标题的含义 2
- 1.3 金融工程中的持续挑战 3
- 1.3.1 金融市场的波动性 3
- 1.3.2 史密斯先生和夫人的 XYZ-LPL 账户的持续投资结果 4
- 1.4 “金融工程 101”：现代投资组合理论 6
- 1.4.1 现代投资组合理论 (MPT) 7
- 1.4.2 资产配置与投资组合波动性 7
- 1.4.3 均值-方差优化 (MVO) 的特征属性 8
- 1.5 资产类别假设建模 11
- 1.5.1 资产类别建模示例 11
- 1.5.1.1 建模资产类别 11
- 1.6 自有投资基金的一些典型示例 14
- 1.7 道琼斯工业平均指数 (DJIA) 与通胀 15
- 1.8 一些不太可取的股票投资方法 17
- 1.8.1 日内交易 17
- 1.8.2 算法交易 17
- 1.9 金融工程分析工具的开发 18
- 2 用于建模金融工程的概率演算 19
- 2.1 金融工程导论 19
- 2.1.1 一些经典金融数据 19
- 2.2 金融工程中的数学建模 19
- 2.2.1 离散模型与连续模型 19
- 2.2.2 决定性模型与概率模型 20

## 前言

*典型退休夫妇的财务挑战与经历 – 史密斯先生和夫人（非真实姓名）*

大约 10 年前，在从事约 40 年的稳定工作后，加州的约翰·A·史密斯先生和玛丽·B·史密斯夫人正在为包括全球广泛旅行在内的积极退休生活做准备。为了照顾他们未来的财务需求，他们决定聘请加州一家当地的专业金融工程和投资管理公司 – XYZ（虚构）– 的服务，该公司通过一家大型全国性金融工程公司 LPL（Linsco – 1968 年和 Private Ledger – 1973 年）进行交易。

为此，史密斯先生和夫人从毕生积蓄中投资了约 $2,000,000，目标如下：

- i) 保留其 $2 M 的资本
- ii) 从 XYZ 获得至少每月 $10,000 的净现金收入

因此，如果原始资本 $2 M 基本保持不变，同时维持每月 $10,000 的稳定提取，则 $2 M 投资的平均年回报率必须约为 (10,000 × 12)/2,000,000 = 0.06，即 6%。

金融服务管理通常收取约 1.5% 的费用。因此，粗略估计金融管理应实现约 6% + 1.5%，即 7.5%。

像 XYZ/LPL 这样的服务如何实现这一目标？退休约 10 年后，在 2016 年 11 月 15 日星期二，金融市场收盘时

| 项目 | 数值 |
|------|-------|
| Dow (DJIA) | 18,923.06/+54.03/+0.29% |
| Nasdaq | 5,275.62/+57.22/+1.10% |
| S&P 500 | 2,180.39/+16.19/+ 0.75% |
| Gold | $1,229.00 per oz +0.37% |

Chandra, S. (2003) Regional economy size and the growth-instability frontier: evidence from Europe. Journal of Regional Science 43 (1), 95–122. doi: 10.1111/1467-9787.00291

Chandra, S. and Shadel, W.G. (2007) Crossing disciplinary boundaries: applying financial portfolio theory to model the organization of the self-concept. Journal of Research in Personality, 41 (2), 346–373. doi: 10.1016/j.jrp.2006.04.007

Chicago Board of Options Exchange (CBOE) index: https://www.janus.com/advisor/funds/janus-balanced-fund?gclid=CKVx6yOsdACFQI daQodzxkNVA 2017.

Christodoulakis (2002) Bayesian optimal portfolio selection: the Black–Litterman approach. Class notes.

Coelen, N. (2000) Black–Scholes Option Pricing Model, Trinity University. Available at http://ramanujan.math.trinity.edu/tumath/research/studpapers/s11.pdf

Coelen, N. (2002) Introduction: finance is one of the most rapidly changing and fastest growing areas.

CRAN, The Comprehensive R Archive Network. http://cran-project.org/ 2017.

Da, Z. and Jagannathan, R. (2005) Teaching note on Black–Litterman model.

Dalgaard, P. (2002) Introductory Statistics with R. Springer Statistics and Computing Series, Springer Science+Business Media, New York, NY.

Damghani B. M. (2013) The non-misleading value of inferred correlation: an introduction to the contellation model. Wilmott Magazine. doi: 10.1002/wilm.102

Daniel, W.W. (2005) Biostatistics: A Foundation for Analysis in the Health Sciences, John Wiley & Sons, Inc., New York, NY.

Daroczi, G. et al. (2013) “Introduction to R for Quantitative Finance”, PACKT Publishing, Birmingham, U.K. www.packtpub.com/introduction-to-r-for-quantitative-finance/book

DeGroot, M. H. (1970) Optimal Statistical Decisions. Wiley Interscience.

Doganoglu, T., Hartz, C., and Mittnik, S. (2007) Portfolio optimization when risk factors are conditionally varying and heavy tailed. Computational Economics 29, 333–354. doi: 10.1007/s10614-006-9071-1

Dow Jones Industrial Average (DJIA) and Inflation http://thesovereigninvestor.com/exclusives/wall-street-legend-predicts-dow-50000/?z=590252 2017.

Dowd, K. (2007) Measuring Market Risk, 2nd Edition, John Wiley & Sons, Ltd, Hoboken, NJ.

Everitt, B.S. and Hothorn, T. (2006) A Handbook of Statistical Analysis Using R, Chapman & Hall/CRC, Boca Raton, FL.

Fantazzini, D. (2009) The effects of misspecified marginals and copulas on computing the value at risk: a Monte Carlo study. Computational Statistics Data Analysis, 53 (6), 2168–2188.
