+   8.12 Explain the difference between odd and even parity. Why would one use one scheme over the other?
+   8.13 What are the limitations of a basic parity scheme? What are the advantages?
+   8.14 What is the maximum amount of information that we can gain if a simple parity check shows no error? shows an error?
+   8.15 If the computed parity on a received code word agrees with the value that was received, what do we know about the correctness of the received data?
+   8.16 If the computed parity on a received code word disagrees with the value that was received, what do we know about the correctness of the received data?
+   8.17 What advantages do block codes have over a basic parity scheme? When would one use a block coding scheme instead of a basic parity scheme? What are the additional costs of a block code scheme?
+   8.18 How do cyclic codes compare with basic, linear, and block encoding schemes? Consider factors such as ease of implementation, complexity, and runtime complexity.
+   8.19 When should one consider using an error-detection/correction scheme as part of a data exchange? Give several examples.
+   8.20 What major costs does one incur when using an error-detection/correction scheme?

# 8.29 PROBLEMS

+   8.1 The chapter discussed the loss of the Ariane 5 rocket and attributed the failure to a mismatch between the word size in the sensors and the word size in the guidance system. Propose a series of tests that might have identified the problem prior to launch.
+   8.2 Propose an addition or a modification to the guidance and control system in the Ariane 5 rocket that would have managed the data in such a way as to have prevented the loss of the rocket without modifying the existing register sizes.
+   8.3 The chapter introduced a problem that occurred on the Mars Pathfinder in which a lower priority task was able to indefinitely block a higher priority task. Propose a series of tests that might have identified a problem prior to launch.
+   8.4 Propose a software or hardware modification that might prevent the blocking problem on the Pathfinder.
+   8.5 Provide a detailed hardware block diagram for the design of the voting block for the fail operational system architecture using different designs as presented in the chapter.

+   8.21 What are some of the security concerns with respect to an embedded system network interface?
+   8.22 When should one consider using an encryption/decryption scheme as part of a network interface? Give several examples.
+   8.23 With respect to a network interface, explain how authentication works.
+   8.24 Explain the purpose of a Secure Operations Center and how such a thing might work.
+   8.25 Explain the purpose of a Firewall and how such a thing might work.

# The Power System

8.26 Identify possible design solutions to address possible failures in the power system of an embedded application. Discuss the advantages and disadvantages of each of your proposed solutions.

# Self-Testing

8.27 Discuss several advantages and disadvantages of built-in self-tests.

# Failure Modes Analysis

+   8.28 During what stage of the development life cycle should failure modes analysis be used? Why?
+   8.29 What kinds of failures should be considered?

+   8.6 Develop a UML sequence diagram expressing the necessary activities and responses to three failures in a fail operational system architecture.
+   8.7 Provide a detailed software pseudocode design of the voting block for the fail operational system architecture using different designs as presented in the chapter.
+   8.8 Compare the strengths and weaknesses of the hardware and software voters discussed in Problems 8.5 and 8.7. Would your analysis change if the same design was used for each of the redundant systems? If so, how?
+   8.9 As an alternative to the fail operational system architecture, the chapter proposes a design utilizing lightweight redundancy. Develop a UML sequence diagram expressing the necessary activities and responses to a failure in the system architecture utilizing lightweight redundancy.
+   8.10 In the system architecture utilizing lightweight redundancy, propose a detailed hardware block diagram or software pseudocode design that identifies when a problem has occurred