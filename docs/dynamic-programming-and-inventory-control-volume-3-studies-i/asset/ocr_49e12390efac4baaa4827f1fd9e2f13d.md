We now test the equation (15.6.16) with \(m^3(x)\frac{\partial z}{\partial t}\frac{t}{t+1}\) and obtain
\[\frac{t}{t+1} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial t} \right)^2 (x,t) dx\)
\[+ \frac{t}{t+1} \int_s^{+\infty} m^{\frac{3}{2}}(x) \frac{\partial z}{\partial t} \left[ \frac{3}{2} \sigma^2 m' m^{\frac{1}{2}} \frac{\partial z}{\partial x} + \nu m^{\frac{3}{2}} \frac{\partial z}{\partial x} \right] (x,t) dx\)
\[- \lambda \frac{t}{t+1} \int_s^{+\infty} m^s \frac{\partial z}{\partial t} \left[ \int_0^{+\infty} (z(x-\xi, t) - z(x,t)) \mu(\xi) d\xi \right] dx\)
\[+ \frac{\sigma^2}{4} \frac{t}{t+1} \frac{d}{dt} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx = 0\)

hence
\[\frac{1}{2} \frac{t}{t+1} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial t} \right)^2 (x,t) dx + \frac{\sigma^2}{4} \frac{t}{t+1} \frac{d}{dt} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx\)
\[\le \int_s^{+\infty} m \left( \frac{\partial z}{\partial x} \right)^2 \left( \frac{3}{2} \sigma^2 m' + \nu m \right)^2 (x,t) dx\)
\[+ \lambda^2 \int_s^{+\infty} m^3 \int_0^{+\infty} (z(x-\xi, t) - z(x,t))^2 \mu(\xi) d\xi.\)

From the estimates already obtained (15.6.30) we deduce (15.6.27) and also
(15.6.31) \(\int_s^{+\infty} \frac{t}{t+1} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial t} \right)^2 (x,t) dx dt \le C ||\varphi||^2.\)

PROOF OF (15.6.27):
Let \(x_0 \in [s_0, M]\). Take \(\rho\) such that
\(0 < \rho \le \frac{s_0 - s}{2}.\)

We call
\(z_R(x,t) = E 1_{Y_y(t) \ge R}.\)

We use the estimate
\(\int_s^{+\infty} m^3(x) \left( \frac{\partial z_R}{\partial x} \right)^2 (x,t) dx \le C \frac{t+1}{t},\)
and the constant does not depend on R. In particular we deduce
(15.6.32) \(\int_s^{M + \frac{s_0 - s}{2}} \left( \frac{\partial z_R}{\partial x} \right)^2 (x,t) dx \le C_{s_0, M} \left( 1 + \frac{1}{t} \right),\)

where we have used the fact that \(m(x)\) has a positive infimum on the interval \([\frac{s+s_0}{2}, M + \frac{s_0-s}{2}]\). Now we have
\[\int_s^{+\infty} m z_R(x,t) dx = \int_s^{+\infty} m 1_R(x) dx = \int_R^{+\infty} m(x) dx\)
\[\ge \int_{x_0 - \rho}^{+\infty} m z_R(x,t) dx\)