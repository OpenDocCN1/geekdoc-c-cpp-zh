
Where $T = \text{the torque N.m}$
$a_m = \text{mean area of cross-section}$
$t = \text{the thickness of the circular section}$

The angle of twist is computed from the formula:
$$ \theta = \frac{\pi(1+v)TL}{E_m^2}$$

Where $L = \text{the length of the steel member}$
$E = \text{modulus of elasticity}$
$r = \text{the mean radius}$

- 5. Write a program to compute the stress distribution in a cylinder with an inner diameter $D_i$ and outer diameter of $D_o$ with inside pressure $p_i$ and the outside pressure $p_o$.

The formula for the radial stress is
$$\sigma_r = \frac{p_ir^2 - p_o^2 + (rr_o/r)^2(P_o - p_i)}{r_o^2 - r_i^2}$$

The formula for the angular stress is
$$\sigma\theta = \frac{p_ir^2 - p_o^2 - (rr_o/r)^2(P_o - p_i)}{r_o^2 - r_i^2}$$

Vary the inside pressure from 4000 pounds/square inch to 10000 pounds/square inch in increments of 1000 pounds. Assume the outside pressure is 0. The radius $r$ varies from $r_i$ to $r_o$.

| Internal Pressure | Radial Stress | Angular Stress |
|---|---|---||

- 6. Write a program to read measurements from a file and print them 6 per line, numbering the lines, with 10 lines per page, numbering the pages. There should be a title on the first page and column headings on every page. Do not number a line if there are no measurements to print in it. Do not number a page and print column headings if there are no measurements to print on it.

- 7. Write a program to print all of the numbers from a file that should contain only positive measurements. Print appropriate error messages if the file header is not 070503 followed by an integer that tells how many measurements are in the file, or if the measurements are not all positive.

# CHAPTER 5
# Modular Design and Functions

## Objective

To divide and subdivide the problem into logical modules. The modules are written in C as manageable and meaningful units called functions.

- 5.1 Introduction to Modular Programming
- 5.2 Functions
- 5.3 Computation Functions
- 5.4 Input and Output Functions
- 5.5 Recursive Functions
- 5.6 Sample Programs

The concept of modular programming was introduced in Chapters 1 and 2. Large and complex engineering and scientific problems require many lines of code to solve them. It is difficult for a programmer to write the code of a long program as a single unit or to debug and maintain a long program as a single unit. It is easier to find logic and execution errors in short modules. When a group of programmers works on a program, they work on separate modules, which are then integrated. As we have seen, a program can be modular by using design tools such as hierarchy charts, flowcharts, pseudocode, and control structures to implement a program as functional modules. C has the built-in capability for modules to be coded as independent functions. These functions are logical pieces of code, which can be compiled, executed, and tested separately for their correctness and functionality. Once functions are written and tested they can be integrated incrementally into an existing program.

Chapter Summary

Exercises

## 5.1 Introduction to Modular Programming

Present day projects in engineering and science are too large and complex to implement as single large programs. First of all it is difficult to analyze the problem as a whole. The problem should be divided into smaller problems along logical lines and the smaller problems analyzed in order to understand the big picture of the entire problem. The project can be easily managed if it is divided into specific tasks and further divided into subtasks that can be easily understood and programmed. Also, computations that are repeated in several places in a program can be identified as subtasks. Tasks and subtasks are represented as boxes in hierarchy charts at the solution design step of program development. Tasks and subtasks are defined as the functional units of the program. A functional unit is one that does a particular computation or moves specific data. Modular programs have the following advantages:

- Smaller modules are easier to understand.
- Different programmers can work on separate modules.
- Modular programs can be modified without changing the entire program.
- Repeated code can be replaced by function call.
- Modularized program is easier to read.
- Independent modules are easier to debug.

### 5.1.1 Design of Modular Programs

In modular design the top module implements the functional description. For example to design a reinforced concrete tank of diameter (d) and height (h) with wall thickness (t), define the top module as: Design the tank.

## 5.1 Introduction to Modular Programming

- Obtain the capacity of tank
- Compute the dimensions based on the assumption that height (h) of the tank is diameter (d)
- Estimate the quantity of materials
- Estimate the cost

The materials can be decomposed into two modules:
- Steel
- Concrete

The concrete can be further decomposed into modules:
- Cement
- Sand

The cost can be decomposed into two modules:
- Materials cost
- Labor cost

The relationship between components and their instructions is shown diagrammatically in Figure 5.1. The hierarchical nature of the diagram in 5.1 shows the generality of the modules at higher levels and the greater details in the lower levels. Notice that the general module is divided into two modules. 

At this stage it is possible to determine what information each module needs from the module above it, and what information each module can provide to the one above it. Each module can also be categorized as computational, input, or output. Table 5.1 shows the data flow between modules and the type of each module for the modules of 5.1.

From the table it becomes clear that module 3.2 must calculate the amount of concrete before calling on module 3.2.1 and 3.2.2 to calculate the amount of cement and sand. Also, module 4.1 must have a way to look up the costs of materials and module 4.2 must have a formula for estimating the amount of labor involved and information on current wages.

There are two approaches commonly used in the implementation of modular programs. The top-down approach would be to start at the top of the diagram and

![](img/8356e6c3bfe3b10354682c60b1e74b1d_287_0.png)
 5.1 Structure chart for the design of a water tank

| Table 5.1 Flow of Data Between Modules
| Module | Type | Needs to Know | Provides |
|---|---|---|---|
| 1 | input | | capacity of tank |
| 2 | computation | capacity of tank | dimensions of tank |
| 3 | computation | dimensions of tank | estimate of materials |
| 4 | computation | estimate of materials | estimate of cost |
| 5 | output | estimate of cost | |
| 3.1 | computation | dimensions of tank | estimate of steel |
| 3.2 | computation | dimensions of tank | estimate of concrete |
| 4.1 | computation | estimate of materials | cost of materials |
| 4.2 | computation | estimate of materials | cost of labor |
| 3.2.1 | computation | estimate of concrete | estimate of cement |
| 3.2.2 | computation | estimate of concrete | estimate of sand |
