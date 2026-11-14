+   - MANET, a source-to-source C compiler based on Cetus: http://specs.fe.up.pt/
+     tools/manet/

+   - KADABRA, a source-to-source Java compiler based on Spoon: http://specs.fe.
+     up.pt/tools/kadabra/

+   - MATISSE, a MATLAB to C/OpenCL compiler: http://specs.fe.up.pt/tools/
+     matisse/

The LARA strategies used in the context of goal (2) have been developed partially
based on the support that third-party tools provide to implement the semantics of the
LARA actions. It is conceivable that LARA strategies, while well defined, cannot be
used in cooperation with tools that do not export a “control interface” that allows the
LARA aspects to carry out the corresponding actions.

# ## 3.6 SUMMARY

This chapter presented the main concepts regarding the first stages of an applica-
tion’s design cycle such as its specification, prototyping and development with
the main emphasis on the abstraction levels, and on how to deal with different con-
cerns; the specializations required when dealing with generic code and with high-
level models, and on how to deal with multiple targets. This chapter also introduced
the concepts of translation, compilation, and synthesis design flows, and hardware/
software partitioning (including the mapping of computations to heterogeneous
architectures). Lastly, we have described an AOP language, LARA, specially
designed to allow developers to describe sophisticated code instrumentation schemes
and advanced mapping and compilation strategies.

# ## 3.7 FURTHER READING

Design flows operating on heterogeneous platforms with hardware accelerators
have been the focus of recent research (see, e.g., the hArtes design flow in [24]).
One of the main tasks of a design flow involves the decision to map computations
to software and/or hardware components. This task is traditionally known as hard-
ware/software partitioning (see, e.g., [25]), especially when the target system con-
siders software components implemented in CPUs and hardware components
synthesized from the input computations. More complete forms of hardware/
software partitioning also consider hardware accelerators being then synthesized
and/or exist as coprocessors. Recently, the migration of computations from the
CPU to hardware accelerators (including GPUs and FPGAs) is referred as offloading
computations to these devices.

Hardware/software partitioning started with static approaches, i.e., with partitioning
performed at design/compile time [26, 40]. At compile time there have been
approaches starting with the computations described in high-level code (such as from