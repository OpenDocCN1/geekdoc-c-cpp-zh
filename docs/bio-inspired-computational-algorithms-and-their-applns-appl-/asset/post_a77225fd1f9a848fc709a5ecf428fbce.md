
![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_108_0.png)

Fig. 10. Convergence process of SDGA without the noise from the competing BBs.

one-max problems with orders 4 and 5 are longer than those of SGA because SGA is strongly premature for the long binary string and small population sizes.

As in Table 1 described, for one-max and deceptive trap problems, all GAs converge to sidewise of the optima, which are overrepresented by BBs. But SGA with different binary representation cannot explore the optima of the problems. The ability of SDGA to explore optima, which are overrepresented by BBs, is significantly better than SGA. To explore the global optimum of the deceptive trap problems, we need use other niche methods to divide the whole population into some sub-populations. In each subpopulation, the global optimum is overrepresented by BBs, thus SDGA can efficiently explore this global optimum of the deceptive trap problems.

## 5.3 Avoid the noise from the competing BBs

To validate the predictions about avoiding the noise from the competing BBs, We have implemented our SDGA to solve 30 dimensional integer one-max problem of order 3. We have counted the number of generations it takes before each of bits fully converges. Results are averaged over 50 independent runs. Figure 10 shows the bits convergence for a string of length l = 90, and the population sizes are 20, 100, 200, 300 respectively. The experimental results are summarized in Table 2. The run duration of each USBB_i, (i = 1,2,3) is an average of the fully converged generations of the bits, which belong to the USBB_i.

As shown in Figure 10 and Table 2, the whole S/D binary string includes three USBBs. In each USBB, the bits converge uniformly at almost same generations. For a non-uniform scaled sequence of USBBs, the domino convergence occurs sequentially from high scaled to low scaled USBBs. Thus, no less salient bit converges with more salient bit at same generations and no noise from the competing BBs occurs.

On the other hand, we know the noise from the competing BBs strongly occurs when GAs using a small population size. In our implementations, when the population size of SDGA is small to 20, the convergence process of bits is as same as SDGA using large population size. The low scaled USBBs converge during long generations by SDGA and no noise from the competing BBs occurs.

It is clear from Figure 10 and Table 2 that the predictions and the experimental results coincide very well.

| population size | run duration of USBB₁ | run duration of USBB₂ | run duration of USBB₃ |
|---|---|---|---|
| 20 | 47.3(8.2) | 193.7(12.7) | 365.6(13.8) |
| 100 | 116.6(6.8) | 263.2(7.8) | 470.8(12.1) |
| 200 | 167.4(7.7) | 366.5(6.7) | 559.6(13.9) |
| 300 | 220.3(7.0) | 430.8(6.6) | 633.6(7.8) |

Table 2. Comparison of the run durations of USBBs fully converged with different population sizes.(Standard Deviation)

## 5.4 SDGA with the mutation operator

In this subsection we have considered the action of the mutation operator for SDGA searching. We have implemented our SDGA with different mutation probabilities to solve 30 dimensional integer one-max problem of order 3. Results are averaged over 50 independent runs. Figure 11 presents the experimental results where mutation probabilities are 0.001, 0.005, 0.01, 0.05 and 0.1 respectively. The plots show for SDGA the run duration — fully converged generations with respect to the population size N.

As shown in Figure 11, when the mutation probabilities are smaller than 0.01, SDGA can fully converge with small and large population sizes and the run durations do not increase too long. When the mutation probabilities increase larger than 0.01, SDGA with large population sizes are difficult to fully converge, and only when using small population sizes, SDGA can fully converge, but the run durations increase significantly.

Table 3 summarizes the experimental results with population sizes 20, 40 and 60. For small population sizes (20 and 40), the mutation operators can improve the performance of SDGA, because it can find some high-quality bits, which are not included in current population. For large population sizes (≥ 60), all high-quality bits are included in the initial population, so mutation operator cannot improve the best fitness when SDGA fully converged. Furthermore, when the mutation probability is larger than 0.01, SDGA cannot fully converge in a reasonable time (here we set the upper bound of the run duration equal to 10^6 generations).

