

for equations (12.5) and (12.6). Consider the use of reduction variables. Consider how to use tasks and task groups to price the following option set: {plain call, plain put, cash-or-nothing, supershare call, supershare put}. You can use lambda functions and captured variables to implement the payoff functions, for example:

```
// Supershare option (Haug 2007 page 176)
double KL = 90.0;
double KH = 110.0;

auto Payoff = [&](double S)-> double
{ if (S < KH && S >= KL) return S/KL; return 0.0; };
```

5. Write parallel code to compute vega, theta and rho as given in equation (12.14). It might be a good idea to first draw a task graph to find sources of potential parallelism. Then decide on which parallel design pattern to apply. Measure speedup. Are the sequential and parallel results the same?

When we say ‘parallel C++’ we refer to both the functionality in C++ Concurrency and in PPL.

3. (Parallelising Finite Difference Schemes)

The objective of this exercise is to parallelise the process of comparing the accuracy of finite difference schemes (as discussed in Chapters 20 to 22) using task groups and parallel_for. In order to scope the problem we compare the option price, delta and gamma produced by the Crank–Nicolson and ADE schemes with regard to accuracy. Some requirements are:

+   R1: Compute option price, delta and gamma by the Crank–Nicolson and ADE schemes.
+   R2: Produce an error report showing how the two methods differ from each other with respect to accuracy.
+   R3: In this version, use a fixed set of option data.
+   R4: Compare the schemes for a range of step sizes in the underlying space and in time directions.

Answer the following questions:

+   a) Create a context diagram for this problem and describe the data flow from source input data to desired output.
+   b) Use the results in part a) to find potential concurrency and then create a task dependency graph consisting of tasks and the data flow between them.
+   c) Implement and test the task dependency graph.
+   d) We relax the requirement R3 in order to support randomly generated input data. What impact has this new requirement on the task dependency graph and its implementation?

4. (Parallel Aggregation)

PPL supports concurrency::parallel_reduce that computes the sum of all elements in a given range by computing successive partial sums. It can also compute the result of successive partial results obtained from using an arbitrary specified binary operator. It is semantically similar to std::accumulate but it requires the binary operation to be associative and an identity value is needed instead of an initial value. It has three overloaded versions based on the number of input arguments and we discuss a specific one. The parameters are:

+   The begin and end iterators (STL style) of the range to be reduced, in other words the iteration bounds.
+   - The value of the reduction’s identity element (0 for addition, 1 for multiplication; for aggregate set union the identity element is the empty set).
+   - The function object that can be applied on a subrange of an iterator range to produce a local partial aggregation. The return value is the local partial result from the first phase of the Parallel Aggregation pattern.
+   - The reduction function that combines the partial results that each subrange has computed.

Answer the following questions:

+   a) Apply this algorithm to the examples in Section 30.4 (for example) and compare it with other aggregation algorithms in that section with regards to efficiency and understandability.
+   b) Determine what the following piece of code is doing:

```
std::vector<long> vec2(2000, 4);
int sumV = 0;
vec2[600] = 4;
auto d = concurrency::parallel_reduce(std::begin(vec2),
std::end(vec2), sumV); std::cout << "Parallel_reduce PPL sum : "
<< d << '\n';
```

How does its performance compare to other aggregation algorithms?

+   c) Compare the performance of PPL aggregation algorithms with that of OpenMP:

```
// OpenMP and reduction variable
M = 8;
std::vector<int> vecA(M, 2);
int sum2 = 0;
int prod2 = 1;
int i;
#pragma omp parallel for private(i), reduction (+ : sum2),
reduction (* : prod2)
for (long i = 0; i < vecA.size(); ++i)
{ // vec is some vector

    sum2 += vecA[i];
    prod2 *= vecA[i];
}
std::cout << "Parallel OpenMP sum and product: "
    << sum2 << ", " << prod2 << '\n';
```

In the case of floating-point data the order in which thread-specific values are combined is non-deterministic in general and hence the final result may not be precisely the same as when the reduction is performed serially. This is caused by the fact that floating-point operations can introduce roundoff errors. This could be a cause of concern in computational finance applications where reproducible and accurate results are needed. We may even decide not to parallelise the specific loop if the error resulting from roundoff becomes unacceptable.

