
![](img/65953ea584e494f3d396b2252cb5ea53_464_0.png)

## Fig. 16.12

The above graph has 8 nodes in which A is the source vertex and H is the destination vertex. First, we need to determine the paths that exist between the two nodes, A and H. They are:

- ADCFH and the length of this path is 14
- ABEFH and the length of this path is 13
- ABEH and the length of this path is 5.

From this, we can find the shortest path between the source vertex, A, and the destination vertex, H. The path is ABEH, which constitutes the minimum length of 5.

A program for finding the shortest path for a graph is as follows:

```c
/* SHORTEST PATH */
#include <stdio.h>
#define size 10
#define infinity 9999

int a[size][size];
int m[size][size];
int i,k,j;
int n;

void Input ();
void Short ();
void Output ();

/* Input function */

void Input()
{
    printf("\n Input the number of vertices: ");
    scanf("%d", &n);
    printf("\n Please enter the adjacency matrix\n");
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
{
    scanf("%d", &a[i][j]);
}
printf("\n");
}
printf("\n Adjacency matrix: \n");
for (i = 0; i < n; i++)
{
    for (j = 0; j < n; j++)
    {
        printf(" %i", a[i][j]);
    }
    printf("\n");
}

/* Output function */
void Output()
{
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            printf(" %d", m[i][j]);
        }
        printf("\n");
    }
}

/* Shortest path function */
void Short()
{
    /* Initialization of matrix m */
    for (i = 0; i < n; ++i)
    {
        for (j = 0; j < n; ++j)
        {
            if (a[i][j] == 0)
                m[i][j] = infinity;
            else
                m[i][j] = a[i][j];
        }
    }
    printf("\n Adjacency matrix after replacing zeros by very large value");
    Output();

/* Shortest path evaluation start from here */
for ( k = 0; k < n; k++)
{
    for ( i = 0; i < n; i++)
    {
        for ( j = 0; j < n; j++)
        {
            if ( m [i][k] <= m [i][k] + m [k][j] )
                m [i][j] = m [i][j];
            else
                m [i][j] = m[i][k] + m [k][j];
        }
    }
    printf("\n STEP %d \n", k);
    Output();
}
}

/* Function main */
void main()
{
    Input();
    Short();
    printf("\n The shortest path matrix is: \n");
    Output();
}
```

## POINTS TO REMEMBER

- 1. Each item in a binary tree has two links: one to a left member, and another to a right member.
- 2. A tree is a recursive (i.e. self-repeating) data structure, and recursive programming techniques are popularly used with trees.
- 3. A tree can be traversed in three major ways: In-order tree traversal, Pre-order tree traversal, Post-order tree traversal.
- 4. A graph is a set of nodes (also called as vertices) and a set of arcs (also called as edges).
- 5. A graph can be represented as an array or as a linked list in C.
- 6. If a graph is to be represented as a linked list then there are two types of list nodes, a header node (also called as graph node), and a list node.

## Review Questions and Exercises

- 16.1 Explain Binary tree in detail.
- 16.2 Discuss the graph representation in C in brief.
- 16.3 Discuss the various C operations that can be associated with the graph in the form of a linked list. Explain this with an example.

## State whether the following statements are True or False

- (a) Each data item (a through g) in a tree is called as a sub-tree.
- (b) Any portion of a tree (e.g. a-b-c) is called as a node.
- (c) A node that does not have any sub-tree is called as a terminal node.
- (d) Accessing a tree is called as the process of tree traversal.
- (e) Items of a tree must be accessed, inserted or deleted in a specific order.
- (f) A tree is a recursive data structure.
- (g) Set of nodes of a graph can also be called as edges.
- (h) A graph is connected if there is a path between any two nodes of the graph.
- (i) If a graph is represented as a linked list then there are three types of list nodes.
- (j) A header node contains the actual information of the node, a pointer to the next node, as well as a pointer to an arc.
- (k) A list node contains a pointer to a node and a pointer to the previous arc.

## Answers to True and False Questions

- (a) False      (b) False      (c) True      (d) True      (e) True
- (f) True      (g) False      (h) True      (i) False      (j) True
- (k) False      (l) False      (m) True

## UNIT VIII

## Chapter 17

## Sorting and Searching Techniques

### 17.1 INTRODUCTION

