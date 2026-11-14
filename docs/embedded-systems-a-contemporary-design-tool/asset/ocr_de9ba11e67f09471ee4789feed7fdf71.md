+   • Synchronous data flow
+   The synchronous data flow model is a special case of the more general process networks. Restrictions are on the understanding of deadlocks and bonds on operations Modules execute sequentially to complete the task. The model supports computations that operate on streams of data token. The operation schedules is statically determined.

+   • Discrete event
+   Modules react to events occurring at instant of time. An event comprises a value and time stamp. The model is applicable to systems that respond to input events, produce output events either at same time or at some future time instant.

+   • Continuous time
+   Models components that interact through continuous time signals. It provides support for analog aspects of some circuits.

# 9.23 CO-VERIFICATION

It is assumed that verification has followed each iteration through the partition-simulate-synthesize cycle. It is further assumed that we have been doing all the appropriate analysis of our design throughout. We are now in the latter stages of the development. We have completed a "final" synthesis of our design and must confirm that it satisfies our original system specification.

# 9.23.1 Hardware-Software Co-Verification

Hardware-Software Co-Verification gives us a means for testing and stressing our design long before we have a physical prototype available. We endeavor to reduce risk by identifying problems earlier rather than later. As today's designs become increasingly integrated, visibility into the internals of the devices becomes more and more limited.

Unfortunately, traditional tools such oscilloscopes and hardware logic analyzers rely on being able to connect and to monitor important signals such as system buses or other data and control signals. With no places to connect to, they lose their effectiveness.

**JTAG** The JTAG port was developed with intention of giving some access. The attendant difficulty is that it must be designed into the system early in the process and consumes valuable internal real estate and I/O pins.

**Signal Tap** Another tool, Signal Tap, developed initially by Altera, provides a very effective way of implementing a soft logic analyzer onto an FPGA.

Driven by the high costs of errors in silicon coupled with increasing demands to reduce time to market, our desire is to verify that our design is correct prior to first silicon. Through Co-Simulation and Co-Verification we strive to verify the hardware-software interface, accelerate the firmware debug process, and exercise the boot code, hardware and software diagnostics, device drivers, board support packages, and some application code.

It is recognized that a good model improves the probability of a solid design. However, models are not perfect. Modeling every hardware and hardware-software interaction quickly becomes impractical as we move toward smaller and higher performance systems. A circuit that may work superbly on paper or as a distributed prototype may suffer signal integrity issues such as severe noise, cross talk, and electromagnetic interference (EMI) contamination as geometries are reduced and operating frequencies increase (rise and fall times decrease) in today's designs.