## 5.5 Genotypic distance on the S/D binary representation

To validate the predictions about the methods dependent on the distance of real-valued space, can be directly used on the S/D binary space based on our new defined genotypic distance, we have combined SGA with the S/D binary encoding and the dynamic niche sharing methods

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_112_0.png)

Fig. 13. Comparison of results of the dynamic niche sharing methods with S/D genotypic distance and Hamming distance for $f_4(x)$. (key: “o” − the optima in the final population)

genotypic distance can explore all optima in $f_3(x)-f_6(x)$ at each run. Contrary, for the niche methods with Hamming distance, the final population converged to a single optimum of the multimodal problem and cannot find multiply optima. That means the niche method cannot work due to the distance distortion between genotypic space (S/D binary space) and phenotypic space (real-valued space) when using Hamming distance.

The experimental investigations reveal that the methods dependent on the Euclidean distance on the real-valued space can be directly used on the S/D binary space with our new defined genotypic distance.

| | Distance threshold | S/D genotypic distance Optima No. | S/D genotypic distance Success rate | Hamming distance Optima No. | Hamming distance Success rate |
|---|---|---|---|---|---|
| $f_3$ | 2.0 | 2 | 100% | 1 | 0% |
| $f_4$ | 0.16 | 5 | 100% | 1 | 0% |
| $f_5$ | 0.16 | 5 | 100% | 1 | 0% |
| $f_6$ | 0.8 | 6 | 100% | 1 | 0% |

Table 5. Comparison of results of the dynamic niche sharing methods with the S/D genotypic distance and Hamming distance.

## 6. Discussion

This paper has given for the first time a uniform-salient building block (USBB) in the S/D binary representation, which includes uniformly scaled bits. This assumes that the phenotypic space $\Phi_p$ is uniformly scaled in each dimension. If the assumption is not satisfied, we need to normalize the phenotypic space $\Phi_p$ first, then encoding the normalized phenotypic space $\Phi'_p$ into the S/D binary space $\Phi_g$ to guarantee that the bits in each USBB have same scale.

SDGA applies on the S/D binary representation and converges from high scaled to low scaled USBBs sequentially. However, when the convergence window USBB cannot converge to single high-quality BB, there are maybe some high-quality BBs existing to describe different optima of the problem. At this time, we need to use some other methods (e.g., the niche methods) to divide the whole population into several sub-populations and each sub-population focus on each optimum. Thus, each optimum will be overrepresented by

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_113_0.png)

Fig. 14. Comparison of results of the dynamic niche sharing methods with S/D genotypic distance and Hamming distance for f5(x). (key: "o" — the optima in the final population)

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_113_1.png)

Fig. 15. Comparison of results of the dynamic niche sharing methods with S/D genotypic distance and Hamming distance for f6(x). (key: "o" — the optima in the final population)

BBs in its sub-population and SDGA can efficiently explore all the optima using these sub-populations.

## 7. Conclusions

In this paper, we introduce a new genetic representation — a splicing/decomposable (S/D) binary encoding, which was proposed based on some theoretical guidance and existing recommendations for designing efficient genetic representations. The S/D binary representation can be spliced and decomposed to describe potential solutions of the problem with different precisions by different number of uniform-salient building blocks (USBs). According to the characteristics of the S/D binary representation, genetic and evolutionary algorithms (GEAs) can be applied from the high scaled to the low scaled BBs sequentially to avoid the noise from the competing BBs and improve GEAs' performance. Our theoretical and empirical investigations reveal that the S/D binary representation is more proper than other existing binary encodings for GEAs searching. Moreover, we define a new genotypic distance on the S/D binary space, which is equivalent to the Euclidean distance on the real-valued space during GEAs convergence. Based on the new genotypic distance, GEAs can reliably
