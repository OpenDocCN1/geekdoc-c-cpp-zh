

### 7.2.2 超软势

In order to reduce the number of plane waves, actual calculations resort to pseudopotentials: close to each ion, the exact wavefunction is replaced by pseudo-wavefunctions centered on the ion.
为了减少平面波的数量，实际计算采用伪势：在每个离子附近，精确波函数被以离子为中心的伪波函数所取代。

The radial part of the pseudo-wavefunctions is nodeless. These pseudo-wavefunctions are localized in r-space and will be denoted by \(|\tilde{\beta}\rangle\). Projection on these pseudo-wavefunctions are denoted by \(\{\tilde{\beta}\}\), which are the dual vectors of \(|\tilde{\beta}\rangle\). The \(\tilde{\beta}\) functions of each type of atom are defined with respect to the displacement from an atomic center and vanish outside of a core region:
伪波函数的径向部分没有节点。这些伪波函数在r空间中是局域化的，将用 \(|\tilde{\beta}\rangle\) 表示。对这些伪波函数的投影用 \(\{\tilde{\beta}\}\) 表示，它们是 \(|\tilde{\beta}\rangle\) 的对偶向量。每种原子的 \(\tilde{\beta}\) 函数是相对于原子中心的位移定义的，并在核心区域之外消失：

\(\tilde{\beta}(r) = \beta(r - R), \quad \beta(r > r_c) = 0,\)

where \(R_i\) is the position of the ion that \(\beta\) is centered around and \(r_c\) is the cut-off radius.
其中 \(R_i\) 是 \(\beta\) 所围绕的离子的位置，\(r_c\) 是截断半径。

With USPPs, the tensor \(Q\) connects diagonal real-space 2-tensors, such as the density \(\rho\), to pairs of projectors [20]:
采用USPP时，张量 \(Q\) 将对角实空间2-张量（如密度 \(\rho\)）与投影算子对联系起来 [20]：

\(\langle \psi' | r | r' \psi \rangle \rightarrow \sum_{ij} \langle \psi' | r' \rangle \left( \langle r' | r \rangle \langle r | r' \rangle + \sum_{ij} \langle r' | \beta_i \rangle Q_{ij} \langle \beta_j | r' \rangle \right) \langle r' | \psi' \rangle,\) (7.9)

