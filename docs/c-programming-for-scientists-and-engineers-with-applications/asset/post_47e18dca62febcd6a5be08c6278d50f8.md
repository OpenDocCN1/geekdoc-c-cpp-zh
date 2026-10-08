
overall design, such a process can be made into a module and such a module can be used to replace the repeated process. It is called a spatial module. The C programming language provides the facility to represent these functional and spatial modules so that they are loosely coupled.

During the design process the user requirements are spelt out. A prototype of the design is developed and tested to see whether it meets the requirements. During the design process the designer must document the design and provide the capability for future updates. The design steps may be repeated several times before writing the application program, to eliminate any design flaws. If there are any design flaws in the solution algorithm, it may be too late to correct them when the final product is found to be functionally incorrect. Therefore, we cannot overstress the importance of the solution algorithm design process. This is the most crucial phase in the development of any software.

## 1.2.2 Structure Charts

A structure chart is a design tool that represents the functional and spatial modules of the algorithm and their relationship to one another. In a structure chart, the statement of the problem is resolved in the form of a rectangular box at the top level. For example, in Figure 1.3 “Calculate the square root of a number” is the statement of the problem. The functions in the next level are represented in rectangular boxes horizontally from left to right in the order in which they are activated. If there is any function in the second level that needs to be divided into subfunctions, the functions at each level are represented from left to right and the further subdivision of the functions at each level is represented vertically.

![](img/8356e6c3bfe3b10354682c60b1e74b1d_30_0.png)

## 12 Introduction to Computers and Programming

The structure chart represents the analysis of the problem of calculating the square root of a number. It also represents program modules. The module “Calculate the square root of a number” invokes the modules beneath it, passing data back and forth to them.

## 1.2.3 Functional Modules

Modules communicate with one another by passing information back and forth. In C, these modules receive numeric values and manipulate them, and the result is conveyed back to the invoking module. An invoking module is a function that calls another function. C provides the facility to write these modules as independent units of a program. These units can be compiled, debugged, and tested independently, then linked into an executable program. Modules can be input modules, computational modules, or output modules. There are number of functional modules available in C’s rich library of functions such as sqrt() to compute a square root of a number or max() to compute a maximum of a set of values. There may also be functional modules written by other people that are available for use. Programmers write their own functional modules for specific problems and, in addition, can use standard library functions and library functions written by other people, as they fit into their application. C is rich in library functions, which will be presented throughout the text. The list of all library functions is provided in Appendix B.

## 1.2.4 Review Questions

- 1. In modular design the large problem is divided into
- 2 What is the relationship between lower-level and higher-level modules in a hierarchy chart?
- 3 Modules must be tightly coupled. True or False? Explain.

## 1.3 Algorithms and Program Development

Solving a problem on a computer requires a thorough understanding and analysis of the problem and of the potential data. Once the problem has been analyzed, the detailed design of a solution can be developed in designing and developing a computerized solution to a problem is to develop an algorithm to solve the problem. At the same time, the algorithm must filter out inappropriate data.

## 1.3.1 Concept of an Algorithm

An algorithm is a procedure consisting of a finite number of precisely defined steps for solving a problem. Each step of an algorithm must be an unambiguous instruction which, when written in a computer language, can be executed by a computer. The order of the steps is critical, because most computers execute steps in the order in which they are presented. An algorithm must terminate whether not the task is completely successfully executed. That, it must recognize the end of the input data and when an answer is sufficiently accurate. Algorithms that monitor the weather, automatic teller machines, and nuclear reactors are continuously active. These types of algorithms are apparent exceptions to the termination requirement. However, they idle as they continuously poll input devices and are normally reactivated as needed.

> Programming Warning: Every step in the algorithm must be clear and precise and the algorithm must terminate.

Programmers should choose an algorithm on the basis of efficiency, reliability, and clarity. Algorithms should be efficient with respect to computational time, storage requirements, and response time. The degree of accuracy required is specified by the user. An algorithm is reliable when it consistently produces answers from valid data and rejects invalid data. Clarity means that an understandable programming style is used. Clarity should not be compromised. However, sometimes a compromise between the other factors is necessary. For example, efficiency may be sacrificed for the sake of a high degree of reliability.

The design of algorithms to solve simple problems can be straightforward, but design of algorithms for large, complex problems can be difficult and time consuming. Although this can only deal with simple problems, the techniques we use are important in the design of algorithms for complex problems.

One common approach to large and complex problems is to use top-down design. Top-down design starts at the top of the structure with a general statement of the problem written in a precise, formal way to provide a high-level specification of the algorithm. This is divided into separate logical parts and a general specification for the solution of these parts is given. These parts correspond to major modules in the final algorithm. The parts are then further subdivided and specifications are drawn up. Finally the algorithm reaches a stage where the specification consists of computations, comparisons, and data access that can be programmed without further explanation.

An Example of a High-Level Problem Specification Calculate, in pounds, the total amount of steel required to build a pipeline to carry water.

The next step would be to divide the problem into logical parts as follows:

- 1. Input the pipeline dimensions
- 2. Check their validity
- 3. Calculate the cross-sectional area
- 4. Calculate the volume of steel
- 5. Calculate the weight
- 6. Output the weight

Each stage of the algorithm should be carefully checked before the algorithm is written in a computer programming language and again before it is tested on a computer. If the design is not proved correct at each stage, it may contain errors that make it necessary to start over. Careful validation during the design process leads to a more nearly correct solution.

## 1.3.2 Concept of Programs and Data

A program is a sequence of executable, unambiguous instructions written in a computer language. The computer can understand instructions of various types: input/output instructions to input data into the computer and output answers from it; move instructions to rearrange data; arithmetic instructions to perform calculations; control instructions to control selection and repetition of actions; logic instructions to help the computer make choices. These types of instructions are available in most programming languages. In C there are also instructions to control where data is stored in the computer memory.

Input refers to data sent to the computer processor from a file on an automatic storage device or from an outside source. Input may come from a keyboard or an automatic device such as a weather station.
