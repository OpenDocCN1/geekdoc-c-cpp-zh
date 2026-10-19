

Rubin H. Landau, Manuel J. Páez and Cristian C. Bordeianu

# 计算物理学

用 Python 求解问题

第三版

![](img/bccda43674e4a93dee81c749eba8d2f7_0_0.png)

Rubin H. Landau
Manuel J. Páez
Cristian C. Bordeianu

# 计算物理学

# 相关书目

Paar, H.H.

# 高级量子物理学导论

2010

Print ISBN: 978-0-470-68675-1; also available in electronic formats

Har, J.J., Tamma, K.K.

# 粒子、材料和结构计算动力学进展

2012

Print ISBN: 978-0-470-74980-7; also available in electronic formats ISBN: 978-1-119-96589-3

Cohen-Tannoudji, C., Diu, B., Laloe, F.

# 量子力学

2 Volume Set

1977

Print ISBN: 978-0-471-56952-7; also available in electronic formats

Schattke, W., Diez Muiño, R.

# 量子蒙特卡洛编程

用于原子、分子、团簇和固体

2013

Print ISBN: 978-3-527-40851-1; also available in electronic formats

Zelevinsky, V.

# 量子物理学 1&2

2 Volume Set

2011

Print ISBN: 978-3-527-41057-6; also available in electronic formats

Rubin H. Landau
Manuel J. Páez
Cristian C. Bordeianu

# 计算物理学

用 Python 求解问题

第 3 版完全修订版

WILEY-VCH
Verlag GmbH & Co. KGaA

# 作者

Rubin H. Landau
Oregon State University
97331 Corvallis OR
United States

Manuel J. Páez
Universidad de Antioquia
Departamento Física
Medellin
Colombia

Cristian C. Bordeianu
National Military College "Ștefan cel Mare"
Câmpulung Moldovenesc
Romania

All books published by Wiley-VCH are carefully produced. Nevertheless, authors, editors, and publisher do not warrant the information contained in these books, including this book, to be free of errors. Readers are advised to keep in mind that statements, data, illustrations, procedural details or other items may inadvertently be inaccurate.

Library of Congress Card No.:
applied for

British Library Cataloguing-in-Publication Data:
A catalogue record for this book is available from the British Library.

Bibliographic information published by the Deutsche Nationalbibliothek
The Deutsche Nationalbibliothek lists this publication in the Deutsche Nationalbibliografie; detailed bibliographic data are available on the Internet at http://dnb.d-nb.de.

© 2015 WILEY-VCH Verlag GmbH & Co. KGaA, Boschstr. 12, 69469 Weinheim, Germany

All rights reserved (including those of translation into other languages). No part of this book may be reproduced in any form – by photoprinting, microfilm, or any other means – nor transmitted or translated into a machine language without written permission from the publishers. Registered names, trademarks, etc. used in this book, even when not specifically marked as such, are not to be considered unprotected by law.

Typesetting le-tex publishing services GmbH, Leipzig, Deutschland

Cover Design Formgeber, Mannheim, Deutschland

Print and Binding Markono Print Media Pte Ltd, Singapore

Print ISBN 978-3-527-41315-7
ePDF ISBN 978-3-527-68466-3
ePub ISBN 978-3-527-68469-4
Mobi ISBN 978-3-527-68467-0

Printed on acid-free paper.

To the memory of Jon Maestri

# 目录

- 致谢 V
- 前言 XIX
- 1 引言 1
- 1.1 计算物理学与计算科学 1
- 1.2 本书的主题 3
- 1.3 本书的问题 4
- 1.4 本书的语言：Python 生态系统 8
- 1.4.1 Python 包（库） 9
- 1.4.2 本书的包 10
- 1.4.3 简单的方法：Python 发行版（包集合） 12
- 1.5 Python 的可视化工具 13
- 1.5.1 Visual (VPython) 的 2D 绘图 14
- 1.5.2 VPython 的动画 17
- 1.5.3 Matplotlib 的 2D 绘图 17
- 1.5.4 Matplotlib 的 3D 曲面图 22
- 1.5.5 Matplotlib 的动画 24
- 1.5.6 Mayavi 的超越绘图的可视化 26
- 1.6 绘图练习 30
- 1.7 Python 的代数工具 31
- 2 计算软件基础 33
- 2.1 让计算机服从 33
- 2.2 编程热身 35
- 2.2.1 结构化且可重复的程序设计 36
- 2.2.2 Shell、编辑器和执行 37
- 2.3 Python I/O 39
- 2.4 计算机数字表示（理论） 40
- 2.4.1 IEEE 浮点数 41
- 2.4.2 Python 与 IEEE 754 标准 47
- 2.4.3 上溢和下溢练习 48
- 2.4.4 机器精度（模型） 49
- 2.4.5 实验：你的机器精度 50
- 2.5 问题：求和级数 51
- 2.5.1 数值求和（方法） 51
- 2.5.2 实现与评估 52

