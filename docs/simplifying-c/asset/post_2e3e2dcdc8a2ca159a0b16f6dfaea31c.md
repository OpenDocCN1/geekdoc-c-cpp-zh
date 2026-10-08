
Let’s now discuss these symbols in brief.

- □ Input/Output symbol: Represents an input to be taken from a user or an output to be displayed on the terminal. It is usually known as an I/O symbol. We can use this symbol for accepting multiple inputs as well as displaying multiple line outputs on the screen.

- □ Terminal symbol: Indicates start or end of a set of instructions in a sequence within a flowchart. At times, it is used to indicate a pause in the set of instructions.

- □ Process symbol: Signifies the core logic of the set of instructions. It represents data movement and arithmetic operations, such as addition, subtraction, and multiplication, present in the set of instructions. Multiple operations can be shown in a single process symbol, which is known as a compound process symbol. The operations in the compound process symbol will be resolved in the sequence of their appearance.

- □ Decision symbol: Alters the flow of execution as per the need of the user. Decision making is a part of all complex set of instructions. It so happens at times that we may need to skip certain instructions and jump to a specific statement. Such a requirement is taken care of by the decision symbol. Figure 3 shows three different ways in which a decision symbol can be used in a flowchart:

![](img/5d422ba7108ffdf64376be51eaf0c459_23_0.png)

Each of these representations is used in specific conditions only.

- □ Flow lines: Indicates which instruction to execute at any given moment of time. The flow of instructions is very important when the solution is to be converted into a computer program. The machine needs to know exactly which step or instruction it has to perform next. The flow lines in a flowchart using arrow heads indicate which instruction needs to be executed next. While drawing a flowchart, we must see to it that the flow lines do not intersect with each other. Avoiding intersections helps in understanding the flow of instructions clearly, although it may not be possible to remove the intersection of flow lines completely for a complex problem.

- □ Connector: Solution of a complex problem is lengthy most of the times. To draw a flowchart for such problems, we need more than one page. It becomes mandatory in such cases to see that the flow of the solution does not go haywire. Connector helps the designer in identifying the flow across the pages.

### Benefits and Drawbacks of a Flowchart

The tools like flowchart allow the user to device solution faster. However, the use of tools has its own benefits and drawbacks. Let's now discuss some of the benefits and drawbacks of using a flowchart as a solution design tool.

The benefits of using a flowchart are as follows:

- It is easy to understand because of limited symbols used
- It provides convenient and easy approach to represent a solution to a problem
- It assists the user in reviewing and correcting the solution
- It allows us to generate multiple solutions for a problem
- It allows us to compare the various solutions generated

The drawbacks of using a flowchart are as follows:

- It becomes time-consuming with flowcharts to represent a complex and large problem.
- It can require redrawing an entire flowchart in case of a minor change in the logic.
- It does not have any standards to represent the details of data that should be shown in the flowchart. Therefore, two flowcharts for a same problem may vary in details.

### Guidelines to Draw a Flowchart

There are no standardized rules to design a flowchart. However, we have tried to give a guideline to assist the user in improving the flowchart design. These guidelines are mentioned as follows:

1. Concentrate on the problem
2. Identify the inputs, outputs, and constraints
3. Limit the details to minimum
4. Do not design or use your own symbols in a flowchart
5. Use language that is easy to understand
6. Select appropriate naming conventions for the variables used
7. Be consistent with the naming conventions throughout the solution
8. Keep the drawing sequence from left to right and top to bottom
9. Avoid intersections, rather use connectors wherever possible
10. Always keep in mind that a flowchart is only a representation tool. The solution is always devised by us.

### Writing an Algorithm

Another popular approach to manually solve a problem is an algorithm. The techniques of a flowchart and an algorithm are used alternatively according to the convenience of the user. An algorithm is a sequence of finite logical steps required to perform a specific task. The term algorithm originated from the name of a Persian mathematician named Al-Khwarizmi.

Designing a flowchart or an algorithm is an art that requires a lot of thinking. Two well-known approaches used by programmers to formulate an algorithm are *stepwise refinement* and *divide and conquer*. In the stepwise refinement method, we initially design an algorithm with minimum details. Then, as and when needed, further details are added step by step to it such that the final solution is obtained. In the divide-and-conquer method, a complex task is simplified by breaking it into several numbers of subtasks, which are less complex but similar in nature. For example, we need to find maximum of 100 numbers. Instead of directly going for the solution, we break the task to find maximum of two numbers first, and then using the solution devised, we find maximum of 100 numbers.

Let’s now write an algorithm for the problem of voting eligibility, which is shown in the following box:

```
Step 1: Start
Step 2: Define CAge, CStatus
Step 3: Accept value of CAge
Step 4: If CAge >= 18 go to step 5
         Else go to step 8
Step 5: Accept value of CStatus
Step 6: If CStatus = Indian go to step 7
         Else go to step 8
Step 7: Print Eligible to Vote go to step 9
Step 8: Print Not Eligible to Vote
Step 9: Stop
```

The flow of an algorithm is always sequential, which means that step 2 should come only after step 1 unless and until the user implicitly changes the flow. The implicit change of flow can be seen in step 4. The execution of step 5 depends on the result of the condition in step 4. If the condition is not satisfied, we directly execute step 8 and all the steps from 5 to 7 are skipped. The user needs to handle the change of flow in the sequence carefully. The preceding example had a scenario of forward jump. At times, we also have to jump backward. For example, if we are at step 6, and due to some conditions we jump to step 3, then it is known as backward jump.

## Properties of an Algorithm

Similar to a flowchart, no standard convention have been defined for writing an algorithm. However, we have provided a list of properties that a good algorithm should satisfy:

- **Definite**: Precisely defined such that each step in the set of instructions has only one meaning.
- **Effective**: All operations should be carried out exactly in finite time limit.
- **Finite**: An algorithm should always have finite number of steps. After completion of these finite steps, the algorithm should stop.
- **Input**: Algorithm may have zero or more inputs.
- **Output**: Algorithm may have one or more outputs.

The next section provides some examples for solving problems using the flowchart and algorithm methods.

# Examples

As we have learned about the three different techniques of solving problems, let’s now work on some problems. In this section, we have provided the solutions using techniques of flowchart and algorithm. The user is free to select any of these techniques as per the requirement and liking to design a solution.

## Example 1:

Mr. Ramesh has purchased a rectangular-shaped land that is 150 m in length and 200 m in breadth. Calculate the area of the land.

### Solution 1:

- a. Using a flowchart, the area of the land can be calculated as follows:

The formula to compute the area of a rectangular surface is: Area = Length × Breadth

Keeping this formula in mind, we can devise a solution using the flowchart and algorithm.

We will use three variables, namely, area, length, and breadth, to solve this problem.

Figure 4 shows the flowchart to calculate the area of the rectangular surface:

![](img/5d422ba7108ffdf64376be51eaf0c459_26_0.png)

▲ Figure 4: Flowchart to Calculate the Area of the Rectangular Surface

Figure 4 shows that the two variables length and breadth have been assigned constant values of 150 and 200, respectively. Therefore, every time we use this flowchart, the output of area available will always be 30,000 m². In addition, note that the flow execution starts at top and flows down toward bottom.

- b. Using an algorithm, the area of the land can be calculated as follows:

The following box shows the algorithm method to solve the given problem:

```
Step 1: Start
Step 2: Define length, breadth, area
Step 3: length = 150
Step 4: breadth = 200
Step 5: area = length × breadth
Step 6: Print value of area
Step 7: Stop
```

The flowchart and algorithm created to calculate the area of the rectangular surface are considered to be static solution. The reason for calling the solution a static
