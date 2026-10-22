# Abstract

Based on the concept of the active rule set, this chapter presents a multiplexed mixed-signal architecture for high-speed fuzzy controller chips. The proposed architecture consists of a programmable analog core which implements the active rule, a RAM memory which stores the parameters (global rule set) and a selection circuitry to identify the input subregion and retrieve the proper parameters from the memory. Thus, the global controller surface response is realized through dynamic programming and multiplexing of the analog core. This architecture can be programmed or trained by a set of input-output data pairs by means of a simple hardware-oriented learning rule which does not need to compute derivatives. The chapter presents also the circuit building blocks needed for implementation of the proposed architecture and illustrates the performance of the whole system through a chip realized in 0.7µm CMOS technology.

# 2.1. Introduction

Fuzzy controllers are used to map a multidimensional input signal x = {x1, x2, ... xM}T onto a scalar output y, in accordance to a well-defined nonlinear relationship [1],

y = f(x)  (2.1)

In control applications the inputs are usually called facts, the output action, and the mapping law surface response. For instance, a fuzzy controller for a washing machine must univocally set the water level (action) as a nonlinear function (surface response) of the clothes’ mass, the water impurity, and the time differential of impurity (facts) [2].

Fuzzy controllers employ the procedure of fuzzy logic inference[1] to construct the surface response. Some characteristic features of this procedure are [4][5]:

+   - The surface response, which is a global model predicting the system behavior for any input, is obtained as a composition of local functions, each one predicting this behavior only for inputs comprised in a limited region of the input space.
+   - These local functions represent insights in the system operation, and are described through inference rules of the type,