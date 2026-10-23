![](bbox=[0.15, 0.12, 0.85, 0.46])

# FIGURE 19.1 Context diagram for minimisation algorithms

requirements. It is important to understand the data flow in the system in which each module receives input and produces output.

The main steps in the core process of finding the minimum are:

+   - Choose the function to be minimised.
+   - Define the termination criterion for the algorithm.
+   - Choose a solver and compute the minimum.
+   - Present the ongoing and final results of the computations.

The design of the system in Figure 19.1 is based on the following interfaces (the rationale here is that we emulate each interface with one function using std::function):

```
// Interfaces.hpp
//
// The specifications for the components with interval search methods.
// These will be the interfaces between the mediator and the other
// components in the system context diagram.
//
// (C) Datasim Education BV 2017

#ifndef Interfaces_HPP
#define Interfaces_HPP

#include <functional>
#include <tuple>
```