Similar regularization techniques based on the Tikhonov regularization have been used to alleviate problems encountered by the linear SRCC formulations in the quasi-degenerate regime [64]. For \(\omega^2 = 0\), the Reg-CCSD(T) approach is identical to the original CCSD(T) formulation. It has been demonstrated that the regularization algorithm, Eq. (14.19), leads to significant improvements of the CCSD(T) results in the geometry regions corresponding to stretched nuclear geometries [63]. It should also be mentioned that the Reg-CCSD(T) and CCSD(T) approaches are characterized by the same numerical overhead proportional to \(n^2 o^4\). As mentioned earlier, the expressions for the Reg-CCSD(T) and CCSD(T) methods have the same algebraic structure. Therefore, the GPU implementation for the noniterative Reg-CCSD(T) methods also provides the GPU implementation for the CCSD(T) approach (\(\omega^2 = 0\)).

# 14.2.2 Multi-Reference Coupled-Cluster Formulations

Many aspects of computational chemistry require methodologies capable of describing a delicate balance between static and dynamic correlation effects for systems and processes belonging to the so-called multi-reference chemistry. The common feature of systems falling into this class of problems is the fact that the corresponding wave functions, in contrast to the closed-shell systems, cannot be described by a single Slater determinant. This situation commonly occurs in bond-breaking processes, poly-radical species, transition-metal compounds, low-spin open-shell states, and reactions involving potential energy surface crossing. To describe these problems, one has to resort to multi-reference methods such as complete active space self-consistent field formalisms, various variants of multi-reference many-body perturbation theory (MRMBPT) methods [65–73] (such as the ubiquitous CASPT2 approach [74]), and multi-reference configuration interaction functions (MRCI) [75], MRCC Methods [76–99], and canonical transformation theory [100].

The dawn of peta-scale computer architectures offers a unique opportunity to validate and apply accurate yet numerically expensive multi-reference theories to large molecular systems. The MRCC method is among the methodologies that can take advantage of this fact. The MRCC formalisms extend the applicability of the SRCC methods to quasi-degenerate situations by replacing the notion of a reference function \(|\Phi\rangle\) used in the SRCC theories by the concept of the model space (\(\mathcal{M}_0\)) spanned (\(l_S\)) by the most important Slater determinants \(|\Phi_\mu\rangle\), \(\mu = 1, \cdots, M\)

```
\(\mathcal{M}_0 = l_S \{|\Phi_\mu\rangle\}_{\mu=1}^{M_0}\) (14.21)
```

required to describe a certain subset of electronic states. In a natural way, the MRCC formalisms lead to partitioning of correlation effects into static (associated with the many-body effects within the model space \(\mathcal{M}_0\)) and dynamic (associated with the many-body effects within the complement of the model space \(\mathcal{M}_0^c\)) effects. These methods thus provide a way to properly treat correlation effects for electronic states characterized by strong correlation effects.

In this chapter, we will focus on the state-specific Hilbert space (HS) formulation of the MRCC theory, where the electronic wave function \(|\Psi\rangle\) is expressed by the Jeziorski–Monkhorst Ansatz [87]

```
\(|\Psi\rangle = \sum_{\mu=1}^M c_\mu e^{T(\mu)} |\Phi_\mu\rangle\) (14.22)
```

where the \(T^{(\mu)}\) are the reference-specific cluster operators. For the complete model space (CMS), which is defined by determinants obtained by all possible distributions of the active electrons among the active spin orbitals, the intermediate normalization condition [87] requires that the cluster operators do not produce any excitations within the model space, that is,

```
\(\langle \Phi_\mu | T^{(\nu)} |\Phi_\mu \rangle = 0 \quad \forall_{\mu \neq \nu}\) (14.23)
```