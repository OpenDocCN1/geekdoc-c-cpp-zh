# 5.7 APPROXIMATING CONTINUOUS INTERACTION BETWEEN HYBRID MODELS

Most numerical integration methods are designed for models in state space form, and it is therefore desirable to put continuously interacting components into a single atomic unit. Other considerations in the design of the simulation software may nonetheless militate against this, and a method for approximating continuous interaction with discrete-events is therefore indispensable.

A widely used technique, described in its most general form by Giambiasi et al. [50], is to encode in an event a polynomial that approximates a continuous output. The recipient of the event uses the polynomial to approximate the original, continuous trajectory. The widespread use of this method testifies to its great utility: it is embedded in the dead-reckoning algorithms of the *IEEE Distributed Interactive Simulation* (DIS) standard [1] and has been widely used in event-based methods for numerical integration [70, 99, 142, 158].

Continuous trajectories are encoded in an event as follows. Given $k$ samples $x_1,\ldots,x_k$ of the continuous function, and possibly some of its derivatives, at times $t_1,\ldots,t_k$, fit a polynomial to the data and send its coefficients in a discrete-event. The recipient keeps these coefficients and uses them to calculate approximate values of the continuous trajectory. In general, the more frequent the events and the greater the information embedded in the polynomial, the more accurate is the approximation.

Dead reckoning in the IEEE DIS standard probably represents the most familiar and most prominent use of polynomial events. Its purpose is to reduce the frequency of position updates for simulated objects in a distributed, interactive simulation. Each simulated object (aircraft, tank, ship, etc.) calculates, by any appropriate means, its time-varying position $x$ and velocity $v$. It also maintains the last position $x_o$ and velocity $v_o$ that it broadcast on the simulation network and the time $t_o$ when that information was sent. The recipients of this data approximate the object’s position at time $t$ with the line

$$\tilde{x}=x_o+(t-t_o)v_o \tag{5.27}$$

The originator of the data calculates its estimated position whenever it recalculates its actual position, and new values for $x_o$, $v_o$, and $t_o$ are sent if $x$ and $\tilde{x}$ deviate by some predetermined quantity. Figure 5.14 illustrates this method.

Dead reckoning uses a truncated Taylor series to approximate the object’s position, but any polynomial can be used in general; the specific choice will depend on the data that are available. For instance, Equation 5.27 could be expanded by using two velocity points $v_o$ and $v'_o$ at times $t_o$ and some earlier time $t'_o$ to more accurately approximate the actual velocity by

$$\tilde{v}=\frac{t-t'_o}{t_o-t'_o}v_o+\frac{t-t_o}{t'_o-t_o}v'_o$$