
matrices in (10.72)-(10.74) can be transformed into field values by multiplying with a matrix that represents the summation of the fields at the appropriate equivalent grid points. In this case,

(10.76) \(\boldsymbol{E_R} = R \boldsymbol{E_W}\)

where \(\boldsymbol{E_R}\) is the reconstructed fields, \(\boldsymbol{E_W}\) is the wavelet coefficients, and \(\boldsymbol{R}\) is the reconstruction matrix. It was previously noted that there are as many independent points that can be reconstructed in \(\boldsymbol{E_R}\) as there are coefficients in \(\boldsymbol{E_W}\). Thus \(\boldsymbol{R}\) is square. For the case of \(r_{max} = 0\), (10.76) can be expanded as

(10.77) \(\begin{bmatrix} \boldsymbol{E}_{1,1} \\ \boldsymbol{E}_{1,2} \\ \boldsymbol{E}_{2,1} \\ \boldsymbol{E}_{2,2} \end{bmatrix} = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & 1 & -1 & -1 \\ 1 & -1 & 1 & -1 \\ 1 & -1 & -1 & 1 \end{bmatrix} \begin{bmatrix} n E_{i,j}^{x,\phi\phi} \\ n E_{i,j}^{x,\psi\psi} \\ n E_{i,j}^{x,\phi\psi} \\ n E_{i,j}^{x,\psi\phi} \end{bmatrix}\)

if the coordinates for the reconstructed fields are given as in Figure 10.15.

### FIGURE 10.15: Coordinates for reconstructed fields.

(Reprinted with permission from [69], copyright © 2005 by Wiley.)

![](img/f73ae67732328dc36596b27ffe8d0152_602_0.png)

Just as R can be used to reconstruct the field coefficients from their scaling/wavelet values, R⁻¹ can be used to decompose the field values to scaling/wavelet coefficients. Thus the application of a PEC boundary condition to an individual equivalent grid point can be accomplished by reconstructing the fields, zeroing the fields tangential to PECs, and then decomposing back to scaling/wavelet coefficients. However, a more efficient method results when the reconstruction/decomposition matrices are applied directly to the MRTD update equations.

By using the reconstruction/decomposition matrices directly on (10.72)–(10.74) a pointwise update equation results. For example, multiplying (10.72) by R, using Hᵢⱼⁿ = R⁻¹RHᵢⱼⁿ, and defining U = RUR⁻¹ yield

(10.78) \( R_n E_{i,j}^n = R_{n-1} E_{i,j}^n + \frac{\Delta t}{\epsilon \Delta y} (U'_{E i_1} R_{n-1} H_{i,j}^n + U'_{E i_2} R_{n-1} H_{i,j-1}^n) \)

which gives the update of the electric field points in terms of the magnetic field points.

Using this equation, it is possible to zero the field points that are tangential to PECs by multiplying with a matrix \( I_p \), which is the identity matrix with zeros in the rows corresponding to PEC locations. As (10.78) is an update equation and the initial values of all fields are 0, multiplying the electric field vectors in (10.78) with \( I_p \) is redundant.

The new update equation with PEC locations zeroed is

(10.79) \( R_n E_{i,j}^x = R_{n-1} E_{i,j}^x + \frac{\Delta t}{\epsilon \Delta y} (I_p U'_{\hat{x}_{i+1}} R_{n-1} H_{i,j}^z + I_p U'_{\hat{x}_{i+2}} R_{n-1} H_{i,j-1}^z) \)

