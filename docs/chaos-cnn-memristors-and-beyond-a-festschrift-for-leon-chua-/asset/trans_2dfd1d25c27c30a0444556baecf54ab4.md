

Fig. 6. 反相同步在具有 Huygens 耦合的两个混沌 Duffing 振荡器中实现。

这组方程描述了一对具有 Huygens 耦合的 van der Pol 振荡器。已发现该系统在某些参数值下表现出混沌行为。与之前讨论的 Duffing 振荡器情况类似，m/m_h 比值是混沌行为出现时的关键参数。需要注意的是，现在耦合杆不再被驱动。

同样，在混沌区域内，只要对其中一个振荡器施加控制作用，耦合的 van der Pol 振荡器也可能表现出同步行为。接下来讨论反相同步和同相同步的特殊情况。

## 5.1. Case A: in-phase synchronization

通过定义如 (10) 的同相同步误差，系统 (27) 的相应误差动力学可写为

```
ë = 1/m [bė - ba(x_s² ẋ_s - x_m² ẋ_m - ẋ_h (x_s² - x_m²)) - k e + u_s]. (28)
```

为了在混沌振荡器中实现同相同步运动，可考虑以下控制器

```
u_s = -k_p e - k_v ė + η, (29)
```

其中 k_p > 0 且 k_v > 0 且 η 可选为

```
η = ba(x_s² ẋ_s - x_m² ẋ_m - ẋ_h (x_s² - x_m²)). (30)
```

遵循 Proposition 27.1 中使用的方法，可以证明控制器 (29)–(30) 对系统 (28) 产生全局渐近稳定，即耦合振荡器渐近同相同步，前提是 k_v > b 且 k_p > 0。

## 5.2. Case B: anti-phase synchronization

如果具有 Huygens 耦合的两个 van der Pol 振荡器表现出同相同步的混沌行为，耦合杆将会振动。然而，当在振荡器中诱导出反相同步时，耦合杆中的振荡会消失，即 x_h → 0 且耦合杆静止，如原始 Huygens 系统中那样，参见 (27) 中的第三个方程。因此，如果实现反相，则原本混沌的运动

将转变为两个现在解耦的 van der Pol 振荡器中的周期运动。为了避免这种情况并在反相同步下保持混沌运动，外部周期激励 (9) 被施加到耦合杆上。

混沌振荡器中的反相同步运动是通过考虑控制器 (29) 实现的，其中 e = (x_m + x_s)，ė = (ẋ_m + ẋ_s)，且 η(·) 选择为

```
η(·) = ba(x_s² ẋ_s + x_m² ẋ_m − ẋ_h (x_s² + x_m²)) − 2k x_h + 2b ẋ_h. (31)
```

与之前一样，(25) 中的控制增益根据 k_v > b 且 k_p > 0 选择。

两个 van der Pol 振荡器的同步混沌运动是通过实验验证的。系统 (27) 在实验装置中实现，采用以下参数值：b = 18.3135 [Ns/m]，b_h = 3.2656 [Ns/m]，k = 6.315 [N/m]，k_h = 388.71 [N/m]，a = 55·10^5 [1/m²]，m = 4.210 [kg]，且 m_h = 5 [kg]。

在第一个实验中，通过对其中一个振荡器施加控制输入 (29)–(30)，其中 k_p = 25 [N/m] 且 k_v = (b + 10) [Ns/m]，使振荡器同相同步。控制器在 t = 20 [s] 时激活。振荡器从初始条件 x_m(0) = 1 [mm] 和 x_s(0) = −1.5 [mm] 释放。剩余的初始条件设为零。

获得的实验结果在 Fig. 7 中呈现。当控制器关闭时，振荡器的混沌轨迹不同步，因此误差 e = (x_s − x_m) 很大，但一旦控制器激活，该误差变得几乎为零，如图 7(a) 和 7(c) 所示。虽然理论上该误差应渐近收敛到零，但在实践中误差信号仍显示出由测量噪声和振荡器之间的（轻微）差异引起的微小振动。控制作用如图 7(d) 所示。

接下来重复实验，但现在应用控制律 (29) 与 (31)，因为希望使振荡器反相同步。为了更好地说明控制律的影响，控制器现在在 t = 115 [s] 时切换开启。如图 8 所示，当控制作用未激活时，系统表现出混沌行为

![](img/039e7d3c23390584a66737067db8b75b_361_0.png)

