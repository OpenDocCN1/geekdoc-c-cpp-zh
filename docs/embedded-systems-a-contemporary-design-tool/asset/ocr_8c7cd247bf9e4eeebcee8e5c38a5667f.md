distinguish between seeded and nonseeded faults. Thus, if x% of seeded faults remain, then x% of nonseeded faults probably remain as well.

An excellent and effective technique for testing basic combinational logic circuits in production is to apply large sequences of random binary patterns to the device inputs. A software testing method called fuzz testing or fuzzing employs a similar idea. The goal of such a scheme is to discover and identify programming errors or security weaknesses in the system and user software. To wit, the software package under test is stimulated with sequences of random, invalid, or unexpected data. The objective is to initiate and identify potential crashes, exceptions, memory leaks, or failures to intended or expected code functionality. An important property of the test data is that it must appear to be sufficiently valid to avoid immediate rejection by the supporting software tools. Yet, such data must also be robust enough to be able to trigger unintended or unexpected behaviors when downloading or applied to the system.

As with any testing, focusing the test design and the testing on areas that can potentially lead to the most damage is important. Earlier, we discussed the concept of a trust zone. A weakness or design oversight in the access protocol to a trust boundary can facilitate opening a door for an attack. Thus, such areas should be given high priority when executing a fuzz test strategy.

# 8.23.3 Protecting the Hardware

Protecting the hardware, like protecting the software, begins with good, disciplined design, implementation, and test practices. We repeat that engineering and the design cycle are an iterative, not a one pass process, and iterative does not mean that we keep guessing until something works. Rather, we continually revisit all steps, as necessary, to ensure a safe, reliable, secure design that meets or exceeds initial or modified requirements.

# 8.23.3.1 First Steps

The following are some preliminary steps that should be followed at the start of a development cycle and then routinely thereafter. At this stage, we are thinking about and planning the design of the system.

Know and understand your system. Build a complete and accurate (memory) map for the system. Know the address or range of addresses for each piece of hardware in the system. Use this information in conjunction with the boot process to detect attempts to alter the boot sequence.

# 8.23.3.2 Second Steps

Moving from concept to design is the next step. Design and incorporate a controlled/limited/restricted access hardware self-test. At power on/boot time, that test should be able test and confirm that each piece of hardware is functional and is at its proper location with the proper identification prior to initializing or enabling the system's runtime function.

Such tests should be independent of and isolated from the system's runtime hardware and software. The controlled access (codes and technique) should also be different from those used for primary system access and control. Both are supported by MILS operating system specifications.

As is done for high reliability fail operational or fail operational systems, the design of the self-test subsystem and the runtime subsystem should utilize different hardware and processor types as well as separate power systems and data and control buses.