where \(\psi, \psi'\) are arbitrary vectors. Integrating over \(r\) yields an overlap matrix
其中 \(\psi, \psi'\) 是任意向量。对 \(r\) 进行积分得到重叠矩阵

\(S = I + \sum_{ij} |\beta_i\rangle Q_{ij} \langle \beta_j|,\) (7.10)

which defines the inner product \(\langle \phi | \psi \rangle \rightarrow \langle \phi | S | \psi \rangle\), where \(Q_{ij} = Q_{ij}(r)\). The eigenproblem is therefore generalized to
它定义了内积 \(\langle \phi | \psi \rangle \rightarrow \langle \phi | S | \psi \rangle\)，其中 \(Q_{ij} = Q_{ij}(r)\)。因此特征问题推广为

\(H|k\rangle |u_{nk}\rangle = \epsilon_{nk} S |u_{nk}\rangle.\) (7.11)

The change in inner product leads to an additional term in the charge density:
内积的变化导致电荷密度中出现一个额外项：

\(\langle r | \rho | r \rangle = \sum_{nk} f_{nk} \left( \langle r | u_{nk} \rangle \langle u_{nk} | r \rangle + \sum_{ij} \langle u_{nk} | \beta_i \rangle Q_{ij}(r) \langle \beta_j | u_{nk} \rangle \right)\) (7.12)

It also leads to the density-dependent nonlocal potential \(V^{nl}[\rho(u, \epsilon)]\), which adds to the cyclic dependence of Eq. (7.8). In the USPP scheme, \(V^{nl}\) is
它还导致了密度依赖的非局域势 \(V^{nl}[\rho(u, \epsilon)]\)，这增加了Eq. (7.8)的循环依赖。在USPP方案中，\(V^{nl}\) 为

\(V^{nl} = \sum_{ij} |\beta_i\rangle D_{ij} \langle \beta_j|,\) (7.13)

where the matrix \(D_{ij}\) depends on the density \(\rho\).
其中矩阵 \(D_{ij}\) 依赖于密度 \(\rho\)。

The rest of this chapter operates with the generality of USPP. The NCPP expressions are recovered by letting \(Q \rightarrow 0\), which implies \(S \rightarrow I\) and reduces the generalized eigenvalue problem to a standard one.
本章其余部分采用具有普遍性的USPP进行处理。通过令 \(Q \rightarrow 0\) 可以恢复NCPP表达式，这意味着 \(S \rightarrow I\) 并将广义特征值问题简化为标准问题。

### 7.2.3 投影增量波（PAW）方法

The PAW scheme [13] is a generalization of the USPP scheme [12] introduced in Section 7.2.2. In the PAW scheme, the wavefunction is related to smooth pseudo-wavefunctions by a linear transformation [13]:
PAW方案 [13] 是第7.2.2节中介绍的USPP方案 [12] 的推广。在PAW方案中，波函数通过线性变换与平滑伪波函数相关联 [13]：

\(|\psi\rangle = |\tilde{\psi}\rangle + \sum_i (|\phi_i\rangle - |\tilde{\phi}_i\rangle) \langle \tilde{\beta}_i | \tilde{\psi} \rangle.\) (7.14)

where the \(\phi\) are generally taken to be solutions to the radial Schrödinger equation for an isolated atom and tildes mark pseudo-quantities. Computationally, PAW and USPP take very similar forms. The relationship between the two is discussed more formally in the literature [12]. Here, we maintain consistency with the notation used for USPPs by letting \(\tilde{\beta} \equiv \beta\).
其中 \(\phi\) 通常取为孤立原子径向Schrödinger方程的解，波浪号标记伪量。从计算角度看，PAW和USPP采用非常相似的形式。两者之间的关系在文献 [12] 中有更正式的讨论。这里，我们通过令 \(\tilde{\beta} \equiv \beta\) 来保持与USPP所用记法的一致性。

### 7.2.4 力与应力

Forces are computed by differentiating the total energy function with respect to ionic positions:
力是通过对离子位置对总能函数求导来计算的：

\(F_i^\mu = -\frac{\partial E[\rho]}{\partial R_i^\mu}.\) (7.15)

where \(\mu\) indexes the spatial components and \(i\) indexes the atomic centers.
其中 \(\mu\) 索引空间分量，\(i\) 索引原子中心。

The total energy is equal to the sum of the electronic energy from the Hamiltonian in Eq. (7.1) and the electrostatic energy due to the ions. This last term will be denoted by \(U[\{R\}]\):
总能量等于Eq. (7.1)中哈密顿量的电子能与离子静电能之和。最后一项将用 \(U[\{R\}]\) 表示：

\(E_{tot}(\{f\}, \{u\}, \{R_i\}) = \frac{1}{N_k} \sum_{nk} f_{nk} \langle u_{nk} | T + V^{nl} | u_{nk} \rangle + \frac{1}{2} \iint dr dr' \frac{\rho(r)\rho(r')}{|r - r'|} + E_x[\rho] + \int dr V_{ion}^{loc}(r)\rho(r) + U[\{R\}].\) (7.16)

where the local potential is separated into its electron-electron Coulombic (Hartree), electron-electron exchange-correlation, and electron-ion Coulombic contributions. Let us introduce \(V_{ext}(r)\), \(D_{ij}^{ion}\), and the onsite density \(\rho_{ij}\):
其中局域势被分离为电子-电子库仑（Hartree）、电子-电子交换-相关和电子-离子库仑贡献。让我们引入 \(V_{ext}(r)\)、\(D_{ij}^{ion}\) 和原位密度 \(\rho_{ij}\)：

\(V_{ext}(r) = \frac{\partial E_{tot}}{\partial \rho} = V_{ion}^{loc}(r) + \int dr' \frac{\rho(r')}{|r - r'|} + \frac{\delta E_x[\rho]}{\delta \rho}.\) (7.17)

\(D_{ij}^{ion} = D_{ij} + \int dr V_{ext}(r) Q_{ij}(r).\) (7.18)

\(\rho_{ij} = \sum_{nk} f_{nk} \langle u_{nk} | \beta_i \rangle \langle \beta_j | u_{nk} \rangle.\) (7.19)

Using these definitions, the total energy can be written as
使用这些定义，总能量可以写成

\(E_{tot}(\{f\}, \{u\}, \{R_i\}) = \frac{1}{N_k} \sum_{nk} f_{nk} \langle u_{nk} | T | u_{nk} \rangle + \int dr V_{eff}(r)\rho(r) + \frac{1}{N_k} \sum_{ij} D_{ij} \rho_{ij} + U[\{R\}].\) (7.20)

leading to the following expression for the forces:
从而得到力的以下表达式：

\(F_i^\mu = -\frac{\partial U[\{R\}]}{\partial R_i^\mu} - \int dr \frac{\partial V_{ion}^{loc}(r)}{\partial R_i^\mu} \rho(r) - \int dr V_{ext}(r) \sum_{ij} \frac{\partial Q_{ij}(r)}{\partial R_i^\mu} \rho_{ij} - \sum_{ij} D_{ij}^{ion} \sum_{nk} f_{nk} \left[ \langle u_{nk} | \frac{\partial \hat{\beta}_i}{\partial R_i^\mu} | \beta_i \rangle \langle \beta_i | u_{nk} \rangle + \langle u_{nk} | \beta_i \rangle \langle \beta_i | \frac{\partial \hat{\beta}_i}{\partial R_i^\mu} | u_{nk} \rangle \right].\) (7.21)

where we have used
其中我们使用了

\(\frac{\partial \rho(r)}{\partial R_k^\nu} = \sum_{nk} f_{nk} \sum_{ij} \frac{\partial Q_{ij}(r)}{\partial R_k^\nu} \langle \beta_i | u_{nk} \rangle \langle u_{nk} | \beta_j \rangle + Q_{ij}(r) \frac{\partial (\langle \beta_i | u_{nk} \rangle \langle u_{nk} | \beta_j \rangle)}{\partial R_k^\nu}.\) (7.22)

Another interesting quantity is the stress tensor. Let us denote by \(\mathbf{a}_1, \mathbf{a}_2, \text{and } \mathbf{a}_3\) the unit cell lattice vectors. We combine them in \(\mathbf{h} = [\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3]\). With these notations, the stress components are
另一个有趣的量是应力张量。让我们用 \(\mathbf{a}_1, \mathbf{a}_2, \text{和 } \mathbf{a}_3\) 表示单元胞晶格矢量。我们将它们组合为 \(\mathbf{h} = [\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3]\)。采用这些记法，应力分量为

\(\sigma_{\mu\nu} = -\frac{1}{\Omega} \sum_i \frac{\partial E_{tot}}{\partial \mu_i} T_{\mu\nu}^i\) (7.23)

where \(\mu\) and \(\nu\) denote the Cartesian indices.
其中 \(\mu\) 和 \(\nu\) 表示笛卡尔索引。

As the interaction energy between electrons and ions depends only on their distances, one can recast the previous equation into [3]
由于电子与离子之间的相互作用能仅取决于它们的距离，可以将前一公式改写为 [3]

\(\sigma_{\mu\nu} = -\left\langle \Psi \left| \sum_p \frac{1}{2m_p} \nabla_{\mu,p} \nabla_{\nu,p} - \frac{1}{2} \sum_{p,p'} \frac{(r_{pp'})_\mu (r_{pp'})_\nu}{|r_p - r_{p'}|} \frac{\partial V}{\partial r_{pp'}} \right| \Psi \right\rangle.\) (7.24)

where the sum over \(p\) and \(p'\) runs over all particles (nuclei and electrons) and \((r_{pp'})_\mu\) is the \(\mu\) Cartesian coordinate of \(\vec{r}_{pp'}\), the vector joining particles \(p\) and \(p'\).
其中对 \(p\) 和 \(p'\) 的求和遍及所有粒子（原子核和电子），\((r_{pp'})_\mu\) 是连接粒子 \(p\) 和 \(p'\) 的矢量 \(\vec{r}_{pp'}\) 的 \(\mu\) 笛卡尔分量。

