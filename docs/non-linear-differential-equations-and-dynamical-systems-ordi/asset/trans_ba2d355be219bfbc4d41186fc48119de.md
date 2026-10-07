

## 非线性微分方程与动力系统

导致线性二阶微分方程 (3.96)。因此变量变换 (3.95a) = (3.97a, b)：

$$y(x) = -\frac{1}{R(x)} \frac{d}{dx}\{\log[u(x)]\} \quad \Leftrightarrow \quad u(x) = C \exp\left\{-\int^x R(\xi)y(\xi)d\xi\right\}$$

$(3.97a, b)$

将 (标准 LVIII) Riccati 方程 (3.58) 变换为 (3.96) = (3.98a-c)，即线性二阶微分方程 (3.98a)，其系数为 (3.98b, c)：

$$u'' + Au' + Bu = 0; \quad A = -P-\frac{R'}{R}, \quad B = QR.$$

$(3.98a-c)$

线性二阶微分方程 (3.98a) 的通积分是两个线性无关特积分 (3.99b) 的线性组合，包含两个任意常数：

$$C = \frac{C_2}{C_1} \quad u(x) = C_1u_1(x) + C_2u_2(x); \quad y(x) =-\frac{u_1'(x) + Cu_2'(x)}{R(x)u_1(x) + Cu_2(x)},$$

$(3.99a-c)$

由此可得 (3.95a) = (3.97a)，Riccati 方程 (3.58) 的解是单个积分常数 (3.99a) 的双线性函数 (3.99c)。

### 3.6.2 与特殊函数理论的关系

变换 (3.97a, b) 在以下方向成立：(i) 若 y 是 Riccati 方程 (3.58) 的解，则 (3.97b) 是线性二阶微分方程 (3.98a-c) 的解；(ii) 若线性微分方程 (3.98a-c) 的解 u 已知，则 (3.97a) 指定 Riccati 方程 (3.100) 的一个解：

$$y' =-\frac{B}{R}\left(A-\frac{R'}{R}\right)y + Ry^2.$$

$(3.100)$

线性二阶微分方程的解指定了多种特殊函数，如 Legendre（超球面 Legendre）多项式 [第 III.8.3 节 (III.9.6)] 和超几何函数（注 I.23.2-I.23.3）。这些特殊函数通常具有无穷表示，如高斯的幂级数（第 I.29.9 节和 II.3.9 节）和广义（第 I.30.20 节和注 II.3）的超几何级数以及超几何级数（第 II.1.9 节）。具有变系数的线性微分方程理论及其相关的特殊函数是

## 微分与一阶方程

随后考虑（第 9.4–9.9 节和注 9.1–9.47）。由于不存在 (i) 具有变系数的线性二阶微分方程 (3.98a) 的一般积分，(ii) Riccati 方程 (3.58) 的一般积分也几乎不可能。两者之间的关系可用于例如考虑与最简单的线性二阶微分方程相关的 Riccati 方程的解 [小节 3.6.3 (3.6.4)]，即具有常数（齐次）系数的方程 [第 1.3 节 (1.6)]。

### 3.6.3 对应于常数系数的 Riccati 方程

最简单的线性二阶微分方程具有常数系数（第 1.3 节），特征多项式的根 (a, b) 满足：

$D=\frac{d}{dx}=0=\{P_{2}(D)\}u(x)=\{(D-a)(D-b)\}u(x)=u''-(a+b)u'+ab\,u.$

若根不同 (3.102a)，特积分 (3.102b, c) 线性无关，且通积分是 (3.102d)：

$a\neq b;\quad u_{1}(x)=e^{ax},$
$u_{2}(x)=e^{bx},$
$u(x)=C_{1}e^{ax}+C_{2}e^{bx};$

微分方程 (3.101b) 的 (3.98a) 对应于 (3.103a, b) 标准 (LIX) Riccati (3.100c)：

${A,B}=\{-a-b,ab\};\quad y'=\frac{ab}{R}+(a+b-\frac{R'}{R})y+Ry^{2};$