By multiplying (10.79) with \( R^{-1} \) and defining \( U^p = R^{-1} I_p U' R \) the PEC MRTD update equation becomes

(10.80) \( _n E_{i,j}^x = _{n-1} E_{i,j}^x + \frac{\Delta t}{\epsilon \Delta y} (U_{i+1}^p H_{i,j}^z + U_{i+2}^p H_{i,j-1}^p) \)

This equation is the same as (10.72) except for the use of the \( U_p \) matrices. Thus, it is possible to implement subcell PEC modeling in MRTD simply by changing the inner product matrices. This method does not increase computational overhead; it only requires the additional memory to store the U matrices.

## 10.8.5 Examples

### 10.8.5.1 CPW-Microstrip Transition.

The coplanar waveguide (CPW)-microstrip transition is shown in Figure 10.16. The loss of this transition can be optimized over a wide frequency range with the use of FDTD and design curves for various packaging specifications can be derived. The plot in Figure 10.17 shows S21 of this transition for a variety of lengths of the central straight section from 10 to 20 GHz. These data were obtained using time-domain voltage probes at the input (V1) and output (V2) of the transition, converting them to frequency domain through the use of a discrete Fourier transform and identifying the reflected voltage through the use of a reference input voltage (Vref) derived by the simulation of a through CPW line [69]. In addition, the use of the full-wave FDTD, that provides the values of all electromagnetic components throughout the geometry, offers a more intuitive visualization of the circuit. For example, in the transition zone the electric fields have to change smoothly from a coplanar waveguide mode to a microstrip mode, to minimize the local reflections. Thus in the design process it is desirable to identify where this transition takes place and optimize the tapering. Figure 10.16 is a plot of total electric field for a transverse cross-section of the transition. It can be seen that at the position of this cross-section, the field is mostly in a CPW mode, though a microstrip mode has started developing below and at the edges of the signal line there. The relative amplitudes of the E-field could provide an intuitive design rule for the spacing between the CPW ground and signal line, so as not to suppress the microstrip mode.

### FIGURE 10.16: CPW-microstrip transition; E-field distribution.

(Reprinted with permission from [69], copyright © 2005 by Wiley.)

![](img/f73ae67732328dc36596b27ffe8d0152_605_0.png)

### FIGURE 10.17: S21 for various central line widths.

(Reprinted with permission from [69], copyright © 2005 by Wiley.)

![](img/f73ae67732328dc36596b27ffe8d0152_606_0.png)

### 10.8.5.2 Microstrip-Line Coupling.

Embedded transmission lines are commonly used in multilayer packages, where the use of noncontinuous grounds could lead to increased cross-talk effects. The FDTD technique is used to estimate the coupling of finite-ground microstrip lines to Figure 10.18 [69]. The results presented in [69] for different line spacing and for a ground connecting via (optimized design) are obtained by combining two simulations, an even and an odd mode excitation. In addition, to reduce the unwanted cross-talk, the electric and the magnetic field distributions are also calculated. It is shown that most of the coupling is through the magnetic field lines, leading to the design conclusion that attempts to reduce the coupling should focus on magnetic shielding.

### FIGURE 10.18: Embedded finite-ground microstrip lines.

(Reprinted with permission from [69], copyright © 2005 by Wiley.)

![](img/f73ae67732328dc36596b27ffe8d0152_607_0.png)

### 10.8.5.3 MEMS Capacitive Switch.

One example of a MEMS structure that benefits from simulation in MRTD is the MEMS capacitive switch shown in Figure 10.19. The gap between the plates in the switch is 1/175th of the substrate thickness. The simulation of this device in FDTD is tedious and slow because of the large number of cells that must be used to accurately represent the very small gap and substrate.

### FIGURE 10.19: MEMS switch feeding capacitive stub.

(Reprinted with permission from [69], copyright © 2005 by Wiley.)

![](img/f73ae67732328dc36596b27ffe8d0152_608_0.png)

In MRTD, the number of cells can be reduced by using the built-in adaptive gridding capability of the method. In addition, further efficiencies can be obtained in large simulations featuring this structure by allowing fewer cells to be used when the electric field variation near the cell is low.

These examples demonstrate the strength of MRTD in the calculation of the scattering parameters as well as in the estimation of the packaging effects and of the parasitic crosstalk between neighboring geometries. In addition, its inherent capability of global electromagnetic field calculation as well as MRTD’s multi-PEC cell allows for the identification of “hot spots” of high field concentration and for the derivation of physics-driven solutions for the improvement of the overall system-on-package efficiency. The time- and space-adaptive grid of MRTD allows it to be used to model finely detailed structures. Areas of the grid containing small features can use increased resolution,
