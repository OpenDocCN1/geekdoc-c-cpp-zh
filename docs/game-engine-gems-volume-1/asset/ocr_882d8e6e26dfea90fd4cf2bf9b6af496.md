# 12.1 Introduction

In recent years, much effort has been devoted to integrating real physics into virtual worlds like those found in video games. Some of these techniques, such as collision detection, are now very familiar to game developers and have been widely integrated into game physics engines. This is not the case for fluids. Simulating fluid dynamics well in virtual environments is generally a challenge. The primary difficulty is that there is no analytic solution to the Navier-Stokes equations describing the fluid dynamics. In general, the computer graphics community uses a grid or particle system to simulate a fluid. This gem uses an Eulerian 3D method on a grid to compute the fluid velocity field.

One of the first studies on simulating fluids in computer graphics was done by Foster and Metaxas [2]. Their work is based on a paper published by Harlow and Welch [3]. A great summary of work on fluids can be found in a recent book [1]. We have implemented the method of Foster and Metaxas [2] to compute the fluid dynamics, so the fluid domain is discretized into voxels. The velocity field computation process is as follows:

+   - The velocity source (or an exterior force), which we call the *blower*, is placed inside the fluid domain (for example, on a selected face of a voxel).

+   - The fluid velocity on all voxel faces in the fluid domain is calculated by solving the Navier-Stokes equations. These velocities can be stored in a file for future use, or precomputed before the simulation starts.

The use of fluid dynamics in video games is very expensive in terms of computing time. For greater performance, we precompute the physics of the fluid. The key idea is to precompute the steps that take a long time. Once the time-consuming steps in the calculation have been done, we use these data to simulate the fluid