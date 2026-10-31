around a infinitely long rotating cylinder which is then transformed together with its surrounding airflow into the shape of an airfoil by a conformal mapping.106

Spinning objects moving through air, such as golf balls or rotating cylinders, experience a force which is due to the effect of their rotation in conjunction with the surrounding medium. This is known as MAGNUS effect after HEINRICH GUSTAV MAGNUS, a German physicist who gave the first comprehensible explanation of this phenomenon. The airflow around a rotating cylinder will be simulated below using the following assumptions:

+   - The cylinder with circular cross section is infinitely long.
+   - The airflow is always perpendicular to the cylinder axis. Furthermore, it is stationary and conservative, i.e.
+   
+     v dot = 0 and A dot = 0
+   
+     with v and A denoting the velocity and area of the airflow.
+   - The air is assumed to be incompressible and frictionless.

This airflow is a potential flow and its velocity field can thus be described as the gradient of some complex function f(z) called velocity potential. The function

f(z) = v0 ( z e^{i varphi} + r^2 e^{-i varphi} / z ) - i Gamma / (2 pi) log(z)

will be used in this example. Here r denotes the radius of the cylinder around which the air flows. v0 is the initial velocity of the air flow, varphi the angle of attack, and Gamma the circulatory component.

First of all a circuit is needed to generate the circumference of the rotating cylinder, i.e. a circle, is needed. This is implemented like before by solving the classic differential equation y double dot = -y as shown in figure 4.11 in section 4.2. The radius is set to about 0.4 by means of the parameter alpha*, which controls the negative feedback, and the initial condition a of the first integrator. Both of these must match to avoid artefacts at the start of a simulation run. As before, the coefficient alpha provides a very small positive feedback. It can be omitted, if the radius does not decrease during a prolonged run. If it required, it should be set to about 0.005, otherwise the sine/cosine signals will be distorted. The time scale factors of the two integrators should be set at least to k0 = 10^3.

The program for the complex velocity potential is rather more complicated and is shown in figure 6.63. This circuit expects three parameters/input values: