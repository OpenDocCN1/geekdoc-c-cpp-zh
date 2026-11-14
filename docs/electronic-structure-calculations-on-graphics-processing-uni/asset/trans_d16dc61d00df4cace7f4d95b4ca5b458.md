

![](img/255d48531d66773aa863436a333dac7d_243_0.png)

图 10.1 适应顺式视黄醇分子形状的实空间网格示例。立方体标记网格点的位置。出于可视化目的，我们展示的网格比实际计算中使用的网格更小、更粗糙。

could be avoided altogether to obtain a simpler full-potential DFT implementation that can run more efficiently on GPUs.

可以完全避免，以获得一种更简单的全势DFT实现，该实现可以在GPU上更高效地运行。

## 10.3 实空间方法的数值方面

The basic procedure in DFT (see Chapter 3) is to calculate the ground state density of a system by solving the KS equations [54]

DFT的基本程序（参见第3章）是通过求解KS方程[54]来计算系统的基态密度。

```
H[n]ψ_i(r) = ε_i ψ_i(r) (10.1a)
n(r) = Σ_{i=1}^N ψ_i^*(r)ψ_i(r) (10.1b)
```

where the operator $H$ is the KS effective single-particle Hamiltonian (atomic units are used throughout)

其中算子$H$是KS有效单粒子哈密顿量（全文均使用原子单位）

```
$H[n] = -\frac{1}{2}\nabla^2 + v_{xc}(r) + v_{bxc}[n](r,t).$ (10.2)
```

The external potential $v_{xc}$ contains the nuclear potential and other external fields that may be present, $v_{bxc}$ represents the electron-electron interaction and is usually divided into the Hartree term that contains the classical electrostatic interaction between electrons and the exchange and correlation (XC) potential.

外部势$v_{xc}$包含核势和可能存在的其他外部场，$v_{bxc}$表示电子-电子相互作用，通常分为包含电子之间经典静电相互作用的Hartree项以及交换-相关（XC）势。

To solve the KS equations, as it is standard in Hartree-Fock (HF) and DFT, a self-consistent field (SCF) iterative scheme is used [59–62]. Every SCF step we need to find the lower eigenvectors and eigenvalues of the KS Hamiltonian for a fixed electron density.

为求解KS方程，如Hartree-Fock（HF）和DFT中常见的那样，采用自洽场（SCF）迭代方案[59–62]。每个SCF步骤中，我们需要为固定电子密度找到KS哈密顿量的较低特征向量和特征值。

In real-space, the discretization of the KS Hamiltonian, Eq. (10.2), is achieved using a high-order finite differences representation [28]. As this results in a sparse operator representation, the diagonalization is performed using methods that do not require access to the elements of matrix representation of the Hamiltonian, but that instead apply the operator to the orbitals. Usually these eigensolvers are called iterative eigensolvers. We prefer the term sparse eigensolvers, as all eigensolvers, including the ones used for dense matrices, must be iterative as a corollary of the Abel–Ruffini theorem [65].

在实空间中，KS哈密顿量（公式10.2）的离散化通过高阶有限差分表示实现[28]。由于这导致稀疏算子表示，对角化采用不需要访问哈密顿量矩阵表示元素的方法，而是将算子作用于轨道。这些求解器通常称为迭代求解器。我们更倾向于使用稀疏求解器这一术语，因为所有求解器（包括用于稠密矩阵的求解器）都必须是迭代的，这是阿贝尔-鲁菲尼定理[65]的推论。

Several sparse eigensolvers have been proposed [64]. In this work, we use the efficient residual minimization directly inversion in the iterative subspace (RMM-DIIS) eigensolver [65, 66]. Eigenvectors are usually preconditioned, for example, in real-space typical choices are a multigrid-based preconditioner [57] or a filter operator that removes high-frequency components [67].

已提出多种稀疏求解器[64]。在本工作中，我们使用高效的残差最小化直接迭代子空间反演（RMM-DIIS）求解器[65, 66]。特征向量通常进行预处理，例如，在实空间中典型的选择是基于多重网格的预处理器[57]或滤除高频分量的滤波算子[67]。

The numerical operations required by most eigensolvers are the application of the KS Hamiltonian and two additional procedures that act over the whole set of orbitals: orthogonalization and subspace diagonalization [66]. Given a set of orbitals, the orthogonalization procedure performs a linear transformation that generates a new orthogonal set. Similarly, subspace diagonalization is an effective method to remove contamination between orbitals. It calculates the representation of the KS Hamiltonian in the subspace spanned by a set of orbitals, and generates a new set where the subspace Hamiltonian is diagonal.

