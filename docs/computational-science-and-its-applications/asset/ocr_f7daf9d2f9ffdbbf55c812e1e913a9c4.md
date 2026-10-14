# 2

# Industrial Applications of Optimal Control for Partial Differential Equations on Networks: Reduction and Decomposition Methods Applied to the Discrete–Continuous Control of Gas Flow in Complex Pipe Systems

Günter Leugering

# CONTENTS

+   2.1 Introduction...............................................................................25
+   2.1.1 Modeling of Gas Flow in a Single Pipe......................................................25
+   2.1.2 Network Modeling ......................................................................26
+   2.2 Optimal Control Problems and Outline.......................................................28
+   2.2.1 Time Discretization ...................................................................29
+   2.3 Domain Decomposition...................................................................32
+   2.4 Domain Decomposition for Optimal Control Problems................................34
+   2.4.1 Optimal Control on the Decomposed System: A Jacobi-Type Procedure ......34
+   2.4.2 Decomposition of the Optimality System for Continuous Controls with Fixed Switching Structure s ...........................................................35
+   2.4.3 Virtual Controls .......................................................................36
+   References......................................................................................38

# 2.1 Introduction

# 2.1.1 Modeling of Gas Flow in a Single Pipe

The aim of this contribution is to provide an exemplary road map—in a nutshell—from a given industrial application, here the control of gas networks, which is far too complex for a direct approach, to a problem that can be actually handled using well-known methods in control theory. This road map involves hierarchies of models, time discretization, reduction of space–time optimal control problems to static ones by way of instantaneous controls. A second objective is to introduce into network modeling what appears to be a tool that is becoming more and more important. Finally, as networks in industrial or civil applications are typically very complex, decomposition techniques are critical for the numerical handling. This reduction is done here by an iterative non-overlapping domain decomposition of the network and the corresponding optimal control problem. Similar