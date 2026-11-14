+   * The ability to meet time constraints, including the time performance of constituent algorithms and real-time deadlines.
+   * The ability to meet communications costs both in time and in the complexity of the implemented solution.
+   * Size and weight constraints, which hold for both the software and the hardware. For the hardware, the design must fit within hardware components and for the software, the memory loading.
+   * Fundamental physics in the form of signal integrity issues and constraints exacerbated by substantially decreasing hardware footprints and increasing operating frequencies (in reality, the associated signal decreasing rise and fall times). The Free Software Foundation does an excellent job in mapping high level software to machine code. However, they are not confronted with the fundamental physics from our friends Maxwell et al.

Today, the current state of the art imposes some restrictions on the hardware architecture that arises from our successes in the hardware arena. The current state of hardware synthesis tools is far ahead of those in software domain. Many of these perform very well. Synthesis from VHDL, Verilog, or SystemC is rather straightforward. Our desire is to make problem computationally tractable as the power of the tools continues to increase.

Thus, to minimize the cost of a particular partition, we have a contemporary bias toward using off-the-shelf processors and easily synthesizable logic devices such as FPGAs. In such an environment we have libraries of proven components. Today, FPGA technology have advanced to point where a processor core can easily be dropped into middle of a CPLD device. The mapping from an HDL to array logic is well understood. Nonetheless, there remains much room for research and improvement.

ASICs and full custom ICs are expensive in both time and money. Once again, we have a bias toward ASICs that can be implemented from legacy libraries. Although more expensive than FPGAs, they are less costly than a full custom implementation.

Thus, while certainly improvements can always be made, there are also interesting areas are in software synthesis and in developing the associated tools. Once again, there have been many advances in this area. Code generators and template based software development are no longer novelties. Herein our focus can be on software component of the problem.

# 9.20.2 Software Synthesis

Translating a sequence of behavioral statements into a standard implementation language such as C or C++ is a relatively straightforward task. More difficult is formulating and meeting scheduling requirements and real-time constraints for the application.

Although this is rapidly changing today, the application is typically built on single processor accompanied by collections of programmable logics. The implication is that, in reality, with a single CPU we only have a single real thread of control. Consequently, concurrent threads of execution that may work well in a model but must be flattened into linear or sequential execution order can present a challenge. Thus, in a simple case, four threads executing concurrently in a model only receive one fourth of CPU rather than all of it. We can increase CPU speed by four times, which can often be impractical, or extend the time constraints.