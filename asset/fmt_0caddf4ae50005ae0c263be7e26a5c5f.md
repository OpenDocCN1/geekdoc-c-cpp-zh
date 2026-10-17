
$\pi^{(f)}(\gamma, \theta|D_0, a_0) \propto \prod_{j=1}^{K_0} \pi_{j=0}^{K_k}(\exp\{ij_j+l_k(\gamma_0 + \gamma_1 + \theta_k)\}) \times \exp\{-(\gamma_0 + \gamma_1 + \theta_k)/a_0+l_k\} \pi_0^{(f)}(\theta_0)d\theta_0 \pi_0^{(f)}(\gamma, \theta).$ (4.10)

其中 $0 \le a_0 \le 1$，$\pi_0^{(f)}(\theta_0)$ 和 $\pi_0^{(f)}(\gamma)$ 是初始先验。在 (4.10) 中，假设 $\gamma_0, \gamma_1, \theta_k$ 和 $\gamma_k$ 服从独立的初始先验 $N(0,\sigma_{\theta_0}^2)$、$N(0,\sigma_{\gamma}^2)$、$N(0,\tau_{\theta_k}^2)$ 和 $N(0,\tau_{\gamma}^2)$。

在 (4.10) 中，参数 $a_0$ 控制历史元序列数据 $D_0$ 对当前数据 $D_K$ 的影响。参数 $a_0$ 可以解释为历史元生存数据的折减参数。将 $a_0$ 的范围限制在 0 到 1 之间是合理的，因此我们取 $0 \le a_0 \le 1$$a_0$ 的主要作用之一是控制模型中 $\gamma_0$ 和 $\gamma_1$ 先验的尾部厚度。随着 $a_0$ 变小，(4.10) 的尾部变得更厚。如果 $a_0=0$，先验不依赖于历史元生存数据。也就是说，$a_0=0$ 等于于为当前研究纳入任何历史元生存数据的先验规范。因此，参数 $a_0$ 控制历史元生存数据对当前研究的影响。当历史与当前元生存数据之间存在异质性，或者历史与当前元生存数据的样本量差异时，这种控制是非常关重要的。

在 (4.10) 中，我们倾向于考虑固定的 $a_0$。当 $a_0$ 固定时，我们确切知道新的元实验中纳入了多少历史元数据，以及第一类错误和统计功效与 $a_0$ 之间的关系。如 4.7 模拟研究中的 SAS MACRO BSMED 所示，固定的 $a_0$ 为我们控制第一类错误提供了额外的灵活性。此外，我们的信息先验规范仅允许我们为历史数据和当前数据的模型借用历史元实验数据。因此，历史元实验数据对 $\gamma_0$ 和 $\gamma_1$ 的影响最大。出于这个原因，[6] 和 [10] 将 (4.10) 给出的功效先验称为“部分借用功效先验”。

### 4.5.2 采样先验

现在，我们转向指定采样先验。在 (4.3) 提出的模型下，我们采用采样先验：

$\pi^{(S)}[\gamma, \theta_l] \propto \alpha^{(S)}(\gamma_0) \pi^{(S)}(\theta_l) \pi_l^{(S)}(\gamma_1)$ 对于 $l=0,1$。在采样先验中，我们首先为 $\gamma_1$ 指定点先验 $\pi^{(S)}(\gamma_1) = \Delta\{\gamma_1=\log(\zeta)\}$ 对于 $l=0$，以及

$\pi^{(S)}(\gamma_1) = \Delta\{\gamma_1=0\}$ 对于 $l=1$，其中 $\Delta\{\gamma_1=\gamma_1^*\}$ 表示 $\gamma_1=\gamma_1^*$ 处的退化分布。然后我们还为 $\pi^{(S)}(\gamma_0)$ 和 $\pi^{(S)}(\theta_0)$ 指定点先验。注意，设计值 $\{\gamma_0, \theta_0\}$ 是通过求解以下方程得到的：

$1-\exp\{\gamma_0+\theta_k\}=r_k$ 和 $\sum_{k=1}^K\theta_k=0$，

其中 $r_k$ 是预定的年发生率。如 4.7 SAS MACRO BSMED 示例，我们假设研究数量 $K=9$，年发生率为 $r_k=0.12$ 对于 $k=1..8$，且 $r_g=0.15$。然后通过求解上述方程，我们得到 $\gamma_0=-4.32, \theta_k=-0.25$ 对于 $k=1..8$，以及 $\theta_g$。因此我们可以根据设计值指定点先验。

