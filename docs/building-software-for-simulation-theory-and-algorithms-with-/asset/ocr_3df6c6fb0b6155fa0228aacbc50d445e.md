**TABLE 2.2** Parameters of the Motors, Gearbox, and Tracks

| Parameter | Value | Description |
|---|---|---|
| $L_m$ | 10⁻³ H | Inductance of the motor |
| $R_m$ | 3.1 Ω | Resistance of the motor |
| $J_g$ | 1.2 × 10⁻⁶ kg·m² | Angular mass of the gears |
| $B_g$ | 6.7 × 10⁻³ N·m·s/rad | Mechanical resistance of the gears to rotation |
| $g$ | 204 | Gear ratio of the gearbox |
| α | 10⁻³ N·m/A | Current-torque ratio of the electric motor |
| $r$ | 0.015 m | Radius of the sprocket wheel |
| $K_t$ | 10⁻³ m/N | Compliance of the track |

equations are read directly from the bond graph:

$$
\dot i_l = \frac{1}{L_m}(e_l - i_l R_m - \alpha \omega_l) \tag{2.11}
$$

$$
\dot \omega_l = \frac{1}{J_g}\left(\alpha i_l - \omega_l B_g - \frac{r}{g}F_l\right) \tag{2.12}
$$

$$
\dot F_l = \frac{1}{K_t}\left(\frac{r}{g}\omega_l - v_l\right) \tag{2.13}
$$

$$
\dot i_r = \frac{1}{L_m}(e_r - i_r R_m - \alpha \omega_r) \tag{2.14}
$$

$$
\dot \omega_r = \frac{1}{J_g}\left(\alpha i_r - \omega_r B_g - \frac{r}{g}F_r\right) \tag{2.15}
$$

$$
\dot F_r = \frac{1}{K_t}\left(\frac{r}{g}\omega_r - v_r\right) \tag{2.16}
$$

where $e_l$ and $e_r$ are the motor voltages and $v_l$ and $v_r$ are the track speeds given by Equations 2.8 and 2.9.

Values for the parameters in Table 2.2 were obtained from manufacturers’ data, from measurements, and by educated guesses. The gear ratio $g$ and current-torque ratio $\alpha$ are provided by the manufacturers. The gear ratio is accurate and precise (especially with respect to the values of other parameters in the model). The current-torque ratio is an average of the two cases supplied by Mabuchi, the motor’s manufacturer. The first case is the motor operating at peak efficiency, and the second case is the motor stalling. The difference between these two cases is small, suggesting that $\alpha$ does not vary substantially as the load on the motor changes. The estimate of $\alpha$ is, therefore, probably very reasonable.

The radius $r$ of the sprocket wheel and the resistance $R_m$ and inductance $L_m$ of the motor were measured directly. A ruler was used to measure the radius of the sprocket wheel. To determine $R_m$ and $L_m$ required more effort. The current $i$ through