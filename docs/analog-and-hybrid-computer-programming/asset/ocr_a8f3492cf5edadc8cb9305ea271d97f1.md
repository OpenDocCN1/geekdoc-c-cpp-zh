![](bbox=[0.28, 0.09, 0.86, 0.31])

Fig. 2.13. Generating a parabola by double integration over a constant

The simplest operation cycle of an analog computer consists of the mode-sequence IC-OP-HALT with the time spent in OP-mode either determined manually or by a precision timer. This is typically called manual control and is often used on low-speed computations.

Nevertheless, in many cases it is desirable to display a more or less flicker-free image of variables vs. time on an oscilloscope display and this requires an automated mode of operation called repetitive operation. Here a precision timer cycles the integrators repetitively through the mode-sequence IC-OP-IC-OP-... With sufficiently high time scale factors it is possible to repeat a full simulation run every couple of milliseconds, thus making it possible to display a set of graphs on an oscilloscope.

Since it is, of course, possible to change the coefficients and initial conditions of a computer setup manually at every instant, repetitive operation can give an immediate insight into the behaviour of a problem with respect to its parameterization as one can see the effects of parameter changes instantaneously on the display.

A variant of this mode of operation is called single run and consists of a single sequence IC-OP-HLT with preset IC- and OP-times. This is especially useful when using a pen plotter as output device where a single run will draw a particular solution of a problem.

The computer setup shown in figure 2.13 illustrates repetitive operation. It consists of two integrators in series where the leftmost integrator is fed with the constant +1. A summer with only one input is used to invert the sign of the output of this first integrator.

Setting both integrators to the same time scale factor k0 = 10^n and setting the OP-time to 2·10^3−n milliseconds, e.g. k0 = 100 and OP-time 20 ms, yields a linear