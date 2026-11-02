| population size | run duration of USBB₁ | run duration of USBB₂ | run duration of USBB₃ |
|---|---|---|---|
| 20 | 47.3(8.2) | 193.7(12.7) | 365.6(13.8) |
| 100 | 116.6(6.8) | 263.2(7.8) | 470.8(12.1) |
| 200 | 167.4(7.7) | 366.5(6.7) | 559.6(13.9) |
| 300 | 220.3(7.0) | 430.8(6.6) | 633.6(7.8) |

Table 2. Comparison of the run durations of USBBs fully converged with different population sizes.(Standard Deviation)

USB Bs. Thus, no less salient bit converges with more salient bit at same generations and no noise from the competing BBs occurs.

On the other hand, we know the noise from the competing BBs strongly occurs when GAs using a small population size. In our implementations, when the population size of SDGA is small to 20, the convergence process of bits is as same as SDGA using large population size. The low scaled USBBs converge during long generations by SDGA and no noise from the competing BBs occurs.

It is clear form Figure 10 and Table 2 that the predictions and the experimental results coincide very well.

# 5.4 SDGA with the mutation operator

In this subsection we have consider the action of the mutation operator for SDGA searching. We have implemented our SDGA with different mutation probabilities to solve 30 dimensional integer one-max problem of order 3. Results are averaged over 50 independent runs. Figure 11 presents the experimental results where mutation probabilities are 0.001, 0.005, 0.01, 0.05 and 0.1 respectively. The plots show for SDGA the run duration — fully converged generations with respect to the population size N.

As shown in Figure 11, when the mutation probabilities are smaller than 0.01, SDGA can fully converge with small and large population sizes and the run durations do not increase too long. When the mutation probabilities increase larger than 0.01, SDGA with large population sizes are difficult to fully converge, and only when using small population sizes, SDGA can fully converge, but the run durations increase significantly.

Table 3 summaries the experimental results with population sizes 20, 40 and 60. For small population sizes (20 and 40), the mutation operators can improve the performance of SDGA, because it can find some high-quality bits, which are not included in current population. For large population sizes (≥ 60), all high-quality bits are included in the initial population, so mutation operator cannot improve the best fitness when SDGA fully converged. Furthermore, when the mutation probability is large than 0.01, SDGA cannot fully converge in a reasonable time (here we set the upper bound of the run duration equal to 10^6 generations).

# 5.5 Genotypic distance on the S/D binary representation

To validate the predictions about the methods depended on the distance of real-valued space, can be directly used on the S/D binary space based on our new defined genotypic distance, we have combined SGA with the S/D binary encoding and the dynamic niche sharing methods