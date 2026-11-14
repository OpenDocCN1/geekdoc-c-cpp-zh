+   2.10 What are the pros and cons of using an open drain/collector device versus a tristate device?
+   2.11 Can an open drain/collector device be used on a tristate bus? Why or why not?

# Fan-In and Fan-Out

+   2.12 Can the calculated fan-out of a logical device be exceeded? If not, why? If so, what are the consequences of doing so?
+   2.13 Can a design such as that described in Question 2.12 be considered to be a good design? If not, why not and if so, why?
+   2.14 Where on a device data sheet would one look to find information supporting a decision such as that described in Question 2.12 and the consequences of such a decision?
+   2.15 How do we compute fan-out for devices from one logic family driving a different logic family? fan-in?

# Real-World Gates – Time

+   2.16 What are the consequences of increasing the rise time or a logic signal? the fall time?
+   2.17 Do the consequences of the situation described in Question 2.16 change as the frequency of the input signal changes?
+   2.18 What are the consequences on the output of a logical device of the rise time of an input signal being longer (shorter) than the fall time?
+   2.19 Do the consequences of the situation described in Question 2.18 change as the frequency of the input signal changes?
+   2.20 What are the effects on the output of a logical device of propagation delay through the device?
+   2.21 How do the effects of propagation delay through a logical device change with increasing (decreasing) frequency?
+   2.22 How is the output of a device affected if the propagation delay through the device is longer (shorter) for a signal making a transition from a logical 0 to a logical 1? Under the same circumstances, how is the output affected, for a state change in the opposite direction?
+   2.23 If a logical circuit has a critical race condition, can that race be corrected by using additional logic gates to match the lengths of the delay paths causing the race? Why or why not?
+   2.24 How can one correct a critical race condition without matching delay path lengths?

# Real-World Gates – The Legacy of Physics

+   2.25 How does the resistance of a piece of material such as a wire or printed circuit board trace affect the temporal behavior of a signal passing through the material?

+   2.26 Describe how the phenomenon called self-inductance occurs.
+   2.27 Describe how the phenomenon called mutual inductance occurs.
+   2.28 What is meant by the term cross talk?
+   2.29 Explain how cross talk can occur via capacitive coupling? via inductive coupling?
+   2.30 Using the first-order RC model of a wire described in Figure 2.28, what is the effect on the temporal behavior of a signal being driven from an open drain/collector device?
+   2.31 Using the first-order RC model of a wire described in Figure 2.28, what is the effect on the temporal behavior of a signal being driven from a tristate device?
+   2.32 Using the first-order RC model of a wire described in Figure 2.28, what is the effect on the temporal behavior of a signal being driven into that wire from a device with a totem pole output configuration?
+   2.33 What are some of the possible effects on the output of a logic gate if one (or more) of the device input(s) is floating?
+   2.34 Do the effects described in Question 2.33 change if the logical device is implemented using CMOS technology? TTL technology?
+   2.35 Do the effects described in Question 2.33 change if the frequency of the input signal is increased? decreased?
+   2.36 What are some of the possible temporal effects on the output of a logic gate if the first-order model of an input digital signal wire is replaced by a second-order model?
+   2.37 What is meant by the term damping factor?
+   2.38 What is the effect on a digital signal if the damping factor for a conducting path is <1, =1, >1?

# Testing Combinational Circuits

+   2.39 When we are troubleshooting an embedded subsystem or system, what fundamental assumptions can we make?
+   2.40 When we are testing an embedded subsystem or system, what fundamental assumptions can we make?
+   2.41 When we are debugging an embedded subsystem or system, what fundamental assumptions can we make?
+   2.42 Consider that we are debugging a circuit of subsystem and we encounter an intermittent or transient fault. We replace one or two parts and the problem goes away. Can we assume that the parts that we replaced were bad? If not, why not?
+   2.43 If we have been debugging two modules and have now concluded that both are working properly, it is now time to integrate them into a larger subsystem. Can we assume