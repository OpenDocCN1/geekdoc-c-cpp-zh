
## Problems

## Exam Practice!

## True/False Problems

Indicate whether the following statements are true (T) or false (F).

- 1. The use of registers within the ALU increases the overall speed of an operation. T F
- 2. Linking and loading is the step that prepares the object program for execution. T F
- 3. The accumulator is a part of the main memory unit that temporarily stores the values and results of arithmetic and logic operations. T F
- 4. A computer program is the implementation of an algorithm. T F

## Multiple-Choice Problems

Circle the letter for the best answer to complete each statement, or for the correct answer to each question.

- 5. Which of the following is not a computer language?
  - (a) C++
  - (b) Fortran
  - (c) Unix
  - (d) Java
  - (e) Basic
- 6. The size of each register in the ALU is
  - (a) dependent on the word size of the computer.
  - (b) dependent on the capacity of the RAM.
  - (c) dependent on the storage capacity of hard disk.
  - (d) always fixed at 64 bit.
- 7. Which of the following shows the right sequence for program execution?
  - (a) executing, loading, compiling, linking.
  - (b) compiling, linking, loading, executing.
  - (c) linking, loading, compiling, executing.
  - (d) loading, linking, compiling, executing.
  - (e) debugging, linking, loading, executing.
- 8. An algorithm refers to
  - (a) a step-by-step solution to solve a specific problem.
  - (b) a collection of instructions that the computer can understand.
  - (c) a code that allows us to type in text materials.
  - (d) stepwise refinement.
  - (e) a set of math equations to derive the problem solution.
- 9. Object code is
  - (a) the result of compiler operations on the source code.
  - (b) the process of obtaining information from the processor.
  - (c) a computer program.
  - (d) a process involving the listing of commands required to solve a specific problem.
  - (e) the result of the linking and loading process.

- 10. Convert the following binary numbers to octal.
  - (a) 101010101
  - (b) 100011011011001
  - (c) 11101001101
  - (d) 10001110011
  - (e) 111000000

- 11. Convert the following binary numbers to hexadecimal.
  - (a) 110011011001
  - (b) 1111000010110100
  - (c) 110101101
  - (d) 1100000000000011
  - (e) 1111111111

- 12. Convert the following decimal numbers to octal.
  - (a) 1292
  - (b) 607
  - (c) 9350
  - (d) 1000010
  - (e) 1111111

- 13. Convert the following numbers to base 10.
  - (a) 11010101₂
  - (b) 476₈
  - (c) 30AF₁₆
  - (d) 4103₅
  - (e) 1111111₆

## Additional Problems

The following problems combine an assignment in which you will learn more about one of the topics in this chapter with an opportunity to improve your written communication skills. (Perhaps your professor will even select some of the written reports for oral presentation in class.) Each report should include at least two references, so you will want to learn how to use library computers to locate reference information. Prepare your report using word-processor software. If you do not already know how to use a word processor, ask your professor for guidance or visit your university's Web site for links to resources on campus.

- 14. Write a short report on one of these outstanding engineering achievements:
  - Analytical Engine
  - Global Positioning Systems
  - Composite materials
  - Application satellites
  - Mars Orbital Camera
  - CAD/CAM
  - Fiber optics
  - CAT scans
  - A good starting point for finding references is the World Wide Web and your local library.

- 15. Write a short report on one of these engineering challenges:
  - Prediction of weather, climate, and global change
  - Computerized speech understanding
  - Mapping of the human genome
  - Improved vehicle performance
  - A good starting point for finding references is the NASA Web site: www.nasa.gov

- 16. Write a short report on an outstanding engineering achievement that is not included in the list given in this chapter. Past issues of Scientific American and the Web would provide some good ideas of recent achievements.

![](img/f2bfa570e453b020c16e048c79a3ea0e_50_0.png)

## ENGINEERING CHALLENGE: Vehicle Performance

Turboprop engines combine the power and reliability of jet engines with the efficiency of propellers. Turboprops use a gas turbine to turn a propeller. Their application has been limited to smaller aircraft because turboprop engines are most efficient at flight speeds under 500 mph. However, the engineering of new materials, blade shapes, and propellers continues to increase the speed and efficiency of the turboprop and the demand for the engine.

## SIMPLE C++ PROGRAMS

### CHAPTER OUTLINE

- Objectives
- 2.1 Program Structure
- 2.2 Constants and Variables
- 2.3 C++ Classes
- 2.4 C++ Operators
- 2.5 Standard Input and Output
- 2.6 Building C++ Solutions with IDEs: NetBeans
- 2.7 Basic Functions Included in the C++ Standard Library
- 2.8 Problem Solving Applied: Velocity Computation
- 2.9 System Limitations
- Summary, Key Terms, C++ Statement Summary, Style Notes, Debugging Notes, Problems

### OBJECTIVES

In this chapter we develop problem solutions containing:

- simple arithmetic computations
- user-supplied information from the keyboard
- information printed on the screen
- programmer-defined data types

### 2.1 Program Structure

In this section, we analyze the structure of a specific C++ program, and then we present the general structure of a C++ program. The program that follows was first introduced in Chapter 1; it computes and prints the distance between two points.

```cpp
/* ........................................................... */
/* Program chapter1_1 ........................................ */
/* ........................................................... */
/* This program computes the ............................... */
/* distance between two points. ............................ */
#include <iostream> // Required for cout, endl.
#include <cmath> // Required for sqrt()

using namespace std;

int main()
{
    // Declare and initialize objects.
    double x1(1), y1(5), x2(4), y2(7);
    double side1, side2, distance;

    // Compute sides of a right triangle.
    side1 = x2 - x1;
    side2 = y2 - y1;
    distance = sqrt(side1*side1 + side2*side2);

    // Print distance.
    cout << "The distance between the two points is "
         << distance << endl;

    // Exit program.
    return 0;
}
/*..................................................*/
```

We now briefly discuss the statements in this specific example; each of the statements is discussed in detail in later sections of this chapter.

The first five lines of this program contain **comments** that give the program a name (chapter1_1) and that document its purpose:

```
/*..................................................*/
/*                                                */
/*   Program chapter1_1                           */
/*                                                */
/*   This program computes the                    */
/*   distance between two points.                 */
/*                                                */
```

Comments may begin with the characters /* and end with the characters */ for multi-line comments, or may begin with the characters // and terminate at the end of the current line for single-line comments. A comment can be on a line by itself, or it can be on the same line as a statement; a comment beginning with the characters /* can extend over several lines.

Each of the comments here is a separate paragraph because each line begins with /* and ends with */. Although comments are optional, good style requires that comments be used throughout a program to improve its readability and to document the computations. In the text programs, we always use initial comments to give a name to the program and to describe the general purpose of the program; additional explanation comments are also included throughout the program. C++ allows comments and statements to begin anywhere on a line.
