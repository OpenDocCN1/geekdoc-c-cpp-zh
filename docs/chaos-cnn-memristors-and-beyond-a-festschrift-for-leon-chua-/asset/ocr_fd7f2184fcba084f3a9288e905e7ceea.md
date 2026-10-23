# 5.3. Experimental results

will change to periodic motion in both van der Pol oscillators, which are now uncoupled. To avoid this scenario and maintain chaotic motion for anti-phase synchronization, the external periodic excitation (9) is applied to the coupling bar.

The anti-phase synchronized motion in the chaotic oscillators is achieved by considering controller (29) with e = (x_m + x_s), ė = (ẋ_m + ẋ_s), and η(·) chosen as

```
η(·) = ba(x_s² ẋ_s + x_m² ẋ_m − ẋ_h (x_s² + x_1²)) − 2k x_h + 2b ẋ_h. (31)
```

As before, the control gains in (25) are chosen according to k_v > b and k_p > 0.

The synchronized chaotic motion of two van der Pol oscillators is validated by means of experiments. System (27) is implemented in the experimental setup with the following parameter values: b = 18.3135 [Ns/m], b_h = 3.2656 [Ns/m], k = 6.315 [N/m], k_h = 388.71 [N/m], a = 55·10^5 [1/m²], m = 4.210 [kg], and m_h = 5 [kg].

In a first experiment, the oscillators are synchronized in-phase by applying to one of them the control input (29)–(30) with k_p = 25 [N/m] and k_v = (b + 10) [Ns/m]. The controller is activated at t = 20 [s]. The oscillators are released from the initial conditions x_m(0) = 1 [mm] and x_s(0) = −1.5 [mm]. The remaining initial conditions are set to zero.

The obtained experimental results are presented in Fig. 7. When the controller is off, the chaotic trajectories of the oscillators are not synchronized and consequently the error e = (x_s − x_m) is large, but once the controller is activated, this error becomes practically zero as depicted in Figs. 7(a) and 7(c). Although theoretically this error should asymptotically converge to zero, in practice the error signal keeps showing small vibrations caused by measurement noise and (slight) differences in the oscillators. The control effort is depicted in Fig. 7(d).

Next, the experiment is repeated, but now control law (29) with (31) is applied because it is desired to synchronize the oscillators in anti-phase. To better illustrate the influence of the control law, the controller is now switched on at t = 115 [s]. As can be seen from Fig. 8, when the control action is not active, the system behaves chaotically

![](bbox=[0.24, 0.095, 0.76, 0.37])

Fig. 7. In this experiment, two van der Pol oscillators with Huygens’ coupling synchronize in-phase.

![](bbox=[0.54, 0.77, 0.9, 0.92])

Fig. 8. Although the oscillators synchronize in anti-phase, the chaotic behaviour disappears.