其解 (3.99c) 涉及 (3.104b) 一个积分常数 (3.104a)：

$C=\frac{C_{2}}{C_{1}}-R(x)y(x)=\frac{C_{1}e^{ax}+C_{2}e^{bx}}{C_{1}e^{ax}+C_{2}e^{bx}}=1+\text{Exp}[(b-a)x];$

上述结果不适用于特征多项式具有重根的情况：

$0=\{P_{2}(D)\}u(x)=\{(D-a)^{2}\}u(x)=u''-2au'+a^{2}u;$

其中线性无关的特积分 (3.106a, b) 导致通积分 (3.106c)：

$u_{1}(x)=e^{ax},\quad u_{2}(x)=xe^{ax},\quad u(x)=e^{ax}(C_{1}+C_{2}x).$

微分方程 (3.105) ≡ (3.98a) 对应 (3.107a, b) 于 (标准 LX) Riccati (3.100) 对应 (3.107c)：

$\{A,B\} = \{-2a, a^2\}; \quad y' = \frac{a^2}{R} + (2a - \frac{R'}{R})y + Ry^2, \quad (3.107a–c)$

具有 (3.106a, b; 3.99c) 通积分 (3.108a)：

$C_0 = \frac{C_1}{C_2} - R(x)y(x) = \frac{C_2 + C_1ax + C_2x}{C_1 + C_2x} = \frac{1 + C_0 + ax}{C_0 + x}, \quad (3.108a, b)$

已证明具有常数系数的线性二阶微分方程 (3.101a) 具有特征多项式，其有两个不同根 (3.101b, 3.102a) 或重根 (3.105a)；具有 (i) 线性无关的特积分 (3.102b, c) [3.106a, b] 和通积分 (3.102d) [3.106c])，其中包含积分常数；且 (ii) 对应的 Riccati 方程 (3.103c) [3.107c) 具有 [标准 LIX (LX)] 通积分 (3.104b) [3.108b]，其中包含一个任意常数 (3.101a) [3.108a]。

### 3.6.4 对应于齐次系数的 Riccati 方程

用齐次 (3.109a) 导出式代替普通 (3.101a) 导数，从具有常数 (3.101b) 的线性二阶微分方程得到 (第1.6节) 齐次 (3.109b) 系数：

$\vartheta = x\frac{d}{dx} \quad 0 = \{P_2(\vartheta)\}u(x) = \{(\vartheta - a)(\vartheta - b)\}u(x) = x^2u'' - (a+b-1)xu' + abu. \quad (3.109a, b)$

若根不同 (3.110a)，特积分 (3.110b, c) 线性无关，通积分 (3.110d) 为线性组合：

$a \neq b: \quad u_1(x) = x^a, \quad u_2(x) = x^b, \quad u(x) = C_1x^a + C_2x^b. \quad (3.110a–d)$

微分方程 (3.109b) ≡ (3.98a) 对应 (3.111a, b) (标准 LXI) 于 Riccati (3.100) 对应 (3.111c)：

$\{A,B\} = \{\frac{1-a-b}{x}, \frac{ab}{x^2}\}; \quad y' = \frac{ab}{x^2R} + [\frac{a+b-1}{x} - \frac{R'}{R}]y + Ry^2, \quad (3.111a–c)$

## 微分与一阶方程

其通积分 (3.99c) 为 (3.112a, b)；

$a \neq b; \quad -Ry(x) = \frac{C_1ax^{a-1} + C_2bx^{b-1}}{C_1x^a + C_2x^b} = \frac{a+bCx^{b-a}}{x+Cx^{b-a+1}}, \quad (3.112a, b)$

使用 (3.104a)。
若特征多项式 (3.109b) 具有重根，则上述解 (3.112b) 不成立 (3.112a)：

