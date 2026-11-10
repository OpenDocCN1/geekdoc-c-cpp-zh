# # Chapter 12

# ## Evolutionary Algorithms Implemented Using MATLAB

Solved MATLAB programs are given in this chapter to illustrate the implementation of Evolutionary Computation in problems such as optimization, proportional-derivative controller, multiobjective optimization, and minimization of functions.

# ### 12.1 Illustration 1: Differential Evolution Optimizer

```
```matlab
%**************************************************
% Script file for the initialization and run of the differential
% evolution optimizer
%**************************************************

% F_VTR    "Value To Reach" (stop when ofunc <F_VTR)
  F_VTR = -10;

% I_D      number of parameters of the objective
%          function
  I_D = 2;

% FVr_minbound,FVr_maxbound   vector of lower
% and bounds of initial population
%          the algorithm seems to work especially
% well if [FVr_minbound,FVr_maxbound]
% covers the region where the global minimum is
%          expected
%*** note: these are no bound constraints!! ***
  FVr_minbound = -3*ones(1,I_D);
  FVr_maxbound = 3*ones(1,I_D);
  I_bnd_constr = 0; % 1: use bounds as bound
% constraints, 0: no bound constraints
```
```