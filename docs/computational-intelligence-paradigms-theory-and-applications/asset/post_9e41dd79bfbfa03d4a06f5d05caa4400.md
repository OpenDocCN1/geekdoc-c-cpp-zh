
![](img/d9a4cc12c48f7466f309cbd3c4549c73_317_0.png)

**FIGURE 7.22:** Fuzzy AND Operator “min”

which truncates the output fuzzy set, and prod (product), which scales the output fuzzy set produced by the implication process.

## Aggregation of the Outputs

The decisions in fuzzy sets are based on testing of all of the rules in an FIS editor, all the rules should be related somehow so as to make a decision. All the fuzzy sets that are responsible for generating the output are combined into a single independent fuzzy set in the aggregation process. Aggregation takes place only once for each output variable, exactly before the last step, defuzzification. The input of the aggregation process is the list of truncated output functions returned by the implication process for each rule. The output of the aggregation process is one fuzzy set for each output variable.

As long as the aggregation method is commutative, then the order in which the rules are executed is insignificant. This step uses three inbuilt methods of the MATLAB’s fuzzy logic toolbox such as max (maximum), probor (probabilistic OR), and sum (sum of each rule’s output set).

In Figure 7.23, all three rules have been placed collectively to demonstrate the output of each rule as aggregated into a single fuzzy set whose membership function assigns a weight value for every output value.

![](img/d9a4cc12c48f7466f309cbd3c4549c73_318_0.png)

**FIGURE 7.23:** Aggregation of the Output of Each Rule

## Defuzzify

The aggregate fuzzy output from the previous step is taken as input to the defuzzification process and the output of the defuzzification process is a single value. Since the aggregate of a fuzzy set from the previous step comprehends a range of output values, it is necessary that the aggregate output must be defuzzified in order to resolve a single output value from the set (Figure 7.24).

The most common defuzzification method is the centroid method, which returns the center of area under the curve. MATLAB’s fuzzy logic toolbox supports five inbuilt methods such as centroid, bisector, middle of maximum, largest of maximum, and smallest of maximum.

The Fuzzy Logic Toolbox aims to provide an open and easily modifiable fuzzy inference system structure. Thus, the Fuzzy Logic Toolbox is designed to be user friendly, to customize the fuzzy inference process for the required application. For instance, the user could replace various MATLAB functions for any of the default functions used in the five steps elaborated above: membership functions, AND methods, OR methods, implication methods, aggregation methods, and defuzzification methods.

![](img/d9a4cc12c48f7466f309cbd3c4549c73_319_0.png)

**FIGURE 7.24:** Defuzzified Output Using Centroid Method

## Advantages of the Mamdani Method

- It’s intuitive.
- It has widespread acceptance.
- It's well-suited to human input.

### 7.5.2 Sugeno-Type Fuzzy Inference

The entire fuzzy inference process elaborated to in the previous section is called Mamdani's fuzzy inference method, which is one of the primary methodology. In this section, the so-called Sugeno, or Takagi-Sugeno-Kang (TS method) method of fuzzy inference is discussed. The TS method was introduced in 1985, similar to the Mamdani method in several aspects. The first steps of the fuzzy inference process, fuzzifying the inputs and applying the fuzzy operator, are similar to that of Mamdani method. The main difference between Mamdani and Sugeno is that the Sugeno output membership functions are either linear or constant.

The Takagi Sugeno fuzzy model has the rules in the form

If “x is X” and “y is Y”, then “z = g(z)”

For a zero-order Sugeno model, the output level z can be a constant or a linear function. In this Sugeno type inference system the consequent part is a crisply defined function. The output level z of each rule is weighted by the firing strength w of the rule. The firing strength for a two input system is given by

w = AndMethod (G1(x), G2(y))

where G1,2 (.) are the membership functions for Inputs 1 and 2. The final output of the system is the weighted average of all rule outputs, computed as

Final Output = (∑_{i=1}^{N} W_i Z_i) / (∑_{i=1}^{N} W_i).

## 需求和架构设计文档

### 版本历史

| 版本 | 日期 | 作者 | 修改内容 |
|---|---|---|---|
| v1.0 | 2023-05-10 | 张伟 | 初始版本 |
| v1.1 | 2023-05-15 | 李娜 | 增加接口定义 |
| v1.2 | 2023-06-01 | 王强 | 修改数据库设计 |

### 1. 引言

本文档描述了系统的整体架构和核心需求。系统旨在提供高效、可靠的数据处理能力，支持大规模并发访问，并确保数据安全。

本文档适用于参与本项目的所有开发人员、测试人员、项目经理及业务相关方。

### 2. 总体架构设计

系统采用微服务架构，各服务之间通过RESTful API进行通信。整体架构分为以下几层：

