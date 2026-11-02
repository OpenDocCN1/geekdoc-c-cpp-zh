![](bbox=[0.3, 0.07, 0.67, 0.33])

**FIGURE 5.4** Using linear interpolation to locate an event in time.

Setting this equal to zero and solving for t gives the location of the event in time at

t ≈ (h g_{j,k}) / (g_{j,k} − g_{j,k+1})

Now the integration step is reduced to this estimate of the event time and a new x_{i+1} is calculated. If this state satisfies condition 1 or 2 in the preceding paragraph, then the search ends; the event is found or the interval has shrunk so as not to include it. Otherwise, these steps are repeated.

To implement this procedure, the discrete-event model has, in addition to its discrete state q, two copies of the continuous state: the present value x and tentative next value x'. For each g_k, there is a Boolean variable e_k that is true if g_k(x,q) ≈ 0 or g_k(x',q) ≈ 0 and false otherwise. The variable h keeps the time separating x and x'. The model first looks ahead by a single integration step to calculate x'. Next, it looks for events at the ends of the interval [0, h] and for events within it that might have been missed. There are four cases. The simplest is where the g_k neither are zero at the ends of the interval nor change sign. In this case, there are no events and, barring external input, the state h units of time later is x'.

The other three cases involve discrete-events. If at the left end of the interval any of the g_k are within ε_tol of zero, then the e_k are set accordingly and an internal event occurs immediately. Conversely, if this is true at the right end of the interval and none of the g_k have otherwise changed sign, then an event occurs at h, with state x', and the e_k are again set accordingly. Otherwise, an event occurs inside the interval and must be located with greater precision—a new h is estimated, a new x' calculated, and the process repeated. Algorithm 5.1 shows this procedure in detail, using the corrected Euler and linear interpolation methods described above.

With Algorithm 5.1, the discrete-event model that simulates a hybrid system can be written compactly as follows. Let s = (x, q, x', ê, h) be the state of the model where ê is the vector of event flags e_1, ..., e_p. The error tolerance ε_tol and maximum