## 4.6 算法

### 4.6.1 预测数据生成

在本节中，我们扩展了 [6] 和 [10] 中的算法，通过引入 4.2 中讨论的试验时长 $\hat{T}_k^D$ 和入组时间 $\hat{\tau}_k^A$ 来生成先验生存数据。具体而言，除了采样先验 $\pi^{(S)}(\gamma, \theta)$ 之外，我们还使用 $\hat{D}_k$ 和 $\hat{\tau}_k^A$ 构建预测生存数据 $D_K$ 中的截断时间。我们的预测数据算法如下：

- 1. 生成 `{\gamma, \theta} \sim \pi^{(S)}(\gamma, \theta)`。
- 2. 对于 `i=1..n_{jk}, j=1..2, k=1..K`，独立生成 `Y_{ijk} \sim f(Y_{ijk}|\theta, x_{ijk})`。
- 3. 如果 `\hat{\tau}_k^A=0`，则设置 `\tau_{ijk}^*=0`；如果 `\hat{\tau}_k^A>0`，则独立生成入组时间 `\tau_{ijk}^*=U(0, \hat{\tau}_k^A)` 对于 `i=1..n_{jk}, j=1..2, k=1..K`。
- 4. 对于 `i=1..n_{jk}, j=1..2, k=1..K`，设置 `C_{ijk}^*=\hat{\tau}_k^D-\hat{\tau}_k^A`。
- 5. 对于 `i=1..n_{jk}, j=1..2, k=1..K`，计算 `y_{jk}=\sum_{i=1}^{n_{jk}}\min(Y_{ijk}, C_{ijk}^*)` 和 `v_{jk}=\sum_{i=1}^{n_{jk}}1\{Y_{ijk} \le \tau_{ijk}^*\}`，其中指示函数 `1\{Y_{ijk} \le \tau_{ijk}^*\}` 在 `Y_{ijk} \le \tau_{ijk}^*` 时为 1，否则为 0。
- 6. 对于 `j=1..2, k=1..K`，设置 `D_K=\{y_{jk}, v_{jk}, x_{ijk}\}`。

### 4.6.2 后验分布采样

在模型 (4.3) 下，利用 (4.4) 和 (4.10)，$(\gamma, \theta_D, \theta_0)$ 的后验分布为：

$\pi(\gamma, \theta_D, \theta_0 | D_K, D_0) \propto \prod_{k=1}^K \prod_{j=1}^2 \exp\{v_{jk}(\gamma_0 + \gamma_1 x_{jk} + \theta_k) - (\gamma_0 + \gamma_1 x_{jk} + \theta_k)v_{jk}\} \times \prod_{k=1}^K \prod_{j=1}^2 (\exp\{y_{0,j} + l_k(\gamma_0 + \gamma_1 + \theta_k)\})^{\theta_0} \pi_0^{(f)}(\theta_0)\pi_0^{(f)}(\gamma)。 (4.11)$

我们使用 Gibbs 采样从给定 $D_K$ 和 $D_0$ 的 (4.11) 后验分布中采样。Gibbs 采样要求在给定其他参数的情况下，从每个参数的全条件分布中采样。首先，`[\gamma | \theta_D, \theta_0, D_K, D_0]` 的全条件密度为：

$\pi(\gamma | \theta_D, \theta_0, D_K, D_0) \propto \prod_{k=1}^K \prod_{j=1}^2 \exp\{v_{jk}(\gamma_0 + \gamma_1 x_{jk} + \theta_k) - (\gamma_0 + \gamma_1 x_{jk} + \theta_k)v_{jk}\} \times \prod_{k=1}^K \prod_{j=1}^2 (\exp\{y_{0,j} + l_k(\gamma_0 + \gamma_1 + \theta_k)\})^{\theta_0} \exp\{-\frac{1}{2} \gamma^T \Sigma_{\gamma}^{-1} \gamma\}, (4.12)$

其中 $\Sigma_{\gamma} = \text{diag}(\sigma_0^2, \sigma_f^2)$ 表示 $\gamma$ 的 $2 \times 2$ 协方差矩阵。

`[\theta_0 | \theta_D, D_0, a_0]` 的全条件密度为：