Fig. 7. 在此实验中，具有 Huygens 耦合的两个 van der Pol 振荡器同相同步。

![](img/039e7d3c23390584a66737067db8b75b_361_1.png)

Fig. 8. 尽管振荡器反相同步，但混沌行为消失了。

## 5.3. Experimental results

![](img/039e7d3c23390584a66737067db8b75b_363_0.png)

Fig. 10. 在此实验结果中，通过使用控制器 (32) 在系统 (6)–(8) 中诱导同相同步。

实验结果表明，在某些情况下，使用 (32) 时，振荡器可能会（渐近）同步，而在其他情况下会出现所谓的实际同步。其稳定性证明被证明是复杂的，但解决这个问题也值得，因为实验结果和计算机模拟表明控制作用很小。这有几个（有益的）含义。首先，执行器出现饱和效应的概率大大降低。其次，小的控制信号导致低能量消耗。为了说明起见，给出了对应于系统 (6)–(8) 且参数值如第 4.3 节所述并使用控制器 (32)，其中 $k_p=1.2$ 且 $k_v=0.5$ 的实验结果，如图 10 所示。

## 7. Conclusions and Recommendations

在这项工作中，已表明两个 Duffing 和两个具有 Huygens 耦合的 van der Pol 振荡器可能经历混沌行为。对于 Duffing 振荡器的情况，耦合杆必须由周期力驱动。耦合强度——或者更确切地说耦合杆的质量——被视为分岔参数，对于 Duffing 振荡器的情况，发现了一系列导致最终混沌状态的倍周期分岔。在混沌区域内，对于 Duffing 振荡器以及 van der Pol 振荡器，振荡器不会自发同步。这并不令人惊讶，因为尽管振荡器是相同的，但对初始条件极其敏感。因此，对其中一个振荡器，即从属振荡器，添加了控制器以诱导混沌运动的同相或反相同步。该原理已通过实验验证。当 Huygens 耦合用于耦合两个任意振荡器时，自发同步的发生（与 Huygens 相同）取决于振荡器是否具有混沌解。

出于第 6 节中提到的原因，有趣的是对使用简单控制器 (32) 时的（同相和/或反相）同步误差动力学进行稳定性分析。

最后，值得一提的是，Huygens 系统是一个令人兴奋且具有挑战性的非线性动力系统，其复杂动力学行为远未被完全理解。对该系统的进一步研究将揭示有关复杂而又引人入胜的同步现象的更多细节。

## References

- [1] Afraimovich, V. S., Verichev, N. N. and Rabinovich, M. I. (1986). Stochastic synchronization of oscillation in dissipative systems, *Radiophysics and Quantum Electronics* **29**, 9, pp. 795–803.
- [2] Bennett, M., Schatz, M. F., Rockwood, H. and Wiesenfeld, K. (2002). Huygens’ clocks, *Proceedings of the Royal Society of London A: Mathematical, Physical and Engineering Sciences* **458**, 2019, pp. 563–579.
- [3] Blekhman, I. I., Fradkov, A. L., Nijmeijer, H. and Pogromsky, A. Yu. (1997). On self-synchronization and controlled synchronization, *Systems and Control Letters* **31**, pp. 299–305.
- [4] Boccaletti, S., Kurths, J., Osipov, G., Valladares, D. L. and Zhou, C. S. (2002). The synchronization of chaotic systems, *Physics Reports* **366**, 1–2, pp. 1–101.
- [5] Chen, G. and Dong, X. (1993). On feedback control of chaotic continuous-time systems, *IEEE Transactions on Circuits and Systems I: Fundamental Theory and Applications* **40**, 9, pp. 591–601.
- [6] Fujisaka, H. and Yamada, T. (1983). Stability theory of synchronized motion in coupled-oscillator systems, *Progress of Theoretical Physics* **69**, 1, pp. 32–37.
- [7] Huygens, C. (1660). In M. Nijhoff (ed.), *Oeuvres completes de Christiaan Huygens*, Vol. 17, pp. 156–189.
- [8] Khalil, H. (2002). *Nonlinear Systems*, 3rd edn. (Prentice Hall, New Jersey).
- [9] Kim, J. R., Shin, D., Jung, S. H., Heslop-Harrison, P. and Cho, K. H. (2010). A design principle underlying the synchronization of oscillations in cellular systems, *Journal of Cell Science* **123**, 4, pp. 537–543.

