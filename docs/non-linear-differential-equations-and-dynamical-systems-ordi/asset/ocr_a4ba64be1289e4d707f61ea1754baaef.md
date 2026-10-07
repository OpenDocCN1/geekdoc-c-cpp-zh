# 4.7.6 Dynamo with Driving Torque Balancing the Joule Dissipation

In the presence of a driving torque the equation (4.347d) for the angular velocity becomes (4.361a):

$$I\dot{\Omega}=M\pm\frac{aZ}{2\pi}\Omega J;\qquad M\Omega=RJ^{2}.\qquad(4.361a,\ b)$$

For a steady motion, the work performed by the driving torque should balance electrical dissipation by the Joule effect (4.361b). For a general driving torque, elimination between (4.361a) and (4.344b), as in (4.354), leads to:

$$\frac{d}{dt}\left(\frac{1}{J}\frac{dJ}{dt}\right)=\pm\frac{Z}{2\pi L}\frac{d\Omega}{dt}=\pm\frac{Z}{2\pi L}\left(\pm\frac{a}{2\pi l}\Omega J+\frac{M}{I}\right)=\pm\frac{aZ}{2\pi I L}\left(L\frac{dJ}{dt}+RJ+\frac{M}{a}\right),$$

(4.362)

that has an extra term compared with (4.354). Thus the driving torque modifies the differential equation, specifying the variation with time of the electric current of the electromechanical homopolar dynamo from (4.354) ≡ (4.355a, b) to (4.362) ≡ (4.363):

$$\ddot{J}-\left(\frac{\dot{J}}{J}\pm bJ\right)\dot{J}\mp bJ\left(\frac{R}{L}J+\frac{M}{aL}\right)=0.$$

(4.363)

The solution of (4.363) depends on the relation $M(\Omega,J)$ between the driving torque, angular velocity, and electric current; if the driving torque is constant the last term in (4.363) includes a linear amplification (oscillation) for the upper $-$ (lower $+$) sign. The simplest case is the driving torque (4.361b) balancing the torque due to the Lorentz force in (4.361a), leading to steady rotation (4.364a); the latter implies by (4.361b) a steady electric current (4.364b). In this case (4.344a) specifies the constant angular velocity (4.364c):

$$\dot{\Omega}=0:\qquad \dot{J}=0,\quad \Omega=\pm\frac{2\pi R}{Z};\quad J=\frac{M\Omega}{RJ}=\mp\frac{aZ\Omega^{2}}{2\pi R}=\mp\frac{2\pi aR}{Z},$$

(4.364a–d)

then (4.361b) specifies the steady electric current (4.364d) from (4.361a). Thus an electromechanical homopolar dynamo (Figure 4.16) with total induction $L$, resistance $R$, and mutual induction $Z$, rotating at constant angular velocity $\Omega$ in (4.344a) acts (problem 122) as a brake (4.345a–c) if the winding is opposite to the direction of rotation ($J_{-}$ in the Figure 4.16); if (problem 123) the winding is in the direction of rotation, the current is constant (4.346b) ≡ (4.364b) for the angular velocity $|\Omega|$ in (4.364c), and decreases (increases) exponentially with time (4.346a) [(4.346c)] for smaller $\Omega<|\overline{\Omega}|$ (larger $\Omega>|\overline{\Omega}|$) values. Taking into account the retarding torque