$\pi(\theta_0 | \theta_D, D_0, a_0) \propto \prod_{k=1}^K \prod_{j=1}^2 (\exp\{y_{0,j} + l_k(\gamma_0 + \gamma_1 + \theta_k)\})^{\theta_0} \exp\{-exp[\gamma_0 + \gamma_1 j + \theta_k]y_{j}]^{\theta_0}\} \exp\{-\frac{1}{2}\theta_0^T \Sigma_{\theta_0} \theta_0\}, (4.13)$

其中 $\Sigma_{\theta_0} = \sigma_0^2/K_0$ 表示 $\theta_0$ 的 $K_0 \times K_0$ 协方差矩阵。

很容易证明 (4.11) 到 (4.13) 中的全条件分布在每个参数上都是对数凹的。因此，我们可以实现 [15] 中的自适应拒绝算法，从 `[\gamma, \theta, \theta_0]` 的后验分布中采样。

### 4.6.3 功效计算

我们讨论了如何计算 [6] 中讨论的第一类错误和功效（power）。令 $n_0$ 和 $a_0$ 分别表示历史元实验生存数据的预设贝叶斯置信水平和折减参数。我们还令 `{\gamma^{(m)},  m=1, \dots, NMCS}` 表示来自后验分布 `\pi(\gamma, \theta_{D_K}, D_0, a_0)` 的 `\gamma_1` 的 Gibbs 样本，其中 `NMCS` 是 Gibbs 样本的量。使用该 Gibbs 样本，我们得到 `P(e^{\gamma_1} < \delta_{\pi^{(f)}})` 的蒙特卡洛估计值：

```
$$\hat{P}_f = \frac{1}{NMCS} \sum_{m=1}^{NMCS} I(e^{\gamma_1^{(m)}} < \delta), \quad (4.14)$$
```

其中 `\pi^{(f)}` 是拟合先验。为了同时计算贝叶斯第一类错误和公式 (4.9) 中的 `\beta_{sl}^{(f)}`，我们使用以下计算算法：

- 1. 设置 `l=0` 并输入 `D, D_0, n_0, \varsigma, a_0, NMCS, nbi,` 和 `REP`。
- 2. 为 `s=0,1` 生成 `{(\gamma, \theta)-\pi^{(s)}}(\gamma, \theta)`。
- 3. 通过 4.6.1 节中的预测数据生成算法生成 `D_K`。
- 4. 运行 Gibbs 采样器从后验分布 `\pi(\gamma, \theta_{D_K}, D_0, a_0)` 生成大小为 `NMCS` 的 Gibbs 样本 `{\gamma_1^{(m)}, m=1, \dots, NMCS}`。
- 5. 计算 `\hat{P}_f` 并重复步骤 2 到 5 共 `REP` 次。
- 6. 在这 `REP` 次运行中，计算 `{\hat{P}_f \geq 0.90},{\hat{P}_f \geq 0.95}` 和 `{\hat{P}_f \geq 0.975}`（默认选项）的比例以及 `{\hat{P}_f \geq n_0}`（用户选择）的比例，从而给出 `\beta_{sl}^{(n)}` 的估计值。
- 7. 如果 `|x|=1`，则返回步骤 2。

## 4.7 SAS MACRO BSMED

### 4.7.1 BSMED 的实现

#### 4.7.1.1 详细宏选项

在本节中，我们介绍了用于贝叶斯生存元实验设计的 SAS 宏 `BSMED` 的细节。如 4.2 “元设计设置”所述，`BSMED` 宏需要两个输入数据集（即当前数据和历史数据（可选））、11 个输入变量以及一个输出文件（可选）。输入变量和设计值的名称与描述显示了 SAS 宏中输入变量和设计值的名称及描述。

表 4.4 输入变量和设计值的名称与描述

| 数据 | 宏中的名称 |  |
|---|---|---|
| 历史 | a0 | 折减参数 ($\alpha_0$) |
| | sigma0 | $\gamma_0$ 的初始方差 ($\sigma_0^2$) |
| | sigma1 | $\gamma_1$ 的初始方差 ($\sigma_1^2$) |
| 当前 | tau0 | $\theta_{UK}$ 的初始方差 ($\theta_{UK}^2$) |
| | tau | $\theta_K$ 的初始方差 ($\theta_K^2$) |
| 设计 | delta | 设计非劣效性边界 ($\zeta$) |
| | eta0 | 用户定义的贝叶斯置信水平 ($\eta_0$) |

