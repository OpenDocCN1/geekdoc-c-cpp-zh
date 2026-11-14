
**watchdog timer**
is easily remedied by simply reaching over and resetting the system. We do not have that luxury with an embedded application that may be flying along at 40,000 ft or two-thirds of the way to Mars. To address the problem, we add what we call a *watchdog timer*. Such a timer is not much more than a fancy alarm clock. Periodically, the microprocessor must reset the timer. If it fails to do so, the timer will reset the microprocessor, which generally solves the problem. In Figure 3, the signal from the watchdog timer comes in to the processor as a nonmaskable interrupt (NMI) – that is, an interrupt that cannot be ignored.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_40_0.png)

**Figure 3** A Microprocessor-Based Embedded System.

**real-time**
Time is often an essential constraint in an embedded application, in contrast to what one finds in a typical desktop application, for example. Stating that a system is *real-time* demands that the system must respond to designated external or internal events within a specified time interval. The expected response is typically the execution of the task associated with the triggering event.

**soft real-time system**
We identify three kinds of real-time systems based on the urgency of meeting the required time constraint. A system is considered to be a *soft real-time system* if failure to meet the time constraint results only in degraded performance.

**hard real-time system**
If a time constraint is not met in a *hard real-time system*, the system is said to have failed. Such a failure may be seen as catastrophic if it can result in considerable risk to people, to the environment, or to a system being monitored or controlled. A *firm real-time system* falls in between, with a mix of the two kinds of tasks.

**microprocessor** The implementation of a *microprocessor*-based embedded system combines the individual pieces into an integrated whole as we see in Figure 3, which presents the architecture for a typical embedded system and identifies the minimal set of necessary components.

## THE EMBEDDED DESIGN AND DEVELOPMENT PROCESS

Not too many years ago, we began the design of a new embedded application with some thought about the problem, wrapped some registers, logic, and buses around the microprocessor, wrote a few lines of assembly language code, downloaded the assembled object file to the development environment, debugged it, and shipped it – or so it seemed. Such an approach worked great when all we had to be concerned about was the microprocessor, a handful of inputs and outputs, a few Small-Scale Integrated (SSI) or Medium-Scale Integrated (MSI) gate packs, and firmware that fit into a couple of PROMs, as we see in the simple drawing in Figure 4.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_41_0.png)

Figure 4 Building an Embedded System.

We find that contemporary embedded applications tend to fall into two groups: the simple ones that run the toaster, microwave, or children’s video game, and the sophisticated ones that control a jet aircraft, manage an entertainment system, aid a medical doctor in diagnosing a patient, or help to control a nuclear reactor. The systems in the second group are orders of magnitude more complex than any of those we used to build. Designing by hand is no longer feasible. Utilizing an ad hoc approach tailored to each different application is too expensive and too fraught with error. We can’t simply wire a few parts together, hack out a bit of software, and spend days or weeks trying to debug the collection. We need tools; we need formal methods. We need tools to model our designs, to perform simulations, and to simplify and interactively optimize the hardware, software, and firmware. Ultimately, we need tools that we can use to synthesize portions of that design either as a programmable logic device or a VLSI circuit.

Figure 5 gives a high-level flow through the development process and identifies the major elements of the development life cycle. Specifically, the hardware portion of the life cycle involves the design, development, and test of the physical system architecture, packaging, printed circuit boards, and, ultimately, the individual components.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_42_0.png)

Figure 5 The Embedded System Life Cycle.

The software portion entails the tasks or algorithmic portion of the application. Such software may be written in a high-level language, assembler, or a mixture of the two. Work in assembly requires detailed knowledge of the microprocessor architecture and its register structure.

The traditional design approach has been to traverse the two sides of the accompanying diagram separately; that is:

- Design the hardware components.
- Design the software components.
- Bring the two together.
- Spend time testing and debugging the system.

Contemporary methodologies favor the combined and “simultaneous” design of both the hardware and the software components, with the objective of meeting system-level requirements through trade-offs between these two. The key points in such an approach are to specify and (iteratively) design and develop both aspects of the system concurrently with the goals of increased productivity – reduced design cycle time – and improved product quality.

Such an approach focuses on the major areas of the design process:

- Ensuring a sound hardware and software specification and input to the process.
- Formulating the architecture for the system to be designed.
- Partitioning the hardware and software.
- Providing an iterative approach to the design of hardware and software.

Each of the issues we have identified is listed in Figure 6 and will be addressed in detail during our studies of the development of modern embedded systems.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_43_0.png)

Figure 6 Considerations when Developing an Embedded System.

The contemporary creative design and development process begins with an abstracted notion of the system to be built and moves through an iterative series of transformations to the final product. Computer-based tools are essential to that process. To be able to effectively use such tools today, as engineers we must understand how to develop accurate hardware and software models of the systems we intend to design and build. As an integral part of embedded systems development, we continually trade off speed, size, power, cost, weight, or time constraints to meet specified constraints or to improve performance. Tools can help us to make those trade-offs more efficiently.

A comprehensive study of the design process and all related modeling tools and methodologies could easily take several volumes – and does. Here, we take a first step and lay the groundwork on which people may build with future work. We will introduce, study, and apply the basic concepts of formal methods and tools. We learn that good system designers and designs proceed using a minimum of five steps. These steps are listed in Figure 7.

- Requirements definition
- System specification
- Functional design
- Architectural design
- Prototyping

## Figure 7 Important Steps in Developing an Embedded System.

In today's world, we see that the contemporary design process must also take into consideration design reuse and intellectual property at every design stage. Through hierarchical modeling and functional decomposition, we will become familiar with and work with formal design methodologies. In our studies, we will use the Verilog HDL – Hardware Design Language – as our hardware modeling and simulation tool. We will study the software life cycle in depth; the Unified Modeling Language (UML) and structured methods are presented and will become our software modeling tools.

(A good, solid, secure, and reliable design always begins with a firm foundation (Figure 8). Without that, everything we add later is fragile. Today, engineering students who want to work in the embedded field must have a sound understanding of the basics of digital hardware and software architecture as well as facility with more complex systems. Thus, we will begin our studies by revisiting the basics; we will build on that knowledge as we move to new topics.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_44_0.png)

## Figure 8 The Essential Foundation.

We will open with the high-level structure and components coupled with an introduction to the von Neumann and Harvard architectures that comprise the hardware and computing core of an embedded application. That core is usually manifest as a microprocessor, microcomputer, or microcontroller. At the opposite end of the system hierarchy, we will take our first look at the bits, bytes, and volts as we study how the various and essential kinds of information (numbers, characters, addresses, and instructions) are represented inside of a digital system.
