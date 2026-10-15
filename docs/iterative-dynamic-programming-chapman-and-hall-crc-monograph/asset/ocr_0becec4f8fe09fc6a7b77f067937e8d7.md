nonconvergence. In model reduction the LJ method has been found useful to match the reduced system’s Nyquist plot to that of the original system [18], or used directly in time domain [40]. LJ optimization procedure has also been used successfully in model reduction in sampled-data systems [41].

# 2.3.1  Determination of region size

One of the aspects of LJ optimization procedure that was not considered until very recently is how to choose the region size vector **r** effectively at the beginning of the iterations, especially when a multi-pass procedure was used. This problem was recently addressed by Luus [22], by suggesting that the initial region size be determined by the extent of the variation of the variable during the previous pass, and, using this approach, rapid convergence resulted in parameter estimation problems [23,25]. With the use of reliable values for the region size at the beginning of each pass in a multi-pass run, the computational efficiency is increased quite substantially. For example, let us consider the nonseparable optimization problem introduced by Luus and Tassone [32] where we have a system described by three difference equations:

$$x_1(k+1)=\frac{x_1(k)}{1+0.01u_1(k)(3+u_2(k))}$$  (2.46)

$$x_2(k+1)=\frac{x_2(k)+u_1(k)x_1(k+1)}{1+u_1(k)(1+u_2(k))}$$  (2.47)

$$x_3(k+1)=\frac{x_3(k)}{1+0.01u_2(k)(1+u_3(k))}$$  (2.48)

with the initial condition

$$\mathbf{x}(0)=[2\quad 5\quad 7]^T.$$  (2.49)

The control variables are constrained by

$$0\leq u_1(k)\leq 4$$  (2.50)

$$0\leq u_2(k)\leq 4$$  (2.51)

$$0\leq u_3(k)\leq 0.5.$$  (2.52)

The performance index to be minimized is

$$I=x_1^2(P)+x_2^2(P)+x_3^2(P)+\left[\left(\sum_{k=1}^{P}x_1^2(k-1)+x_2^2(k-1)+2u_3^2(k-1)\right)
\left(\sum_{k=1}^{P}x_3^2(k-1)+2u_1^2(k-1)+2u_2^2(k-1)\right)\right]^{1/2}$$  (2.53)

where $P$ is the number of stages.