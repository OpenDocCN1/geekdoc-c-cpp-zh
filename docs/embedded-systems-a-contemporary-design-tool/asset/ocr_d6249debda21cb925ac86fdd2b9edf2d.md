# Stubs

In Figure 21.39, the main bus is indicated by the horizontal trace. The stub branches off the main bus to another module, which is indicated by the vertical trace. Reflections off that module can destructively interfere with signals on main bus. Such a phenomenon can be present in essentially any real-world design.

![](bbox=[0.28, 0.17, 0.42, 0.21])

Figure 21.39 Stub Branching off the Main Bus

# Ringback

illustrated in Figure 21.40, ringback identifies the amount of signal voltage that rings back into the threshold region of a receiving device. The primary effect is a delay in the transmitted signal being recognized and enabling the receiving device to respond to change in state of the input. A device in an indeterminate state for an extended time can significantly increase skew between signals and potentially lead to false outputs from receiving device.

![](bbox=[0.28, 0.36, 0.45, 0.47])

Figure 21.40 Ringback

# Nonmonotonic Edges

illustrated in Figure 21.41, nonmonotonic edges occur when a signal edge deviates from linear behavior through the threshold region. Such a phenomenon is caused by stubs on longer traces of a multidrop bus.

![](bbox=[0.28, 0.57, 0.63, 0.7])

Figure 21.41 Nonmonotonic Signal

# Return Path Discontinuities

A ground gap in the reference plane is illustrated in Figure 21.42. In the top trace fragment, the signal flows in the trace and the return current, indicated by the dashed line, flows under the signal trace.

![](bbox=[0.28, 0.81, 0.42, 0.9])

Figure 21.42 Return Path Discontinuity