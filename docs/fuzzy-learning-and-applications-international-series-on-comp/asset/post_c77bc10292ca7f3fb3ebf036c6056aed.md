
![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_301_0.png)

Figure 9.8 Membership functions and consequents of the optimized fuzzy controller

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_301_1.png)

Figure 9.9 Comparison between classical and fuzzy PD regulators

## 9.6 The indirect optimization strategy

In this section a different optimization strategy is used to design the fuzzy controller for the focusing system. More specifically a 2-step optimization strategy is adopted. The first step uses a genetic optimization strategy to derive a fuzzy controller which approximates the classical PD. The classical PD controller described in Section 4 was discretized as follows:

y(k) = a e(k) + b de(k) (9.6)

where y is the controller output, e is the error signal (difference between the reference and the output of the system) and de is the error derivative. The controller output was then computed for a number of (e, de) values and the patterns obtained were used as training patterns for a neuro-fuzzy network. At the end of the training a set of fuzzy rules which interpolates the classical PD controller is obtained (FC1). The FC1 rules do not introduce any improvement with respect to the classical PD. The FC1 rules were then used as a starting point for a second optimization phase, i.e., the initial population for a GA was built allowing a variation of 10% around the membership function and the consequents of the FC1 rules. A GA was therefore used to minimize the quadratic performance index used in the direct approach. Finally, a set of optimized fuzzy rules representing the fuzzy controller was obtained (FC2).

### 9.6.1 Approximation of the classical controller by a set of fuzzy rules

In order to perform the desired approximation, the classical controller is simulated using a white noise as input. The simulation allows us to obtain the set of I/O values which can be used to identify the fuzzy model of the controller. After a trial and error phase, five fuzzy sets were chosen for each of the input variables. Both the membership functions and the consequences were maintained symmetrical with respect to the origin. The number of fuzzy sets and rules was selected a priori and a genetic algorithm was used to train the neurofuzzy network to minimize the quadratic error between the target and the output of the fuzzy controller on the whole set of learning patterns. The genetic algorithm parameters were fixed as follows:

- population size: 40;
- number of generations: 60;
- range of the error variable: [−0.01, 0];
- range of the error derivative variable: [−0.001, 0];
- range of the consequents: [−0.03, 0]

The fuzzy rules obtained are given in Fig. 9.10.

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_303_0.png)

Figure 9.10 Fuzzy rules which approximate the classical PD controller

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_303_1.png)

Figure 9.11 Fitness function trend

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_304_0.png)

Figure 9.12 Comparison of the behaviour of the controllers with a band-limited white noise. The dashed line is the fuzzy controller

Fig. 9.11 shows the fitness function values versus the number of generations.

The performance of the fuzzy controller can be illustrated by Figs. 9.12 and 9.13 where the system responses with the fuzzy and classical controllers are compared, with band-limited white noise and a step function disturbance. As can be observed, the performance of the controllers is quite similar, even if the classical controller gives again better performance.

### 9.6.2 Optimization of the fuzzy controller

Starting from the previously determined fuzzy controller, a 10% variation was considered for each parameter of the controller and a genetic algorithm was used, as in direct optimization. The fitness function and the genetic algorithm parameters were fixed as in Section 5. The performance of the optimized fuzzy controller is shown in Figs. 9.14, 9.15 and 9.16.

Similar results were obtained for the whole set of disturbances. Performance analysis indicates the great improvement introduced by the fuzzy PD controller. A detailed explanation of the reasons which allow to obtain a performance improvement with a fuzzy controller is given in the following section.

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_305_0.png)

Figure 9.13 Comparison of the behaviour of the controllers with a step noise (dashed line = optimized)

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_305_1.png)

Figure 9.14 Comparison of the behaviour of the controllers with a step disturbance (dashed line = optimized)

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_306_0.png)

Figure 9.15 Comparison of the behaviour of the controllers with a step disturbance (dashed line = optimized)

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_306_1.png)

Figure 9.16 Comparison of the behaviour of the controllers with a step disturbance (dashed line = optimized)

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_308_0.png)

Figure 9.18 Fuzzy controller output surface

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_308_1.png)

Figure 9.19 Level curves of the classical controller output: output versus the error derivative

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_310_0.png)

Figure 9.22 Level curves of the fuzzy controller output: output versus the error

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_310_1.png)

Figure 9.23 The partitioned values of Kp

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_311_0.png)

Figure 9.24 The partitioned values of Kd

## 9.8 Implementation details

The designed Fuzzy controller was implemented using an ST52 microcontroller manufactured by STMicroelectronics and was tested on the Philips ROM65200 CD-ROM system. ST52 is a microcontroller that executes Boolean and fuzzy algorithms. The versatility of the I/O configuration of this microcontroller allows it to interface with a wide set of external devices such as D/A converters, power control devices (SCR, TRIAC) and external sensors. The ST52 is supported by the software tool Fuzzystudio 3.0 which develops each project graphically and automatically converts it into an optimized microcode. The fundamental component of the chip is the fuzzy core, which consists of four 8-bit input channels, 16 membership functions for each input and two 8-bit outputs.

Fig. 9.25 shows the control algorithm implemented in FuzzyStudio 3.0.

Once the ST52 was programmed the microcontroller was inserted on a small board. The input of the ST52 was connected to the focus system output (focus error) while the output was connected to a suitable driver for the coil of the focus system. A set of measurements was performed validating the controller performance obtained in simulation.

## 9.9 Conclusion

This chapter has described the fuzzy control design of the focus system of a CD player. The fuzzy controller is a classical Sugeno type Fuzzy-PD. The system was tuned in two different ways, based on optimization, by means of a simulator, of the membership function shape and of the consequents. The first method consisted of direct optimization of the controller, using a genetic algorithm to minimize the mean square error of the output. In this case the performance obtained was comparable with that of a classical PD. The second method consisted of two steps. The aim of the first step was to learn the behaviour of a classically-designed linear controller, using a fuzzy controller. Then in the second step the parameters of the fuzzy controller were optimized. In this case the results showed that this controller outperforms the linear one. In particular it was shown that the fuzzy controller is equivalent to a set of several PD controllers. A practical implementation on a real system was performed using a fuzzy microcontroller and the measurements confirmed the results obtained in simulation.
