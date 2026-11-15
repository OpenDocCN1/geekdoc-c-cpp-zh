Decomposition Outline. We used decomposition outlines in Chapters 1 and 2 to provide the first definition of a problem solution. This outline is written in sequential steps and can be shown in a diagram or a step-by-step outline. For very simple problems, such as the one that was developed in Chapter 2, we can go from the decomposition outline directly to the C statements:

# Decomposition Outline

+   1. Read the new value.
+   2. Compute the corresponding velocity and acceleration values.
+   3. Print the new velocity and acceleration.

However, for most problem solutions, we need to refine the decomposition outline into a description with more detail. This process is often referred to as a divide-and-conquer strategy, because we keep breaking the problem solution into smaller and smaller portions. To describe this stepwise refinement, we use pseudocode or flowcharts.

Refinement with Pseudocode and Flowcharts. The refinement of an outline into more detailed steps can be done with pseudocode or a flowchart. Pseudocode uses English-like statements to describe the steps in an algorithm, and a flowchart uses diagram to describe the steps in an algorithm. The fundamental steps in most algorithms are shown in Figure 3.1, along with the corresponding notation in pseudocode and flowcharts.

Pseudocode and flowcharts are tools to help us determine the order of steps to solve a problem. Both tools are commonly used, although they are not generally both used with the same problem. In order to give examples of both tools, some problem solutions will use pseudocode and others will use flowcharts; the choice between pseudocode and flowcharts is usually a personal preference. Sometimes we need to go through several levels of pseudocode or flowcharts to develop complex problem solutions; this is the stepwise refinement that we previously discussed. Decomposition outlines, pseudocode, and flowcharts are working models of the solution, and thus are not unique. Each person working on a solution will have a different decomposition outline and pseudocode or a flowchart description, just the C programs developed by different people will vary, although they solve the same problem.

# Structured Programming

A structured program is written using simple control structures to organize the solution to a problem. A simple structure is usually defined to be a sequence, a selection, or a repetition. A sequence structure contains steps that are performed one after another; a selection structure contains one set of steps that is performed if a condition is true, and another set of steps that is performed if the condition is false; and a repetition structure contains a set of steps that is repeated as long as a condition is true. We now discuss each of these simple structures, and use pseudocode and flowcharts to give specific examples.

Sequence. A sequence contains steps that are performed one after another. All the programs developed in Chapter 2 have a sequence structure. For example, the pseudocode for the program that performed the linear interpolation is as follows:

```
Refinement in Pseudocode
main:
    read f, a
    read c, f, c
    read b
    set f_b to f_a + b - a
                c - a   (f_c - f_a)
    print f_b
```