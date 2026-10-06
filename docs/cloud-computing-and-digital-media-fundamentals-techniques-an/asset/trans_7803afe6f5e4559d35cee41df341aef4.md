

![](img/f13da3dd59d15874e4b22b03a274001b_0_0.png)

# 云计算与数字媒体

## 基础、技术与应用

编辑：
Kuan-Ching Li, Qing Li 和 Timothy K. Shih

![](img/f13da3dd59d15874e4b22b03a274001b_0_1.png)

# 云计算与数字媒体

基础、技术与应用

# 云计算与数字媒体

基础、技术与应用

编辑：
Kuan-Ching Li
Qing Li
Timothy K. Shih

CRC Press
Taylor & Francis Group
博卡拉顿 伦敦 纽约
CRC Press 是 Taylor & Francis Group 旗下品牌，属于 Informa 业务公司
一部 CHAPMAN & HALL 书籍

MATLAB® 是 The MathWorks, Inc. 的商标，经许可使用。The MathWorks 不保证书中文字或练习题的准确性。本书对 MATLAB® 软件或相关产品的使用或讨论并不构成 The MathWorks 对特定教学方法或 MATLAB® 软件特定使用的认可或赞助。

CRC Press
Taylor & Francis Group
6000 Broken Sound Parkway NW, Suite 300
Boca Raton, FL 33487-2742

© 2014 Taylor & Francis Group, LLC
CRC Press 是 Taylor & Francis Group 旗下品牌，属于 Informa Media Group

不对美国政府原始作品主张
版本日期：20131101

国际标准书号-13: 978-1-4665-6918-8 (电子书 - PDF)

本书包含源自真实且受推崇来源的信息。尽管已尽努力发布可靠的数据和信息，但作者和出版商不对所有材料的有效性或其后果承担责任。作者和出版商已尝试追溯本出版物复制的所有材料的版权所有者，如果未获得以这种形式出版的许可将向版权所有者道歉。如果任何版权材料未得到妥善说明，请告知我们，以便我们在未来的重印中进行纠正。

除美国版权法允许，未经出版者许可，本书的任何部分均不得以现在或以后发明的任何电子、机械或其他形式进行印刷、复制、传输或利用，包括影印、微缩胶片以及任何信息存储检索系统中的利用。请访问 http://www.copyright.com/ 或联系 Copyright Clearance Center, Inc. (CCC), 222 Rosewood Drive, Denver, MA 01923, 978-750-8400。CCC 是一个非营利组织，为各种用户提供许可和注册。对于获得 CCC 影印许可的组织，已授予单独的系统。

商标公告：产品或公司名称可能是商标或注册商标，仅用于标识和解释，无侵权意图。

访问 Taylor & Francis 网站 http://www.taylorfrancis.com

以及 CRC Press 网站 http://www.crcpress.com

# 目录

前言，ix
序言，xiii
编辑者，x
贡献者，xix

- 第1 章 移动多媒体云计算：概述 1
JIEHAN ZHOU, HAIBIN ZHU, MIKA YLIANTTILA, AND MIKA RAUTIAINEN
XIAOMING NAN, YIFENG HE, AND LING GUAN

- 第3 章 使用移动云服务的专业社区支持实践 47
DEJAN KOVACHEV AND RALF KLAMMA

- 第4 章 针对两种音乐信息检索范式的 GPU 与云计算 81
CHUNG-CHEH WANG, TZU-CHUN YEH, WEI-TSA KAO, JY-SHING ROGER JANG, WEN-SHAN LIOU, AND YAO-MIN HUANG

- 第5 章 云环境下 MPEG-DASH 的视频转码调度 103
ROGER ZIMMERMANN

- 第6 章 泛在学习的云端智能教学机制 127
MARTINS, YUNG-HUI, AND NEIL 

- 第7 章 多租户数据库的多查询优化 147
LI, JIN, WANG, AND SHI-FENG

- 第8 章 大规模相关性分类 169
FAUST, HAO, AND YIN 

- 第9 章 云端高效处理 191
YANG, SHU, AND CHING-FEI 

- 第10 章 搜索框架开发 235
ZHANG, XIAO, AND LEING-PIN 

- 第11 章 云集合研究 255
YAO, BIN, AND LUNG 

- 第12 章 云计算的用户界面 303
LAUREN, TATTAR, AND GALE 

- 第13 章 医疗保健中的标准化多媒体 345
PULKIT, DEVA, AND SHASH 

- 第14 章 云数字版权管理 345（注：原文显示为345）
等等，原文第13章和第14章都是345。
- 第14 章 云中的数字版权管理 345
PAOLO, OTTER, AND STEAUDIO 

- 第15 章 数字素养：云计算如何持续 359
RICHARDS, BRIAN, AND MATTHIAS

# 前言

随着移动设备用户的增加，对无处不在的访问需求的现代需求推动了数字媒体企业和高管对云计算的采用。大多数云中心可以被认为是地理中性的，因为全球各地的移动设备都可以访问它们。正是这种云服务的特性，使得数字媒体公司能够开发出新颖更好的方法，快速高效地向细分消费者交付媒体内容。

在受云计算强烈影响的各种技术学科中，数字媒体可能是从近期云计算进展中受益最深的。这种显著影响的一个原因可以归于数字媒体在生成、编码、存储、处理、传输、接收和消费的整个生命周期中具有巨大的数据量和实时性要求。云计算服务凭借其按需提供的特性，能够提供极其灵活的

许多数字媒体应用确实需要在数据中心进行计算，以便有效管理媒体内容，从而减轻媒体终端的计算需求负担。此类应用非常适合最公认的云计算服务类别——基础设施即服务（IaaS）。对于涉及指标数据的密集型计算，通常需要在云中心的并行机器来实现。最近，两种新类型的云计算服务，即软件即服务（SaaS）和平台即服务（PaaS），也被认为具有从根本改变分布在分散地理位置消费者访问媒体内容方式的潜力。

我们有理由云技术将深度渗透到各行各业。根据领先市场分析机构的最新预测，未来几年云服务的复合增长率应保持在20%甚至更高。基于云的策略还可以提高媒体公司的竞争优势。

# 前言

随着移动设备用户的增加，对无处不在的访问需求的现代需求推动了数字媒体企业和高管对云计算的采用。大多数云中心可以被认为是地理中性的，因为全球各地的移动设备都可以访问它们。正是这种云服务的特性，使得数字媒体公司能够开发出新颖更好的方法，快速高效地向细分消费者交付媒体内容。

