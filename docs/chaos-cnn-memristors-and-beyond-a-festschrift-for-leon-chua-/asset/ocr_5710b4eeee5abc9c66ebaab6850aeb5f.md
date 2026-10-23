![](bbox=[0.094, 0.092, 0.489, 0.364])

Fig. 1. The current main areas of research with respect to memristors.

![](bbox=[0.512, 0.089, 0.887, 0.338])

Fig. 2. The pinched hysteresis loop of a so-called HP memristor driven by a periodic source voltage \(v(t)=V\cos(\omega t)\). The memristor symbols indicate the state of the memristor, i.e. the wider the red region becomes, the higher is the conductance of the device.

conceptually and practically realized [3, 8, 15]. The theory behind the memristor has been extended as well but mostly within the frame of single memristors [3, 7] and less for extended networks which include memristors [6, 11]. Electrical circuits with memristors are often difficult to analyze due to the nonlinearity and the dynamics of the memristor.

The analytical description of memristor networks is the very aim of this chapter which is structured as follows: First, we will give a short introduction to the basic properties of single memristors in general and the HP memristor in particular. In Sec. 3, we then consider the *Multilinear Theory of Nonlinear Networks* [10], which can be applied to simple structured memristor networks. For more complex networks we introduce a method based on a *Volterra Series* representation. By means of this, a general description of single memristor circuits is obtained.

# 2. The Behavior of Single Memristors

According to Chua’s definition [4] a memristor is a device which has a characteristic curve in the \(\Phi-Q\) domain where \(\Phi(t)=\int_{-\infty}^{t}v(t')dt'\) denotes the flux and \(Q(t)=\int_{-\infty}^{t}i(t')dt'\) denotes the charge. The characteristic curve may be presented by either of the two possibilities,

$$\Phi=F(Q)\quad\text{or}\quad Q=G(\Phi). \tag{1}$$

In the first case, we name the device a charge controlled memristor whereas in the second case, the device is called a flux-controlled memristor. The memristance \(M\) and the memductance \(W\) are defined by

$$M=\frac{dF(Q)}{dQ}\quad\text{and}\quad W=\frac{dG(\Phi)}{d\Phi}, \tag{2}$$

respectively. In 1976, Chua and Kang generalized the memristor to the concept of memristive systems [5]. The memristance of such a system depends on an internal state vector **x**. A memristive system is defined by

$$v(t)=M(\mathbf{x})\cdot i(t)$$
$$\dot{\mathbf{x}}=f(\mathbf{x},i). \tag{3}$$

A capacitance and inductance can be defined as well with an additional state vector giving the memory related quantities \(L(\mathbf{x})\) (meminductance) and \(C(\mathbf{x})\) (memcapacitance) [14]. The best investigated type of memristor is the \(TiO_2\)-memristor which usually is called the HP memristor for sake of simplicity. Starting with a linear drift model [13], the memristive behavior could be described simply by a series of voltage dividers. A more advanced model takes into account a nonlinear drift and the boundaries of the memristor by means of a window function \(F(x)\) (e.g. [9]),

$$v(t)=\left(R_{ON}x+R_{OFF}(1-x)\right)\cdot i(t)$$
$$\dot{x}=\lambda\cdot i(t)\cdot F(x). \tag{4}$$