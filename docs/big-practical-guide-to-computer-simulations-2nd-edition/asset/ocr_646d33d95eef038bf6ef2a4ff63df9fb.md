# Chapter 3

# Software Engineering

Performing simulations or other large-scale software projects is not only a matter of skillful coding. A lot depends on the organization of the design and the way of programming. Also the methods used for testing and the organization of actually running the simulations and performing the data analysis have a strong influence on the success of a project. This is in particular true, if several people are involved in the project. In this chapter, strategies for performing software projects are discussed. The corresponding computer-science field is called *software engineering*. An introduction to software engineering is given, for example, in Ref. [Somerville (1989)], while a more practical approach is presented in Ref. [Kernighan and Pike (1999)].

First, a general introduction to software engineering is given (Sec. 3.1). In Sec. 3.2, some hints are given on how to structure the source-code documents efficiently, such that programming, debugging and documentation are facilitated. In the Sec. 3.3, the *subversion* tool is presented, which facilitates the management of any kind of projects, also software projects, in particular if several people cooperate.

# 3.1 How to manage a (simulation) project

When you are creating a program, you should start never immediately writing the code. In this way, only tiny software projects such as scripts can be completed successfully. Otherwise your code will probably be very inflexible and contain several hidden errors which are very hard to find. If several people are involved in a project, it is obvious that a considerable amount of planning is necessary.

But even when you are programming alone, the first step you should