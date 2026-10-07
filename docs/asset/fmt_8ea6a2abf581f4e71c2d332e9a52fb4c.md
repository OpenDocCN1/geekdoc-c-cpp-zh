
`seq(1,a)`. `seq(2,c)`. `seq(3,g)`. `seq(4,a)`. `seq(5,a)`. `seq(6,a)`.

`seq(7,u)`. `seq(8,c)`. `seq(9,g)`. `seq(10,a)`. `seq(11,a)`. `seq(12,a)`.

`seq(13,c)`. `seq(14,g)`. `seq(15,s)`. `seq(16,c)`. `seq(17,a)`. `seq(18,a)`.

`seq(19,u)`. `seq(20,u)`. `seq(21,u)`. `seq(22,u)`. `seq(23,g)`. `seq(24,u)`.

![](img/820e4521e28ac939f5ce28.png)

## 7.A.4 蛋白质结构

1. 以下实例有等效解，但很容易看出第一个无法被改进。

```
% hhhhhhhhh

prot(1,h). prot(2,p). prot(3,p). prot(4,h).

prot(5,p). prot(6,p). prot(7,p). prot(8,p).

prot(9,p). prot(10,p). prot(11,p). prot(12,p).

prot(13,p). prot(14,p). prot(15,p). prot(16,h).
```

2. 寻找下一个实例的最优解少于 `1 min`。在最优折叠中，氨基酸相互封闭并形成蛋白质的核心。该实例具有氨基酸接触。

```
% hhhhhpp

prot(1,h). prot(2,p). prot(3,p). prot(4,h).

prot(5,p). prot(6,p). prot(7,h). prot(8,p).

prot(9,p). prot(10,h). prot(11,p). prot(12,p).

prot(13,h). prot(14,p). prot(15,p). prot(16,h).
```
注意该氨基酸序列表示为 $h(php)^n$。通过添加三元组可以得到 $n > 0$ 的 $h(php)^n$ 实例。3. 该实例有多个最优解，但很容易看出最优解无法被改进。

```
% hhhhhhhhhhhhhhhhh

prot(1,h). prot(2,h). prot(3,h). prot(4,h).

prot(5,h). prot(6,h). prot(7,h). prot(8,h).

prot(9,h). prot(10,h). prot(11,h). prot(12,h).
```
这类氨基酸序列可以通过添加事实显地得到。

## 7.A.5 基因调控网络

这是 [Gebser 等人，2011] 中使用的数据。

```
vertex(le1), vertex(li1), vertex(g), vertex(lacY)

vertex(lac2), vertex(lac1), vertex(a), vertex(cAMPRC5)

%

input(le), input(g)

%

edge(le1,li1), edge(lacY,li1) 

%

edge(lac2,lacY), edge(lac1,lac2), edge(lac2,lacY)

edge(lac2,a), edge(a,lac2), edge(cAMPRC5)

edge(cAMPRC5,lac2)

%

observed(le1,plus), observed(le1,g,plus), observed(lacY,li1)

observed(lacY,plus), observed(lac1,lacY,minus), observed(lac1,lac2,minus)

observed(lac2,li1,minus), observed(lac2,g,minus), observed(lac2,a,plus)

observed(a,minus), observed(cAMPRC5,minus), observed(cAMPRC5,lac2,plus).
```
通过添加节点可以获得不同的结果。对于以下输入，获得带有边的最小解：

```
observed(le1,plus), observed(li1,plus)

observed(g,plus), observed(lacY,plus)

observed(lac2,plus), observed(lac1,plus).
```
在给出以下观测结果时，网络是一致的，答案集为：

```
observed(le1,plus), observed(g,plus).
```

## 7.A.6 代谢网络

这是图 7.13 的完整实例。

```
draft(d)

reaction(r1,x), reaction(r2,x), reaction(r3,d)

reaction(r4,d), reaction(r5,x), reaction(r6,d)

reactant(m1,r1), reactant(m2,r2), reactant(m2,r3)

reactant(m3,r4), reactant(m4,r4), reactant(m1,r5)

reactant(m4,r5), reactant(m4,r6)

product(m3,r1), product(m3,r2), product(m4,r3)

product(m5,r4), product(m6,r5), product(m7,r6)

seed(m1), seed(m2), target(m5), target(m7).
```

## 第 7 章 探索生命：集合编程

以下示例来自 Thiele 的博士论文 [Thiele 2012]。

```
draft(d).

reaction(r1,d), reaction(r2,d), reaction(r3,d).

reaction(r4,d), reaction(r5,d), reaction(r6,d).

reaction(r7,a), reaction(r8,a), reaction(r9,a).

reactant(m7,r2), reactant(m8,r2).

reactant(m3,r3), reactant(m4,r3), reactant(m5,r5).

reactant(m6,r6), reactant(m7,r6), reactant(m8,r6).

product(m4,r1), product(m5,r2), product(m6,r3).

product(m7,r4), product(m8,r5), product(m9,r6).

seed(m8), target(m9).
```
