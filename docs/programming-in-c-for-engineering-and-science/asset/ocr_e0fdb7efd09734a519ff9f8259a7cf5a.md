fields, expressing each field as a decimal integer, and separating the fields with a period; for example, at the time of this writing, 163.205.10.1 was the IP address for the above site at the NASA Kennedy Space Center. Each of the four parts is an 8-bit integer, so the entire address can be stored in 32 bits.

# 7.1.1 Problem

A gateway is a device used to interconnect two different computer networks. Suppose that a gateway connects an engineering firm to the Internet and that the company’s network administrator needs to monitor connections through this gateway. Each time a connection is made, the IP address of the employee’s computer is transmitted to the network administrator, who analyzes the components that make up the address and records them.

# 7.1.2 Object-Centered Design

# 7.1.2.1 Behavior

The program will display on the screen a prompt for an IP address. The user will enter a string of characters from the keyboard, which the program will read. The program will then compute and output its four network/host information blocks on the screen along with descriptive text, or display an error message if the user did not enter a valid address.

# 7.1.2.2 Objects

From the statement of the desired behavior, we can identify the following objects:

| Problem Objects | Type | Kind | Name | |
|---|---|---|---|---|
| Software Objects | | | | |
| screen | output device | variable | cout | |
| prompt | text string | constant | none | |
| IP address | text string | variable | address | |
| keyboard | input device | variable | cin | |
| network/host information blocks | text string | variable | block1, block2, block3, block4 | |
| descriptive text error message | text string | constant | none | |

# 7.1.2.3 Operations

Again, from the statement of the desired behavior, we can identify the following operations:

+   i. Display a string on the screen.
+   ii. Read a string from the keyboard.
+   iii. Find each network/host information block and extract it from the string.
+   iv. Display each information block on the screen.

# 7.1.2.4 Algorithm

We now organize these operations into the following algorithm, which also shows how operation (iii) requires some refinement into simpler operations that are provided in C++.