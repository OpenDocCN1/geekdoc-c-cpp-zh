![](bbox=[0.11, 0.12, 0.87, 0.52])

# FIGURE 11.7 Single CPU and GPU water cooling loop.

Liquid cooling may sound like an exotic solution to the heat problem, but it’s actually quite a practical one. One of the major breakthroughs in cooling in the early days of supercomputers was the use of nonconductive liquids. The Cray-II, for example, used a special nonconductive liquid made by 3M called Fluorinert into which the entire circuit boards were immersed. The liquid was pumped through the system and then to an external cooling unit where the heat was dispersed.

For GPU computing, we’ve moved on a little. Although immersing an entire motherboard and GPU in nonconductive liquid such as commonly available oils works, it’s not a good solution. The liquid can eventually penetrate sensitive components, which ultimately results in system failure.

Liquid cooling enthusiasts came up with the idea of liquid cooling blocks. These are hollow blocks of copper through which liquid runs and never makes physical contact with any electrical (Figure 11.7). You can buy nonconductive liquids, which we use in our liquid-cooled systems, minimizing the risk of any damage to components should some spillage occur.

A modern liquid-cooled system consists of a number of heat collectors, a CPU block, one or more GPU blocks, and, optionally, memory and chipset blocks. The hollow copper blocks have liquid pumped through them, which is fed from a reservoir. The output of the heated liquid is then fed into a cooling system, usually one or more radiators or a heat exchanger. The typical layout is shown in Figure 11.8.