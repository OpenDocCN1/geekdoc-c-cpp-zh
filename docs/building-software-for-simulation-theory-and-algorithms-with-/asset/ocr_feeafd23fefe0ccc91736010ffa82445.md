```
```cpp
double new_err = -(*(xb.begin())); // New error value
err_int += new_err*err; // Integral of the error
double derr = (new_err-err)/e; // Derivative of the error
err = new_err; // Value of the error
csignal = 50.0*err+5.0*err_int+1.0*derr; // Control signal
send_control = true; // Send a new control value
}
void delta_conf(const adevs::Bag<double>& xb)
{
    delta_int(); delta_ext(0.0,xb);
}
double ta() { if (send_control) return 0.0; return DBL_MAX; }
void output (const adevs::Bag<double>& yb) { yb.insert(csignal); }
void gc_output(adevs::Bag<double>&){}
private:
    double err, err_int, csignal;
    bool send_control;
};

#endif
```
```

# 6.1.2  Integration with an Ethernet Simulator

Now the cart and its controller are separated by a 10-Mbps (megabits per second) Ethernet that is shared with several other computers. What these others do is unimportant, but they consume some fraction of the network’s throughput. From the perspective of the cart and controller, additional network traffic degrades the performance of the communication channel by introducing delay, variation in delay, and, in some instances, lost data. When other users place very little data onto the network, their impact on the performance of the controller is negligible. As much as 40% of the network capacity can be consumed by other users before there is a noticeable change in the trajectory of the cart and pendulum, but greater use of the network degrades the controller’s performance.

The simulator for this system has three parts: the controller and cart, the Ethernet, and the sources of background traffic. The first part is built with our simulation framework. A model of the network and traffic generators is available as part of the OMNeT++ (objective modular network testbed) simulation tool and its INET extension (the software is available for download at http://www.omnetpp.org/). To build an integrated model, the simulator for the controller and cart are embedded in an OMNeT++ component, which in turn is connected to OMNeT++’s model of an Ethernet frame encapsulator and MAC device. The rest of the network is built using the graphical tools and NED language that are native to OMNeT++.

Figure 6.3 shows the classes that are directly involved in the integration of the cart and controller model with the OMNeT++ simulator. The CartPID class encapsulates the Simulator, PIDControl, and CartModel classes within a single OMNeT++ module. This module does three things: (1) it intercepts messages coming from the