$0 = \{P_2(\theta)u(x) = \{(\theta-a)^2\}u(x)=x^2u''-(2a-1)xu'+a^2u;}; \quad (3.113)$

在此情况下 (3.114a)，线性无关的特积分 (3.114b, c) 导致 (标准 LXI) 通积分 (3.114d)：

$a=b; \quad u_1(x)=x^a, \quad u_2(x)=x^a\log x; \quad u(x)=x^a(C_1+C_2\log x). \quad (3.114a-d)$

方程 (3.113) = (3.98a) 为 (3.115a, b) 对应 (3.100) Riccati 方程 (3.115c)：

$\{A,B\=\{\frac{1-2a}{x}, \frac{a^2}{x^2}\}; \quad y'=\frac{a^2}{x^2}+\frac{2a-1}{x}[\frac{R'}{R}]y+Ry^2, \quad (3.115a-c)$

其通积分为：

$-R(x)y(x)=\frac{C_1a+C_2a\log x}{C_1x+C_2x\log x}, = \frac{C_0a+a\log x}{C_0x+C_0\log x)}, \quad (3.116a, b)$

使用 (3.108a)。
已证明具有齐次系数的线性二阶微分方程，其特征多项式具有不同根 (3.109b, 3.110a) 或重根 (3.113)，具有：线性无关的特积分 (3.110b, c) (3.114b, c) 和通积分 (3.110d)(3.114d)，其中包含两个任意积分常数；且 (ii) 对应的 [标准 LXI (LXXX)] Riccati 方程 (3.111c) 具有通积分 (3.112b) (3.116b)，关于一个任意常数 (3.104a) [[3.104a]]。除利用 (i) 特积分（小节 3.5.2-3.5.5）或 (ii) 变换为线性二阶方程（小节 3.6.3-3.6.4）求解广义 Riccati 方程 (3.58) 外，(iii) 直接求解也是可能的，例如具有受限常数系数的原 Riccati 方程（小节 3.6.5）。

### 3.6.5 原 Riccati 方程的直接求解

广义 Riccati 方程 (3.58) 是原 Riccati 方程 (3.117d) 的推广，对应于系数 (3.117a–c)：

$R(x),Q(x),P(x)=\{b,\frac{\lambda}{x},ax^{\lambda}\}: \quad y'=ax^{\lambda}+\frac{\lambda}{x}y+by^{2}. \quad (3.117a–d)$

$y(x)=x^{\lambda}u(x): \quad x^{\lambda}u'=ax^{\lambda}+bu^{2}x^{\lambda}. \quad (3.118a, b)$

在特殊情况 (3.119a) 下，微分方程 (3.118a) 简化为 (3.119b)，即可分离变量：

$n=2\lambda: \quad x^{-\lambda}u'=a+bu^{2}, \quad \int\frac{du}{a+bu^{2}}-C=\int x^{\lambda}dx=\frac{x^{1+\lambda}}{1+\lambda}. \quad (3.119a–c)$

(3.119c) 右边的积分是直接的，左边的积分对 (a, b) 具有相同符号 (3.120a) [相反符号 (3.121a)] 时不同 (3.120b)[3.121b]：

$k=\frac{b}{a}>0: \quad \int\frac{du}{a+bu^{2}}=\int\frac{du}{1+ku^{2}}=\frac{1}{a\sqrt{k}}\int\frac{dv}{1+v^{2}}=\frac{1}{\sqrt{ab}}arc\tan(u\sqrt{k})$

$=\frac{1}{\sqrt{ab}}arc\tan(x^{-\lambda}y\sqrt{\frac{b}{a}}), \quad (3.120a, b)$

$k=-\frac{b}{a}>0: \quad \int\frac{du}{a+bu^{2}}=\int\frac{du}{1-ku^{2}}=\frac{1}{a\sqrt{k}}\int\frac{dv}{1-v^{2}}=\frac{1}{\sqrt{-ab}}arc\tan(u\sqrt{k})$

$=\frac{1}{\sqrt{-ab}}arg\tan(x^{-\lambda}y\sqrt{\frac{b}{a}}), \quad (3.121a, b)$

其中：(i) 在两种情况下均使用了变量变换 (3.122a, b)：

$v=u\sqrt{k}, \quad du=\frac{dv}{\sqrt{k}}, \quad u(x)=x^{-\lambda}y(x), \quad (3.122a–c)$