Information retrieval is one of the key features expected out of a computerized system. Given a telephone number getting the name and address of the subscriber, given a policy number showing the policy details are all some of the widely used retrieval practices. Basically, the process of retrieval involves searching a collection of well-organized data in a faster manner which must be capable of throwing the result almost instantaneously to the querying person. In order to be faster, the retrieval process has to be very efficient. Also, the data must be so arranged that it assists the retrieval process. The retrieval as we have been talking so far is called searching while the organizing of data is achieved through sorting. We will discuss these two aspects in this chapter.

### 17.2 SORTING

As we saw in the last section, the term sorting means bringing some orderliness in the data, which are otherwise not ordered. Consider a simple scenario—you are going to the railway station to board a train. The train, which you are supposed to board, is at platform 10. Assume that the railway station does not follow an ordered platform numbering scheme. Because of this the platforms are numbered in the fashion—8, 5, 2, 1, etc. Will it not take more time for you to locate the platform, which you are looking for? On the other hand, if the platform numbers are arranged like 1, 2, 3, etc. finding the 10th platform is an easier task. Thus, an ordered data makes the searching process efficient and easier. The term sorting refers to the process of bringing orderliness in the data.

Many sorting methods are advocated. Each method has its own advantages and disadvantages. Often a designer or a developer is puzzled as to which method is best and efficient. The efficiency could be measured in terms of memory usage, time taken to sort, CPU usage, etc. We are more concerned about the quickness of the algorithm. The next section answers this question.

### 17.2.1 Sorting Efficiency

The efficiency of sorting algorithms is measured using the O-notation (called Big O). The letter O stands for "order of". Let us understand what we mean by this notation. Consider an algorithm, which can sort n numbers in 50 seconds on a Pentium II PC. The same algorithm can run in 40 seconds on a Pentium III PC. Here the reduction in the time is not due to an increase in the efficiency of the algorithm but due to the configurational change in the PC in which it is getting executed. Hence the reduction in time is not attributable to the efficiency of the algorithm but to that of the machine. Hence we need an altogether different scale to measure the efficiency of an algorithm. The answer is the O-notation. It is intended to measure the performance of the algorithm based on the number of inputs it receives.

Let us understand some mathematics behind the O-notation. Consider a general quadratic equation of the form an² + bn + c = 0. In this form, let us assume the values of a, b and c to be 0.5, 0.25 and 0.12 respectively. The equation now becomes: f(n) = 0.5n² + 0.25n + 0.12

What will happen to this function, as n gets larger and larger? This would mean that n would contribute more to the expression yielding higher values. You can also eventually see that the term n² will significantly contribute to the value of f(n). Hence the terms n and the constant are not very important. The O-notation depends on this.

The notation identifies the most contributing term in the expression and throws out the other terms. We categorize the O-notation based on these dominant terms to create various classes of functions to measure an algorithm's efficiency. Some of the widely used classes are O(1) – Constant, O(n) – linear, O(n³) – polynomial, O(2ⁿ) – Exponential and O(log n) – logarithmic. The corresponding tabular form is shown in Table 17.1.

## Table 17.1 O-notation analysis

| n | O(1) | O(n) | O(log n) | O(n log n) | O(n²) | O(n³) |
|---|---|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 2 | 1 | 2 | 1 | 2 | 4 | 8 |
| 4 | 1 | 4 | 2 | 8 | 16 | 64 |
| 8 | 1 | 8 | 3 | 24 | 64 | 512 |
| 16 | 1 | 16 | 4 | 64 | 256 | 4096 |

Let us now understand what Table 17.1 means?

- **O(1)**—this means that an algorithm will run for a constant amount of time irrespective of the size of input it receives. Whatever be the size of the input you give, the algorithm will run for the same amount of time to give the result. Some examples are push to stack, pop from stack.
- **O(n)**—this means that the amount of time the algorithm will take to complete is directly proportional to the size of the input. If the size of the input is large, the time taken to complete the process will increase. Consider a typical case of finding the sum of numbers in an array. If the array size increases, the time taken to compute the sum also increases.
- **O(n²)**—this means that the amount of time the algorithm will take to complete increases by n² if you increase the size of the input by n. Certain sorting algorithms (which we will see shortly) like bubble sort, insertion sort have this.
