# # Chapter 5

# # Iterative Control Statements: Loops

# ## 5.1 Introduction

Often we come across requirements where same set of operations need to be executed multiple times to generate the required output. For example, we need to repeatedly perform multiplication to calculate factorial of a number; we need to repeatedly draw lines to construct a polygon and so on. Each time the operation may use different data sets for evaluation; hence, results of each of the individual operations may be different, but the expression that defines the operation is always the same. To give an example, although lines are drawn repeatedly to construct a polygon, the [x, y] coordinates (data values) giving start and end of a line may be different each time. Immaterial of the data used in each stage, we will still consider this as an repetitive execution of the same operation. We can form an expression to draw line from (x1, y1) to (x2, y2) in terms of variables x1, y1, x2 and y2. We can change the value of these variables each time before repeating draw line operation so as to ensure that each line is created at a different position and the consolidated result is a polygon.

To elaborate what we just said, let us try to construct a triangle using a series of drawLine operations. A triangle can be visualized as a consolidated effect of three lines drawn at correct positions. Hence, the execution of the drawLine operation must be repeated thrice. Before we proceed further, readers are requested to note that the detailed study of computer graphics is out of the scope of this textbook, however, we still give an example to draw a triangle using some abstract operation drawLine to understand the concept of loops in C/C++.

Let us assume that the expression to draw a single line from point (x1, y1) to point (x2, y2) be as shown below:

```
`drawLine[(x1,y1),(x2,y2)]`
```

Drawing a triangle using this operation will now be a three-step process, which is elaborated as below:

**Stage 1:** Initialize variables x1=50, y1=0, x2=0, y2=50 and execute the operation

```
`drawLine[(x1,y1),(x2,y2)]`
```

The line drawn in this step is shown in Figure 5.1.