在宏中，需要输入变量（包括 MCMC 运行次数 (NCMC)、模拟数据集数量 (DEP) 和预热样本数 (nbi)）来运行 MCMC 并生成预测生存数据。此外，我们还包含一个初始种子数 (SEEDGEN) 作为输入变量。输入的历史数据应使用 SAS 变量名 `\kappa, y, v,` 和 `\kappa` 分别代表试验 ID (TID)、受试者总持续时间、事件数和治疗组指示，其中 0 表示对照组，1 对应实验组。输入的当前数据需要 SAS 变量名 `K, n, p, x, TA` 和 `TD` 分别代表试验 ID、总样本量、对照组受试者比例、年化事件率、入组时间和试验时长。`BSMED` 宏的结构如下：

```
%macro BSMED(hist,curr,delta,eta0,NMCS,nbi,a0,REP,sigma0,sigmal,tau0,tau,SEEDGEN,output);
```

- 1. 生成预测生存数据
- 2. 从后验分布中采样
- 3. 计算第一类错误和功效
- 4. 预期的输出

```
%mend BSMED;
```

`BSMED` 宏不需要历史数据的输入文件。如果有历史数据，我们可以简单使用：

```
%BSMED(HIST=hist,curr=curr,delta=1.3,a0=0.10,eta0=0.96,NMCS=20000,nbi=5000,REP=5000,sigma0=
```

如果没有历史数据，我们简单使用：

```
%BSMED(CURR=curr,delta=1.3,a0=0.10,eta0=0.96,NMCS=20000,nbi=5000,REP=5000,sigma0=
```

如上述宏所示，`BSMED` 由四个主要部分组成：生成预测生存数据、运行 MCMC 从后验分布中采样、使用后验估计计算第一类错误以及产生预期的输出。在随后的子节中，我们为这些宏的主要组件提供了详细开发，除了使用 PROC REPORT 的预期输出。

### 4.7.2 预测生存数据

根据 4.6.1 描述的算法，我们在宏中简要介绍预测数据的生成。在代码 1 预测数据的第一部分显示了从采样先验生成 `\gamma_0` 和 `\gamma_1` 的 SAS 代码。对于 `s=0` 和 `s=1`，我们在原假设和备择假设下从采样先验生成 `\gamma_1`。在代码 1 预测数据的第二部分，我们利用当前数据 `i=1..n, j=2, k=1..k` 生成失效时间 `V_{ijk}` 和入组时间 `A_{ijk}` 以及计算截断时间。然后，我们计算 `j=2` 的总事件数 `(v_{jk})`。这些量是构建每个模拟集合当前数据似然函数的关键组件，通过初始种子（例如 SEED=123456789）进行数据生成以复制相同的结果。

#### 代码 1 预测生存数据的生成

```
%do s=0 to 1;

data current&;

set current_new;

gammal0=

if &s=0 then do;

gammal1=log(&delta);

else do;

gammal0=0;

end;

theta_k=

lambda=exp(gamma0+gamma1*x+theta_k);

end;

%do s=0 to 1;

do m=1 to &REP; (使用种子数作为变量)

data current_sim;

set current&;

y=0;

v=0;

call streaminit(&seed);

do i=1 to n;

yi=-log(RAND('UNIFORM'))/lambda;

if TA=0 then do;

tAI=0;

else do;

tAI=RAND('UNIFORM')*TA;

end;

ci=TD-TAI;

if yi<=ci then do;

vi=1;

time=yi;

else do;

vi=0;

time=ci;

end;

y=y+time;

v=v+vi;

end;

output;

keep K v group;

run;

%end;

%end;
```

### 4.7.1.3 运行 MCMC 从后验分布采样

示例 4.2 运行蒙特卡洛 (MCMC) 显示了如何使用部分先验从后验分布采样。我们允许用户选择参数 `\gamma_0,\theta_{jk}` 和 `\theta_k` 的初始方差。由于我们不需要打印每个模拟集合的后验估计，我们使用选项抑制 SAS 窗口中的后验估计。`ods exclude all` 选项还可以节省存储并减少计算时间。为了重现结果，我们在 PROC MCMC 中使用初始种子（例如 SEED=123456789）生成的值。
