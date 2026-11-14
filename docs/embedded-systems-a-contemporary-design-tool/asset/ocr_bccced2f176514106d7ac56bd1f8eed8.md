+   - The synchronization relation, which specifies temporal dependency.
+   - The message transfer by port, which implies a producer/consumer kind of relationship.

We will discuss each of these when we study processes and inter-process communication. All of them are critical in the design and development of today's embedded systems.

# 9.18.2 The Architectural Model

The architectural model describes the physical architecture of the system based on real hardware components such as microprocessors, arrayed logics, special purpose processors, custom circuitry, analog and digital components, and the many interconnections between them.

# 9.18.3 The Need for Both Models

These two views, when considered separately, are not sufficient to completely describe the design of contemporary systems. It is necessary to add the mapping between the functional viewpoint and the architectural one. Such a mapping defines a (functional) partition and the allocation of functional components to the hardware and/or the software elements. Such a process is also called architectural configuration.

+   - mapping
+   - functional viewpoint
+   - architectural configuration
+   - functional model
+   - architectural structure

The functional model, located between the specification model and the architectural model, is suitable for representing the internal organization of a system. It explains all necessary functions and the couplings between them – expressed from the point of view of the original problem. Using such a scheme leads to a technology-independent solution. In particular, with this kind of model, all or part of the description can be implemented either in software or hardware. Once again, ideal for the Co-Design methodology.

The functional model is the basis for a coarse-grain partitioning of the system. Such a partitioning leads naturally to the selection of which functions to implement in hardware or software. The architectural structure is finer grained and generally follows from the functional model; the architecture may also be imposed a priori.

# 9.19 MODELING TOOLS AND LANGUAGES FOR CO-DESIGN

We have now formulated a high-level architecture for the system. The next steps are Co-Synthesis and Co-Simulation, i.e. mapping the architecture to an executable model, synthesizing the model, and simulating the system running the modeled hardware and software. Before taking that step, let us look at some of the available modeling tools and methods.

Specifying and modeling complex contemporary embedded designs draws upon wide variety of tools and methods. We want to be able to model and conjoin both the hardware and the software and, thus, we must have a seamless way of expressing both and ultimately sequencing in the real physical hardware. Solid models, as well as modeling and specification languages, are essential for comprehending, expressing, managing, and validating the design. It is important to keep in mind that no one tool does everything for all phases of the development process.

The Co-Design process utilizes a variety of models at different levels and for different reasons. For the structural and hierarchical aspects, we utilize system description languages