The pseudopotentials introduce a dependence on the wavefunctions. The number of wavefunction terms grows with the system size, so the computation of those terms dominates the cost of computing forces and stresses.
伪势引入了对波函数的依赖。波函数项的数量随系统大小增长，因此计算这些项主导了计算力和应力的成本。

Efficient evaluation of the stress tensor will not be further discussed here. Interested readers are redirected to, for example, [3] or [21].
应力张量的高效计算在此不再进一步讨论。感兴趣的读者可参阅，例如，[3] 或 [21]。

### 7.2.5 迭代对角化

In the self-consistent scheme, the Hamiltonian itself is converging along with the charge density. Therefore, each self-consistent iteration does not require the exact diagonalization of the Hamiltonian, so long as the eigensolutions are converging as quickly as the Hamiltonian. Furthermore, we are interested in the lowest \(N_e\) eigenvalues and associated eigenfunctions, as only the \(N_e \gtrsim n_e\) lowest eigenfunctions contribute to the charge density. Directly diagonalizing the Hamiltonian would be a waste of effort.
在自洽方案中，哈密顿量本身与电荷密度一起收敛。因此，每次自洽迭代不需要对哈密顿量进行精确对角化，只要特征解的收敛速度与哈密顿量一样快即可。此外，我们关注最低的 \(N_e\) 个特征值及其相关特征函数，因为只有最低的 \(N_e \gtrsim n_e\) 个特征函数对电荷密度有贡献。直接对角化哈密顿量将是一种浪费。

