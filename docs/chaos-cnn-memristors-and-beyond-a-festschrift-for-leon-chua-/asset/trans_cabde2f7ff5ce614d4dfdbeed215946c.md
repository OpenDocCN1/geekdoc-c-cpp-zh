

四元数值的混沌神经元模型及其网络的动力学细节，并进一步将该模型推广到四元数的推广形式，如 Clifford 代数。

## 6. 结论

我们提出了一个混沌神经网络模型及其若干扩展。虽然我们仅以记忆相关动力学作为应用进行了说明，但混沌神经网络模型还有许多其他应用 [40]。特别是组合优化是一个重要的应用。混沌神经网络的优化动力学在数值上 [41, 42] 和数学上 [43–45] 都已得到阐明，并且也开发了实用的算法 [46–49]（参见 Ikeguchi 等 [50] 的最新综述）。混沌神经网络的表述是产生固定点伪吸引子之间传递动力学的一种自然方法。这种传递动力学是通过不应期效应导致固定点吸引子的失稳而实现的，或等价地由混沌神经元特有的自循环抑制连接实现。应注意，传递动力学可能与前额叶皮层中的高级脑功能有关 [51]。

此外，混沌神经网络模型已在电子电路上实现 [52–54]。我们的未来目标是详细分析扩展混沌神经网络的时空动力学，考虑其与脑动力学的关系，并为实际应用实现其电子电路。

## 致谢

本研究部分得到 Aihara 创新数学建模项目、日本学术振兴会（JSPS）通过“科学技术政策委员会（CSTP）发起的世界领先创新研究与开发科学技术资助计划（FIRST Program）”的支持。MO 得到日本学术振兴会 JSPS 特别研究员资助（21-937）的支持。

## 参考文献

