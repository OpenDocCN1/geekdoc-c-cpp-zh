
- 8.12 Explain the difference between odd and even parity. Why would one use one scheme over the other?

- 8.13 What are the limitations of a basic parity scheme? What are the advantages?

- 8.14 What is the maximum amount of information that we can gain if a simple parity check shows no error? shows an error?

- 8.15 If the computed parity on a received code word agrees with the value that was received, what do we know about the correctness of the received data?

- 8.16 If the computed parity on a received code word disagrees with the value that was received, what do we know about the correctness of the received data?

- 8.17 What advantages do block codes have over a basic parity scheme? When would one use a block coding scheme instead of a basic parity scheme? What are the additional costs of a block code scheme?

- 8.18 How do cyclic codes compare with basic, linear, and block encoding schemes? Consider factors such as ease of implementation, complexity, and runtime complexity.

- 8.19 When should one consider using an error-detection/correction scheme as part of a data exchange? Give several examples.

- 8.20 What major costs does one incur when using an error-detection/correction scheme?

## 8.29 PROBLEMS

- 8.1 The chapter discussed the loss of the Ariane 5 rocket and attributed the failure to a mismatch between the word size in the sensors and the word size in the guidance system. Propose a series of tests that might have identified the problem prior to launch.

- 8.2 Propose an addition or a modification to the guidance and control system in the Ariane 5 rocket that would have managed the data in such a way as to have prevented the loss of the rocket without modifying the existing register sizes.

- 8.3 The chapter introduced a problem that occurred on the Mars Pathfinder in which a lower priority task was able to indefinitely block a higher priority task. Propose a series of tests that might have identified a problem prior to launch.

- 8.4 Propose a software or hardware modification that might prevent the blocking problem on the Pathfinder.

- 8.5 Provide a detailed hardware block diagram for the design of the voting block for the fail operational system architecture using different designs as presented in the chapter.

- 8.21 What are some of the security concerns with respect to an embedded system network interface?

- 8.22 When should one consider using an encryption/decryption scheme as part of a network interface? Give several examples.

- 8.23 With respect to a network interface, explain how authentication works.

- 8.24 Explain the purpose of a Secure Operations Center and how such a thing might work.

- 8.25 Explain the purpose of a Firewall and how such a thing might work.

## The Power System

- 8.26 Identify possible design solutions to address possible failures in the power system of an embedded application. Discuss the advantages and disadvantages of each of your proposed solutions.

## Self-Testing

- 8.27 Discuss several advantages and disadvantages of built-in self-tests.

## Failure Modes Analysis

- 8.28 During what stage of the development life cycle should failure modes analysis be used? Why?

- 8.29 What kinds of failures should be considered?

- 8.6 Develop a UML sequence diagram expressing the necessary activities and responses to three failures in a fail operational system architecture.

- 8.7 Provide a detailed software pseudocode design of the voting block for the fail operational system architecture using different designs as presented in the chapter.

- 8.8 Compare the strengths and weaknesses of the hardware and software voters discussed in Problems 8.5 and 8.7. Would your analysis change if the same design was used for each of the redundant systems? If so, how?

- 8.9 As an alternative to the fail operational system architecture, the chapter proposes a design utilizing lightweight redundancy. Develop a UML sequence diagram expressing the necessary activities and responses to a failure in the system architecture utilizing lightweight redundancy.

- 8.10 In the system architecture utilizing lightweight redundancy, propose a detailed hardware block diagram or software pseudocode design that identifies when a problem has occurred

- 8.11 Propose a hardware or software strategy for detecting, annunciating, and managing a node or link failure in a system utilizing a star bus configuration.

## 8.12 Repeat Problem 8.11 for a system utilizing

- (a) A multidrop bus configuration.
- (b) A single ring bus configuration.

## 8.13 Using an array as the model for a typical data container for storing unsigned integers.

- (a) Identify all of the boundary conditions that should be tested for.
- (b) Write a software program that will implement the tests identified in part (a).

- 8.14 Design an algorithm that accepts data from an external source. Data values that fall in the range of ±4.0 are considered to be valid; data values exceeding the range are considered invalid. If the data is within range, it is to be displayed. If values fall outside of the valid range, a warning is to be issued and displayed and no additional data accepted until the warning is acknowledged. Use sinusoidal data in the range of ±5.0 to verify the performance of your algorithm.

- 8.15 Extend the design in Problem 8.14 to issue the warning and display the ceiling and floor values of the data but continue to accept input data. If the input data value returns to the specified range, the warning annunciation is to continue until acknowledged, but the current incoming data values are to be displayed.

- 8.16 Give a Verilog design for a system that will accept an 8-bit word, in parallel, append an odd parity bit, and output the resulting 9-bit word.

- 8.17 Repeat Problem 8.16 by writing a software algorithm to accomplish the same task.

- 8.18 Give a Verilog design for a system that will accept a 9-bit word, in parallel, check for odd parity, and output the 8-bit data word if the received parity is correct; otherwise issue an error.

- 8.19 Repeat Problem 8.18 by writing a software algorithm to accomplish the same task.

- 8.20 Give a Verilog design for a system that uses a Hamming code for error management. The system should accept an 8-bit data word, in parallel, encode the data, then output the resulting code word.

- 8.21 Repeat Problem 8.20 by writing a software algorithm to accomplish the same task.

- 8.22 Give a Verilog design for a system that will accept a 16-bit word that has been encoded using a Hamming code. The system should then check and output the corrected 8-bit data word.

- 8.23 Repeat Problem 8.22 by writing a software algorithm to accomplish the same task.

- 8.24 Give a Verilog design for a system that uses a block code for error management. The system should accept a 15-word block of 8-bit data words one word at a time, generate odd parity over the individual words, and even parity over the block, output each of the 15-9-bit data words, followed by the block check character.

- 8.25 Repeat Problem 8.24 by writing a software algorithm to accomplish the same task.

- 8.26 Give a Verilog design for a system that will accept a block of data words encoded as specified in Problem 8.24; then check the parity for each data word and for the block. The system should output each of the 8-bit data words, issue a word error if the parity is incorrect for any word, and issue a block error if the block check word is in error.

- 8.27 Repeat Problem 8.26 by writing a software algorithm to accomplish the same task.

- 8.28 Give a Verilog design for a system that uses cyclic encoding based on the following generator polynomial for error management.

g(x) = x⁸ + x⁷ + x⁶ + x⁴ + 1

- (a) Use your design to encode the word 1011001.
- (b) Verify that your design can detect a single-bit error in a received code word.

- 8.29 Repeat Problem 8.28 by writing a software algorithm to accomplish the same task.

- 8.30 Implement the design for the monitoring and control system for the full-operation 15.0 VDC redundant power supply system discussed in the chapter. You can assume that values of the supply voltages are acquired through an analog-to-digital converter.

- 8.31 Implement the design for the monitoring and control system for the reduced-operation 15.0 VDC power supply system that utilizes four set points discussed in the chapter. You can assume that values of the supply voltages are acquired through an analog-to-digital converter. Choose the set point to be in the range of 4–14 VDC. Explain the reasoning behind each of your choices.

- 8.32 Design a built-in self-test for a 256K by 8 SRAM. You must ensure that no data is ever corrupted as a result of your test. Your test must be able to operate while normal memory operations are taking place. Is your design done in hardware, software, or a combination? Explain your choice.

- 8.33 Design a power up self-test for a 256K by 8 ROM that utilizes a block check scheme. Is your design done in hardware, software, or a combination? Explain your choice.

- 8.34 Give the pseudocode for an algorithm that verifies the operational integrity of an embedded application at power up. State any assumptions.
