# Chapter 12

# Time optimal control

# 12.1 Introduction

There are numerous situations where time optimal control problems arise. For example, in startup of a chemical reactor, it is frequently desired to reach the desired state of operation as fast as possible. In operating a crane system, one frequently would like the trolley to reach a desired point in minimum time. In the drug displacement problem, it is desirable to reach some specified concentration of drugs in a patient’s bloodstream in minimum time. In the operation of a robot arm to deliver a payload to a certain location, we encounter the time optimal control problem. Therefore, a considerable amount of research effort has gone into solving the time optimal control problem. For linear systems, linear programming may be used to determine the minimum number of time steps to reach the desired state, but for high dimensional nonlinear systems the determination of time optimal control policy is generally very difficult.

In this chapter we wish to examine several approaches that have been used with IDP to solve some time optimal control problems.

# 12.2 Time optimal control problem

Let us consider the system described by the differential equation

d**x**/dt = **f**(x, u)  (12.1)

where the initial state **x**(0) is given. The state vector **x** is an (n × 1) vector and **u** is an (m × 1) control vector bounded by

α_j ≤ u_j ≤ β_j,   j = 1, 2, ⋯, m.  (12.2)

At the final time t_f the state variables must be at the desired values, i.e.,

h_i = x_i(t_f) − x_i^d = 0,   i = 1, 2, ⋯, n.  (12.3)