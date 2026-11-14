Once the initial functionality is confirmed, testing efforts shift to ensuring that the completed system meets all requirements and design specifications. Any system will change and grow with time as modifications are made or as new features and capabilities are added to satisfy new and changing customer requirements. As with the original design, one must make certain that the completed system, with all its new features and capabilities, also satisfies all specifications. Meeting all specifications means making certain that the original behavior of the system has not been modified in unintended or unexpected ways as a result of the changes. Finally, because no manufacturing process is perfect yet, we must make certain that the system functions properly after being built.

# Test suites

When we are thinking about testing and when we are putting test suites together, a good way to think about them is in terms of the amount of information that can be gained with each step. When a step within a test fails, what is it saying? What is the maximum amount of information that can be gained from the failure? When a test succeeds, what does it say about the circuit or system being tested? Are we closer to proving that it performs as we desire? If yes, then good. If not, then why did we include that step?

# 2.9 MODELING, SIMULATION, AND TOOLS

As we have seen in our studies so far, modeling and simulation play a critical role in the design of modern-day digital circuits and systems. We have learned about several different kinds of tools as well as how and when we apply them. When we move to test, those tools should follow; they are just as important during the test portion of the development as they were during the design portion. Today one would not think about attacking a complex design without modeling tools like Spice, VHDL, or Verilog. Test problems should be attacked with the same formal methods.

As we learned earlier, models and modeling are essential to the design, development, and test of today's complex digital systems. One can use models to break a problem down into parts that are simpler and easier to manage. During the early stages in the design of a circuit or system, models can serve as aids to understanding and dealing with the complexity of the problems to be solved. During test, models serve as aids in understanding the behavior of the hardware or software under faulted conditions and as guides in developing a solid testing strategy and the subsequent tests.

Faults and errors in the original design or those introduced during its manufacture are no different in their effects on the behavior of the circuit or system than the components that are designed into the system. We will take a preliminary look how to begin to model such faults and the role such models play during the debug and test of a design. In Chapter 9, we will take a more detailed look when we introduce the co-design process.

+   - co-design
+   - intermittent, transient faults
+   - fault, failures errors

Before we begin, however, let's look at the scope of our problem. The analysis and understanding of *intermittent* (existing only occasionally) or *transient* (occurring only once) faults require detailed statistical information characterizing how they occur and special tools for analyzing the collected data. We will begin with some of the relevant vocabulary before we proceed. A *fault* is any unsatisfactory system condition or state. *Failures* and *errors* are different kinds of faults. A failure is an (undesired) dynamic event occurring at a specific time. An error is static. An error is an inherent characteristic of a system resulting, for example, from a design mistake or oversight. A fault can affect a system in many different ways.

Faults may be random or systematic, and failures are typically random. When a failure occurs in a system, we now have a system that once functioned properly that no longer