Iterative procedures provide an elegant solution to this problem: the eigenproblem can be solved in a subset (generally called the *expansion set*) [22] that is much smaller than the plane-wave basis. Any eigensolutions of the full problem will also be eigensolutions in the expansion space. There exist several common iterative approaches for PWDFD:
迭代方法为这一问题提供了优雅的解决方案：特征问题可以在一个子集（通常称为*扩展集*）[22]中求解，该子集远小于平面波基。全问题的任何特征解也将是扩展空间中的特征解。对于PWDFD存在几种常见的迭代方法：

- the conjugate gradient algorithm [23, 24],
- 共轭梯度算法 [23, 24]，
- the blocked Davidson scheme [25–28], and
- 阻塞Davidson方案 [25–28]，以及
- the residual minimization scheme with direct inversion in iterative subspace (RMM-DIIS) [15, 22, 29].
- 迭代子空间中直接反演的残差最小化方案（RMM-DIIS）[15, 22, 29]。

Though reviews of commonly used iterative methods can be found in Refs [15, 22].
尽管关于常用迭代方法的综述可以在Refs [15, 22]中找到。

The expansion set is built iteratively so that the eigenvectors and eigenvalues in the expansion space are the best approximations of the eigenvectors and eigenvalues in the full space. One usually distinguishes the blocked algorithms that work on many bands at the same time from the unblocked algorithms that optimize each band sequentially. In either case, the key step is to compute the vectors that are added to the expansion set to ensure that the lowest eigenfunctions of the expansion set converge to the actual eigenvalues. Let us denote by \(|\hat{\phi}_p\rangle\) the approximation of the eigenvector \(|\phi_p\rangle\). A central quantity of most iterative schemes is the residual vector \(|R(\hat{\phi}_p)\rangle\):
扩展集是迭代构建的，使得扩展空间中的特征向量和特征值是全空间中特征向量和特征值的最佳近似。通常将同时处理多个能带的阻塞算法与按顺序优化每个能带的非阻塞算法区分开来。无论哪种情况，关键步骤都是计算添加到扩展集中的向量，以确保扩展集中的最低特征函数收敛到实际特征值。让我们用 \(|\hat{\phi}_p\rangle\) 表示特征向量 \(|\phi_p\rangle\) 的近似。大多数迭代方案的一个核心量是残差向量 \(|R(\hat{\phi}_p)\rangle\)：

\(|R(\hat{\phi}_p)\rangle = (H - \epsilon_{scp} S)|\hat{\phi}_p\rangle,\)

