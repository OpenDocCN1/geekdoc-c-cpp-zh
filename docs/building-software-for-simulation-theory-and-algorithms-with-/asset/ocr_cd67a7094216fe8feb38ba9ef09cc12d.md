```
```cpp
17 void der_func (const double *q, double *dq);
18 // State event function that detects turning movements
19 void state_event_func (const double *q, double *z);
20 // Sample x, y, and theta periodically
21 double time_event_func (const double *q);
22 // Expiration of the timer and collision events are internal
23 void internal_event(double* q, const bool* events);
24 // Change in the motor voltage is an external event
25 void external_event(double *q, double e,
26                  const adevs::Bag<SimEvent> &xb);
27 // Confluent events
28 void confluent_event(double* q, const bool* events,
29                  const adevs::Bag<SimEvent> &xb);
30 // Output position events for the display when the timer expires
31 void output_func(const double *q, const bool* events,
32                  adevs::Bag<SimEvent> &yb);
33 // Garbage collection
34 void gc_output(adevs::Bag<SimEvent>&){}
35 // Get the resistance of the motor (left and right are the same)
36 double getMotorOhms() const { return Rm; }
37 // Is the tank turning?
38 bool isTurning() const { return turning; }
39 // Get the current in the motor
40 double getLeftCurrent(const double* q) const;
41 double getRightCurrent(const double* q) const;
42 // Index of the turning state events and timer time event
43 static const int TURNL, TURNR, TIMER_EXPIRE;
44 // Indices of the state variables
45 static const int WL, WR, FL, FR, IL, IR, X, Y, THETA, W, V, TIMER;
46 // Model parameters
47 const double mt, Jt, B, Br, Bs, Bl, Sl, Lm,
48                  Rm, Jg, Bg, g, alpha, r, Kt;
49 private:
50     // Initial conditions
51     const double x0, y0, theta0;
52     // Hysteresis value for stopping turns
53     const double Hs;
54     // Communication interval for the numerical integration algorithm
55     const double cint;
56     // Motor voltages
57     double el, er;
58     // Is the tank turning?
59     bool turning;
60     // Use simplified dynamics?
61     const bool simple;
62 };
63
64 #endif
```
```