- 3 计算中的误差与不确定性 53
- 3.1 误差类型（理论） 53
- 3.1.1 灾难模型：相减抵消 55
- 3.1.2 相减抵消练习 56
- 3.1.3 舍入误差 57
- 3.1.4 舍入误差累积 58
- 3.2 贝塞尔函数中的误差（问题） 58
- 3.2.1 数值递推（方法） 59
- 3.2.2 实现与评估：递推关系 61
- 3.3 实验误差调查 62
- 3.3.1 误差评估 65

- 4 蒙特卡洛：随机性、行走与衰变 69
- 4.1 决定论随机性 69
- 4.2 随机序列（理论） 69
- 4.2.1 随机数生成（算法） 70
- 4.2.2 实现：随机序列 72
- 4.2.3 评估随机性和均匀性 73
- 4.3 随机行走（问题） 75
- 4.3.1 随机行走模拟 76
- 4.3.2 实现：随机行走 77
- 4.4 扩展：蛋白质折叠与自回避随机行走 79
- 4.5 自发衰变（问题） 80
- 4.5.1 离散衰变（模型） 81
- 4.5.2 连续衰变（模型） 82
- 4.5.3 带盖革计数器声音的衰变模拟 82
- 4.6 衰变实现与可视化 84

- 5 微分与积分 85
- 5.1 微分 85
- 5.2 前向差分（算法） 86
- 5.3 中心差分（算法） 87
- 5.4 外推差分（算法） 87
- 5.5 误差评估 88
- 5.6 二阶导数（问题） 90
- 5.6.1 二阶导数评估 90
- 5.7 积分 91
- 5.8 积分作为盒计数（数学） 91
- 5.9 算法：梯形法则 93
- 5.10 算法：辛普森法则 94
- 5.11 积分误差（评估） 96
- 5.12 算法：高斯求积 97
- 5.12.1 映射积分点 98
- 5.12.2 高斯点推导 99
- 5.12.3 积分误差评估 100
- 5.13 高阶法则（算法） 103
- 5.14 蒙特卡洛积分：石头投掷（问题） 104
- 5.14.1 石头投掷实现 104
- 5.15 均值积分（理论与数学） 105
- 5.16 积分练习 106
- 5.17 多维蒙特卡洛积分（问题） 108
- 5.17.1 多维积分误差评估 109
- 5.17.2 实现：1D 蒙特卡洛积分 110
- 5.18 快速变化函数的积分（问题） 110
- 5.19 方差缩减（方法） 110
- 5.20 重要性采样（方法） 111
- 5.21 von Neumann 拒绝采样（方法） 111
- 5.21.1 简单随机高斯分布 113
- 5.22 非均匀评估 113
- 5.22.1 实现 114

## 6 矩阵计算 117

- 6.1 问题 3：N−D Newton–Raphson；绳上两质量 117
- 6.1.1 理论：静力学 118
- 6.1.2 算法：多维搜索 119
- 6.2 为什么矩阵计算？ 122
- 6.3 矩阵问题类别（数学） 122
- 6.3.1 实用矩阵计算 124
- 6.4 Python 列表作为数组 126
- 6.5 数值 Python（NumPy）数组 127
- 6.5.1 NumPy 的 linalg 包 132
- 6.6 练习：测试矩阵程序 134
- 6.6.1 绳问题的矩阵解法 137
- 6.6.2 探索 139

## 7 试错搜索与数据拟合 141

- 7.1 问题 1：盒中量子态的搜索 141
- 7.2 算法：二分法的试错根 142
- 7.2.1 实现：二分算法 144
- 7.3 改进算法：Newton–Raphson 搜索 145
- 7.3.1 带回溯的 Newton–Raphson 147
- 7.3.2 实现：Newton–Raphson 算法 148
- 7.4 问题 2：磁化强度的温度依赖性 148
- 7.4.1 搜索练习 150
- 7.5 问题 3：拟合实验光谱 150