- [1] L. O. Chua, C. W. Wu, A. Huang, and G.-Q. Zhong, A universal circuit for studying and generating chaos. I. routes to chaos, IEEE Transactions on Circuits and Systems I: Fundamental Theory and Applications. 40(10), 732–744 (Oct., 1993). ISSN 1057-7122. doi: 10.1109/81.246149.
- [2] L. O. Chua and L. Yang, Cellular neural networks: Theory, IEEE Trans. Circuits Syst. 35(10), 1257–1272, (1988).
- [3] L. Chua, Memristor-the missing circuit element, IEEE Transactions on Circuit Theory. 18(5), 507–519 (Sep., 1971). ISSN 0018-9324. doi: 10.1109/TCT.1971.1083337.
- [4] K. Aihara, T. Takabe, and M. Toyoda, Chaotic neural networks, Physics Letters A. 144, 333–340, (1990).
- [5] K. Aihara, Chaos in neurons, Scholarpedia. 3(5), 1786, (2008). URL http://www.scholarpedia.org/article/Chaos_in_neurons.
- [6] W. S. McCulloch and W. H. Pitts, A logical calculus of the ideas immanent in neural nets, Bulletin of Mathematical Biophysics. 5, 115–133, (1943).
- [7] G. Matsumoto, K. Aihara, M. Ichikawa, and A. Tasaki, Periodic and nonperiodic responses of membrane potentials in squid giant axons during sinusoidal current stimulation, Journal of Theoretical Neurobiology. 3, 1–14, (1984).
- [8] K. Aihara and G. Matsumoto. Chaotic oscillations and bifurcations in squid giant axons. In ed. A. V. Holden, Chaos, pp. 257–269. Manchester and Princeton University Presses, Manchester and Princeton, (1986).
- [9] K. Aihara, T. Numajiri, G. Matsumoto, and M. Kotani, Structures of attractors in periodically forced neural oscillators, Physics Letters A. 116(7), 313–317, (1986). ISSN 0375-9601. doi: 10.1016/0375-9601(86)90578-5.
- [10] G. Matsumoto, K. Aihara, Y. Hanyu, N. Takahashi, S. Yoshizawa, and J. Nagumo, Chaos and phase locking in normal squid axons, Physics Letters A. 123(4), 162–166, (1987). ISSN 0375-9601. doi: 10.1016/0375-9601(87)90696-7.
- [11] A. L. Hodgkin and A. F. Huxley, A quantitative description of membrane current and its application to conduction and excitation in nerve, The Journal of Physiology. 117(4), 500–544, (1952).
- [12] K. Aihara and G. Matsumoto. Forced oscillations and route to chaos in the Hodgkin-Huxley axons and squid giant axons. In eds. A. V. Holden and L. Olsen, Chaos in Biological Systems, pp. 121–131. Plenum Publishing, New York, (1987).
- [13] E. R. Caianiello, Outline of a theory of thought-processes and characteristics of a mathematical neuron model, Kybernetik. 10, 155–164, (1972).
- [15] A. Mees, K. Aihara, M. Adachi, K. Judd, T. Ikeguchi, and G. Matsumoto, Deterministic prediction and chaos in squid axon response, Physics Letters A. 169(1-2), 41–45, (1992). ISSN 0375-9601. doi: 10.1016/0375-9601(92)90802-S.
- [16] K. Aihara. Chaos in axons. In ed. M. Arbib, The Handbook of Brain Theory and Neural Networks, 1st edition, pp. 183–185. The MIT Press, Cambridge, Massachusetts, (1995).
- [17] W. de Melo and S. van Strien, One-Dimensional Dynamics. (Springer-Verlag, 1993).
- [18] R. FitzHugh. Mathematical models of excitation and propagation in nerve. In ed. H. Schwan, Biological Engineering, chapter 1, pp. 1–85. McGraw-Hill, NY, (1969).
- [19] K. Aihara. Chaotic neural networks. In Bifurcation Phenomena in Nonlinear Systems and Theory of Dynamical Systems, vol. 710, RIMS Kokyuroku, pp. 145–163. Kyoto University, (1989).
- [20] M. Adachi and K. Aihara, Associative dynamics in a chaotic neural network, Neural Networks. 10(1), 83–98, (1997). ISSN 0893-6080. doi: 10.1016/S0893-6080(96)00061-5.
- [21] M. Oku, K. Iwayama, K. Tokuda, H. Suzuki, and K. Aihara, Parallel simulation of a large-scale chaotic neural network, IEICE Tech. Rep. 109(269), 55–59 (November, 2009). (in Japanese).
- [22] M. Oku and K. Aihara. Associative dynamics of color images in a chaotic neural network. In Proc. NOLTA'10, pp. 465–468, (2010).
- [23] M. Oku and K. Aihara, Associative dynamics of color images in a large-scale chaotic neural network, NOLTA, IEICE. 2(4), 508–521 (October, 2011). doi: 10.1587/nolta.2.508.
- [24] A. M. Collins and M. R. Quillian, Retrieval time from semantic memory, J. Verb. Learn. Verb. Behav. 8(2), 240–247, (1969). ISSN 0022-5371.
- [25] Y. Miyashita, Cognitive memory: cellular and network machineries and their top-down control., Science. 306(5695), 435–440 (Oct., 2004). doi: 10.1126/science.1101864.
- [26] S. Amari, Learning patterns and pattern sequences by self-organizing nets of threshold elements, IEEE Transactions on Computers. C-21(11), 1197–1206, (1972).
- [27] D. Kleinfeld, Sequential state generation by model neural networks., Proc. Natl. Acad. Sci. U.S.A. 83(24), 9469–9473 (Dec., 1986).
- [28] H. Sompolinsky and I. Kanter, Temporal association in asymmetric neural networks, Phys. Rev. Lett. 57(22), 2861–2864 (Dec., 1986).
- [29] B. Kosko, Bidirectional associative memories, IEEE Trans. Syst. Man Cybern. 18(1), 49–60, (1988).
- [30] M. Oku and K. Aihara. Associative dynamics with structured relations among memories in a chaotic neural network. In Proc. NOLTA'11, pp. 366–369, (2011).
- [31] Y. Osana, M. Hattori, and M. Hagiwara. Chaotic bidirectional associative memory. In Proc. ICNN'96, Vol. 2, pp. 816–821, (1996).
- [32] S. A. Nene, S. K. Nayar, and H. Murase. Columbia Object Image Library (COIL-100). Technical Report CUCS-006-96, Department of Computer Science, Columbia University, (1996).
- [33] Y. Shinohara, T. Kanamaru, H. Suzuki, T. Horita, and K. Aihara, Array-enhanced coherence resonance and forced dynamics in coupled FitzHugh-Nagumo neurons with noise, Phys. Rev. E. 65(5 Pt 1), 051906 (May, 2002).
- [34] N. F. Rulkov, I. Timofeev, and M. Bazhenov, Oscillations in large-scale cortical networks: map-based model, J. Comput. Neurosci. 17(2), 203–223, (2004). doi: 10.1023/B:JCNS.0000037683.55688.7e.
- [35] M. Oku and K. Aihara. Traveling waves in locally connected chaotic neural networks and their phenomenological modeling. In Proc. ICCN'11, (2011). (in press).
- [36] A. Hirose, Ed., Complex Valued Neural Networks — Theories and Applications. (World Scientific, 2003).
- [37] G. M. Georgiou and C. Koutsougeras, Complex domain backpropagation, IEEE Transactions on Circuits and Systems II: Analog and Digital Signal Processing. 39(5), 330–334 (May, 1992). ISSN 1057-7130. doi: 10.1109/82.142037.
- [38] I. Nemoto and K. Saito, A complex-valued version of Nagumo-Sato model of a single neuron and its behavior, Neural Networks. 15(7), 833–853, (2002). ISSN 0893-6080. doi: 10.1016/S0893-6080(02)00066-7.
- [39] G. Tanaka and K. Aihara, Complex-valued multistate associative memory with nonlinear multilevel functions for gray-level image reconstruction, IEEE Transactions on Neural Networks. 20(9), 1463–1473 (Sept., 2009). ISSN 1045-9227. doi: 10.1109/TNN.2009.2025500.
- [40] K. Aihara, Chaos engineering and its application to parallel distributed processing with chaotic neural networks, Proceedings of the IEEE. 90, 919–930, (2002).
- [41] T. Yamada and K. Aihara, Nonlinear neurodynamics and combinatorial optimization in chaotic neural networks, Journal of Intelligent and Fuzzy Systems. 5, 53–68, (1997).
- [42] I. Tokuda, T. Nagashima, and K. Aihara, Global bifurcation structure of chaotic neural networks and its application to traveling salesman problems, Neural Networks. 10(9), 1673–1690, (1997). ISSN 0893-6080. doi: 10.1016/S0893-6080(97)00023-3.
- [43] L. Chen and K. Aihara, Chaos and asymptotical stability in discrete-time neural networks, Physica D: Nonlinear Phenomena. 104(3-4), 286–325, (1997). ISSN 0167-2789. doi: 10.1016/S0167-2789(96)00302-8.