大多数求解器所需的数值操作是应用KS哈密顿量以及作用于整个轨道集的两个额外程序：正交化和子空间对角化[66]。给定一组轨道，正交化程序执行线性变换以生成新的正交集。同样，子空间对角化是消除轨道间污染的有效方法。它计算由一组轨道张成的子空间中KS哈密顿量的表示，并生成新的集，其中子空间哈密顿量为对角矩阵。

After the diagonalization step a new set of orbitals and a new electron density are obtained; this density is mixed with the densities from previous steps to generate a new guess density. From the new guess density, the corresponding KS effective potential needs to be calculated. Numerically, the most expensive part of this step is obtaining the Hartree potential, $v_H$, that requires the solution of the Poisson equation. The approximated XC potential, $v_{xc}$, also needs to be recalculated each SCF step. This potential is usually approximated by a local or semi-local expression that is evaluated directly on the grid, in fact most DFT codes do this evaluation on a real-space grid.

对角化步骤后，得到一组新的轨道和新的电子密度；该密度与之前步骤的密度混合以生成新的猜测密度。从新的猜测密度出发，需要计算相应的KS有效势。从数值上讲，此步骤中最昂贵的部分是获得Hartree势$v_H$，这需要求解泊松方程。近似XC势$v_{xc}$也需要在每个SCF步骤中重新计算。该势通常由局部或半局部表达式近似，该表达式直接在网格上求值，事实上大多数DFT代码都在实空间网格上进行此求值。

TDDFT [68] is the extension of DFT to describe excitations and time-dependent processes. The basic formulation of TDDFT is given by the time-dependent KS (TDKS) equation

TDDFT [68]是DFT的扩展，用于描述激发和时间相关过程。TDDFT的基本公式由时间相关KS（TDKS）方程给出

```
$i\frac{\partial}{\partial t}\psi_k(r,t) = H[n(t)]\psi_k(r,t)$ (10.3a)
```

```
$n(r,t) = \sum_{k=1}^N \psi_k^*(r,t)\psi_k(r,t).$ (10.3b)
```

In this case the effective KS Hamiltonian is time-dependent. This dependency comes from the external potential, that can now involve some time-dependent fields, and from the Hartree and XC potentials that depend on the time-dependent density. In the exact TDDFT formulation, the XC potential depends on the density from all previous times and on the initial conditions. However, in practice these memory effects are neglected and the XC potential is only considered as a function of the electronic density at the current time, this is known as the adiabatic approximation [69].

在这种情况下，有效KS哈密顿量是时间相关的。这种依赖性来自外部势（现在可能涉及一些时间相关场）以及依赖于时间相关密度的Hartree和XC势。在精确的TDDFT公式中，XC势依赖于所有先前时间的密度和初始条件。然而，在实践中，这些记忆效应被忽略，XC势仅被视为当前时间电子密度的函数，这被称为绝热近似[69]。

The direct solution of the TDKS leads to the method of real-time TDDFT. This is a flexible approach to model the response of an electronic system, molecular [42] or crystalline [43], to different kinds of perturbations. It is useful, for example, to calculate optical absorption spectra [42, 47, 70], non-linear optical response [71, 72], circular dichroism [73, 74], van der Waals coefficients [75], Raman intensities [76, 77], and photoemission [78]. It is also the basis for the Ehrenfest-TDDFT molecular dynamics approach [35, 79–84].

直接求解TDKS导致实时TDDFT方法。这是一种灵活的方法，用于建模电子系统（分子[42]或晶体[43]）对不同类型扰动的响应。例如，它可用于计算光学吸收谱[42, 47, 70]、非线性光学响应[71, 72]、圆二色性[73, 74]、范德华系数[75]、拉曼强度[76, 77]和光电发射[78]。它也是Ehrenfest-TDDFT分子动力学方法[35, 79–84]的基础。

We now detail the procedure to perform a real-time propagation in real-space TDDFT. Typically, the initial conditions are the electronic ground-state as obtained from a DFT calculation. The KS orbitals are then propagated under the action of a time-dependent Hamiltonian. In the case of linear optical response calculations, the external field has the form \(E(r, t) = \kappa \delta(t)\) that can be applied as a phase to the initial KS orbitals [42, 70]. For crystalline systems, a macroscopic electric field cannot be included through the scalar potential and needs to be represented by a time-dependent vector potential [43].

我们现在详细介绍在实空间TDDFT中进行实时传播的程序。通常，初始条件是从DFT计算获得的电子基态。然后，KS轨道在时间相关哈密顿量的作用下传播。在线性光学响应计算的情况下，外部场的形式为\(E(r, t) = \kappa \delta(t)\)，可以作为相位应用于初始KS轨道[42, 70]。对于晶体系统，宏观电场不能通过标量势包含，而需要由时间相关矢量势表示[43]。

