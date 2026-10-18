

## 2.4 Representing and Running Algorithms

At last, in this section, we will implement a C++ program. It will ask a user to enter a number and, after checking whether it is a positive value, display the number’s square root. That is, if 16 is entered, 4 will be displayed, and so on. However, before we go to the C++ code, which is one of the forms of representing algorithms, let’s first reflect on what an algorithm is and the ways to express it.

In this section, we will learn the following:

- What an algorithm is, and how to represent it
- What the Unified Modeling Language (UML) is, and what can be represented with UML activity diagrams

An algorithm describes steps for execution. Algorithms are frequently encountered not only in computer science but also in daily life. For example, fire alarm instructions in every office provide the steps to be followed in the event of a fire; selecting a given program on a dishwasher specifies the steps to be performed by the machine to clean our precious glass; etc.

Much depends on the abstraction level at which we are operating. The concept of abstraction in computer science is frequently encountered: when representing algorithms, it simply tells what level of details is necessary. In some cases, especially if we wish to view the entire form of an algorithm, a more general coarse level is preferred, and an image can be used: more specifically, a diagram that uses commonly agreed-on symbols. Such diagrams are used in many domains, such as electric engineering and architecture. In computer science, we are lucky to have a common system of diagrams under the umbrella of UML (see http://uml.org and www.visual-paradigm.com). UML is much more than a simple collection of common symbols – this framework facilitates the entire software development process shown in Figure 2.4. We will return to it many times. However, let's now present the UML activity diagram that represents the steps required by our program, shown in Figure 2.5.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_33_0.png)

Basically, there are two types of symbols in Figure 2.5. Actions are in rounded rectangles, and decision blocks are in diamonds. Lines ending in arrows show the control flow. Therefore, such diagrams are sometimes called flow charts. Usually, in simple diagrams, the main flow proceeds from top to bottom. But observe that the flow can be easily redirected, forming loops in execution. There are also black circular symbols denoting the beginning and end of an action, respectively. Although simple and straightforward, the ending symbol reminds us about a very important problem in algorithm design: the *stop problem*. Put simply, this means a well-designed algorithm should have well-defined stop conditions, i.e. it should not hang up forever in an undefined state. Some software, such as operating systems, operates in an indefinite loop; however, it should never find itself in an undefined state or behavior.

Note that in Figure 2.5, the whole program can be seen in one glance. But at the same time, the steps express certain general actions, such as “Compute sqrt(x),” without in-depth details. This is what we call the coarse level or, more generally, a *top-down* approach. On the other hand, going into detail means entering finer and finer levels: that is, “going down” the design. Usually, this involves more symbols; to avoid clutter, these are usually presented in separate diagrams. Nevertheless, in some tasks, it is possible to start from the details. Such a *bottom-up* approach is much less useful in our domain and usually results in designs in which upper-level components do not interface well.

Yet another way to present algorithms is in the form of the pseudo-code. This is a mixture of simple computer commands interspersed with more general statements, usually written in the form of human-readable commands or short sentences. Algorithm 2.1 presents this approach.

**Algorithm 2.1**  An algorithm for computing the square root of a real value expressed in pseudo-code (a mixture of programming commands and human-readable commands).

|  |  |
|---|---|
| **Input:** | A real value x |
| **Output:** | Square root of x |
| 1 | if x ≥ 0 |
| 2 | &nbsp;&nbsp;&nbsp;&nbsp;Print `sqrt ( x )` |
| 3 | else |
| 4 | &nbsp;&nbsp;&nbsp;&nbsp;Print an error message |

The ultimate representation comes in the form of computer code, such as that presented in Listing 2.1. This can be translated into a computer-executable format and launched.

The code in Listing 2.1 does what was outlined in Figure 2.5 and in Algorithm 2.1.

# 2.4.2 Using Online Compilers

Before we explain each line of code in Listing 2.1, we can compile it and run its executable with the help of an online platform with a C++ compiler, as shown in Figure 2.6.² However, when typing, we may make a mistake, in which case the code will not compile, and the platform will display an error message from the compiler. This should be carefully read to see what the problem is, in order to fix it. But sometimes the precise position of an error can be difficult to determine, and the real culprit may be a few lines above the place indicated by the compiler. So, we should also check the preceding lines.

> ² For example, to quickly evaluate short programs, we can use one of the following platforms: [http://ideone.com](http://ideone.com), [https://wandbox.org](https://wandbox.org), [http://coliru.stacked-crooked.com](http://coliru.stacked-crooked.com), [https://repl.it](https://repl.it), [www.onlinegdb.com](http://www.onlinegdb.com), or [http://cpp.sh](http://cpp.sh).