Investigate this anomaly using PPL and OpenMP. Take examples to exhibit the effect of roundoff error.

# CHAPTER 31

# Monte Carlo Simulation, Part I

> Analyse a little, design a little, program a little.
> —Grady Booch

> Why are software process models important? Primarily because they provide guidance on the order (phases, increments, prototypes, validation tasks) in which a project should carry out its major tasks. Many software projects have come to grief because they pursued their various development and evolution phases in the wrong order.
> —Barry Boehm

## 31.1 INTRODUCTION AND OBJECTIVES

In this chapter and in Chapter 32 we initiate a project to design and implement an option pricing software framework using the Monte Carlo method. In order to reduce the scope and keep the presentation manageable we focus on the pricing of a range of one-factor options whose underlying variable is described by stochastic differential equations (SDEs). In general, analytical solutions are not available and we resort to numerical methods, in particular the finite difference method (FDM).

Some of the goals of this chapter are:

-   - To develop a process to design the software framework that produces a series of software prototypes with each prototype containing more functionality than its predecessor. In this case we attempt to simulate the lifecycle of real software projects (for example, market-driven products or in-house development projects).
-   - To show how the techniques that we introduced in Chapter 9 can be applied to the design of flexible and extendible code. In this chapter we show how to achieve this goal in a bottom-up manner by creating a series of software prototypes while in Chapter 32 we formalise the design when we present a predefined architecture that can be instantiated to reproduce the results in this chapter as a special case.
-   - Rather than using only the object-oriented style to design the software framework (as in Duffy and Kienitz, 2009), we augment this style with generic and functional styles that are now supported in C++.

We introduce and describe the following software prototypes:

-   - P1: A *monolithic program* (‘ball of mud’) that prices one-factor plain call and put options using the explicit Euler method. This prototype functions as a requirements document and *feature list* (in the sense of the discussion in Section 9.3.2) that can be extended in later prototypes.
-   - P2: A solution based on policy-based design (PBD) and templates as discussed in Section 9.3.4.
-   - P3: This is a variation of solution P2 in which class hierarchies based on subtype/dynamic polymorphism are replaced by the *Curiously Recurring Template Pattern* (CRTP). CRTP is described in Chapter 21 (in particular, Section 21.7.2) where we apply it to PDE models.
-   - P4: A design based on the approach that we introduced in Section 6.8 that will be presented in Chapter 32. In this case we try to play down the role of classes and objects and focus more on system decomposition and the implementation of inter-component interface contracts using universal function wrappers (the class `std::function`).

There is no unique way to choose which prototypes to develop or in which order. However, there is a wrong way and a right way. In practice, customer and market requirements will determine how a software project evolves. We now discuss this topic.

### 31.1.1 Software Product and Process Management

From a software process viewpoint, the approach in this chapter is similar to that in the *Spiral Model* (Boehm, 1986). The spiral model is a risk-driven process for software projects. Based on the unique risk patterns of a given project, the spiral model guides a team to adopt elements of one or more process models, such as incremental, waterfall or evolutionary prototyping. The basic principles are (www.wikipedia.org):

+   a) Focus is on risk assessment and on minimising project risk by breaking a project into smaller segments and providing more ease of change during the development process, as well as providing the opportunity to evaluate risks and weigh consideration of project continuation throughout the life cycle.
+    b) Each cycle involves a progression through the same sequence of steps, for each part of the product and for each of its levels of elaboration, from an overall concept-of-operation document down to the coding of each individual program.
+    c) Each trip around the spiral traverses four basic quadrants: (1) determine objectives, alternatives, and constraints of the iteration, (2) evaluate alternatives; identify and resolve risks, (3) develop and verify deliverables from the iteration and (4) plan the next iteration. We begin each cycle with an identification of stakeholders and their “win conditions”, and we end each cycle with review and commitment.

We see Boehm’s *Spiral Model* as complementing the approach taken in Chapter 9. It is a *process driver* that helps deliver more functionality after the completion of each cycle. It is not the only model around and it may not be the best one in all cases. A discussion of the relative merits of the competing software development processes (such as *Agile* and *Waterfall*) is outside the scope of this chapter. See Exercise 1 where we discuss the spiral model from a project management viewpoint.