- 展示层：负责前端页面渲染及用户交互
- 应用层：包含业务逻辑处理服务
- 服务层：提供通用业务能力组件
- 数据层：包含数据库、缓存及搜索引擎

![](img/d9a4cc12c48f7466f309cbd3c4549c73_320_0.png)

### 3. 核心功能需求

系统核心功能包括用户管理、数据分析、报表生成和权限控制。以下为关键需求描述：

> 安全性：所有外部接口必须采用OAuth 2.0协议进行身份认证，数据传输必须使用HTTPS加密。

系统需支持每秒1000次以上的并发请求处理，平均响应时间不超过200毫秒，保证99.9%的可用性。

condition, it must be updated regularly and smoothly to keep up with the changing state of the flight vehicle. In such cases, a Sugeno fuzzy inference system is extremely well suited to the task of smoothly interpolating the linear gains that would be applied across the input space; it's a natural and efficient gain scheduler. Similarly, a Sugeno system is suited for modeling nonlinear systems by interpolating between multiple linear models.

### Advantages of the Sugeno Method

- It's computationally efficient.
- It works well with linear techniques (e.g., PID control).
- It works well with optimization and adaptive techniques.
- It has guaranteed continuity of the output surface.
- It's well-suited to mathematical analysis.

### 7.5.3 Conversion of Mamdani to Sugeno System

The MATLAB command-line function mam2sug can be used to convert a Mamdani system into a Sugeno system (not necessarily with a single output) with constant output membership functions. It uses the centroid associated with all of the output membership functions of the Mamdani system. The following Mamdani system mam21.fis is taken as the input.

```matlab
% mam21.fis
[System]
Name = 'mam21'
Type = 'mamdani'
NumInputs = 1
NumOutputs = 1
NumRules = 4
AndMethod = 'min'
OrMethod = 'max'
ImpMethod = 'min'
AggMethod = 'max'
DefuzzMethod = 'centroid'

[Input1]
Name = 'angle'
Range = [-5 5]
NumMFs = 2
MF1='small':'gbellmf',[5 8 -5 0]
MF2='big':'gbellmf',[5 8 5 0]

[Input2]
Name = 'velocity'
Range = [-5 5]
NumMFs = 2
MF1='small':'gbellmf',[5 2 -5 0]
MF2='big':'gbellmf',[5 2 5 0]

[Output1]
Name = 'force'
Range = [-5 5]
NumMFs = 4
MF1='negBig':'gbellmf',[1.67 8 -5 0]
MF2='negSmall':'gbellmf',[1.67 8 -1.67 0]
MF3='posSmall':'gbellmf',[1.67 8 1.67 0]
MF4='posBig':'gbellmf',[1.67 8 5 0]

[Rules]
1 1, 1 (1) : 1
1 2, 2 (1) : 1
2 1, 3 (1) : 1
2 2, 4 (1) : 1
```

The code implementing the mam2sug function is shown below:

```matlab
mam_fismat = readfis('mam21.fis');
sug_fismat = mam2sug(mam_fismat);
subplot(1,2,1);
gensurf(mam_fismat, [1 2], 1);
title('Mamdani system (Output)');
subplot(1,2,2);
gensurf(sug_fismat, [1 2], 1);
title('Sugeno system (Output)');
```

The output in graphical format is shown in Figure 7.27.

![](img/d9a4cc12c48f7466f309cbd3c4549c73_324_0.png)

**FIGURE 7.27:** Illustration of Mamdani to Sugeno Conversion

## 7.6 Fuzzy Automata and Languages

Due to their diverse behavior application as a discrete model, cellular automata have created more interest in the implementation for several processes. Wolfram's discussion on universality and complexity in cellular automata described four classes of behavior for automata: class 1 for homogeneous stable behavior, class 2 for simple periodic patterns, class 3 for chaotic aperiodic behavior, and class 4 for complex behavior which generates local structures. Recent work by Cattaneo, Flocchini, Mauri, Quaranta Vogliotti, and Santoro introduced an alternate classification scheme that can be obtained by generalizing Boolean cellular automata to a fuzzy automata and then observing the qualitative behavior of a Boolean window embedded in a fuzzy domain. These automata can be classified according to whether the Boolean behavior dominates, a mixture of Boolean and Fuzzy behavior appears, or purely fuzzy behavior appears. The fuzzy behavior can further be divided into subclasses with homogeneous and non-homogeneous behavior. Classical cellular automata consist of an array of states, typically selected from a finite set, along with local rules for updating the array of states. Some of the simplest automata are defined on one dimensional lattice of cells, are Boolean (two state), and base the future state of a cell upon the states in a 3-cell neighborhood consisting of the cell and its left and right neighbors. Let denote the value, 0 or 1, of the cell at position i at time t.

Table 7.1 shows the behavior of an example automaton. It is called Rule 17 since the list of results, , gives the binary digits of 17. Rule 17