There are many approaches to perform the propagation of the KS orbitals and the electron density in time [85]. In this work, we use a predictor-corrector approach to account for the nonlinearity induced by the density dependence on Eq. (10.3a), combined with an approximate enforced time-reversal symmetry (AETRS) propagator [85]. The AETRS propagator, as several other propagation methods, requires the calculation of the exponential of the KS Hamiltonian. For the time-propagation results presented in this chapter, we use a fourth order Taylor expansion of the exponential. This exponential is never calculated explicitly, but applied over orbitals. Hence, as in the case of the eigensolver, the main operation required for the time propagation is the application of the KS Hamiltonian. In this case, there is no need to orthonormalize the orbitals, since orthonormality is preserved during the time evolution. Additionally, as in the case of a ground-state calculation, each time step we need to recalculate the Hartree and XC potentials.

有许多方法可以对KS轨道和电子密度进行时间传播[85]。在本工作中，我们使用预测器-校正器方法来处理由公式(10.3a)中的密度依赖性引起的非线性，并结合近似强制时间反演对称（AETRS）传播器[85]。AETRS传播器（如其他几种传播方法）需要计算KS哈密顿量的指数。对于本章中提出的时间传播结果，我们使用指数的四阶泰勒展开。该指数从未显式计算，而是作用于轨道。因此，与求解器的情况一样，时间传播所需的主要操作是应用KS哈密顿量。在这种情况下，不需要对轨道进行正交归一化，因为正交归一性在时间演化过程中被保留。此外，与基态计算的情况一样，每个时间步我们都需要重新计算Hartree和XC势。

In the real-time framework, the observables are time-dependent quantities. For example, the induced electric field is obtained from the electric dipole moment that can be readily calculated from the electronic density. For the calculation of circular dichroism the quantity of interest is the time-dependent magnetization, that is calculated as the expectation value of the angular momentum operator [73, 74]. Frequency resolved quantities are obtained from the Fourier coefficients of the time-resolved quantities. They are traditionally obtained through a windowed Fourier transform, however, more advanced method based on the compressed sensing approach have been shown to require considerably shorter, and computationally cheaper, time propagations [86, 87].

在实时框架中，可观测量是时间相关的量。例如，感应电场是从电偶极矩获得的，该电偶极矩可以很容易地从电子密度计算得出。对于圆二色性计算，感兴趣的量是时间相关磁化，它作为角动量算子的期望值计算[73, 74]。频率分辨量是从时间分辨量的傅里叶系数获得的。它们传统上通过窗口傅里叶变换获得，然而，基于压缩感应方法的更高级方法已被证明需要显著更短且计算成本更低的时间传播[86, 87]。

## 10.4 通用GPU优化策略

In this section, we discuss the general scheme that we have developed to efficiently solve the real-space DFT and TDDFT equations on GPUs. This strategy was designed taking into account the strengths and weaknesses of the current generation of GPUs, but is also effective for CPUs with vectorial floating point units.

在本节中，我们讨论了开发的通用方案，以便在GPU上高效求解实空间DFT和TDDFT方程。该策略在设计时考虑了当前一代GPU的优势和劣势，但对于具有矢量浮点单元的CPU也同样有效。

A way to fulfill the GPU requirement of multiple independent operations is to expose data-parallelism to the low-level routines. For example, if the same operation needs to be performed over multiple data objects, the routines should receive as an argument a group of those objects, instead of operating over one object per call. For the DFT case, our GPU optimization strategy is based on the concept of blocks of KS orbitals [6]. Instead of acting over a single KS orbital at a time, performance critical routines receive a group of orbitals as argument. By operating simultaneously over several orbitals, the amount of parallelism exposed to the processor is increased considerably. We illustrate this idea in Figure 10.2. This approach has been adopted by other real-space GPU implementations [16].

满足GPU多个独立操作要求的一种方法是向低级例程暴露数据并行性。例如，如果需要对多个数据对象执行相同的操作，例程应将一组这些对象作为参数接收，而不是每次调用对一个对象进行操作。对于DFT情况，我们的GPU优化策略基于KS轨道块的概念[6]。与一次作用于单个KS轨道不同，性能关键例程将一组轨道作为参数接收。通过同时对多个轨道进行操作，暴露给处理器的并行性量大大增加。我们在图10.2中说明这一想法。这种方法已被其他实空间GPU实现采用[16]。

