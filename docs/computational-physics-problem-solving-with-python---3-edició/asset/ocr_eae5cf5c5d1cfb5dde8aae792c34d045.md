3. *Diffusion* It is well known that light molecules diffuse more quickly than heavier ones. See if you can simulate diffusion with your MD simulation using a Lennard–Jones potential and periodic boundary conditions (Satoh, 2011).

+   a) Generalize the velocity-Verlet algorithm so that it can be used for molecules of different masses.
+   b) Modify the simulation code so that it can be used for five heavy molecules of mass $M = 10$ and five light molecules of mass $m = 1$.
+   c) Start with the molecules placed randomly near the center of the square simulation region.
+   d) Assign random initial velocities to the molecules.
+   e) Run the simulation several times and verify visually that the lighter molecules tend to diffuse more quickly than the heavier ones.
+   f) For each ensemble of molecules, calculate the RMS velocity at regular instances of time, and then plot the RMS velocities as functions of time. Do the lighter particles have a greater RMS velocity?

4. As shown in Figure 18.7, simulate the impact of a projectile with a block of material.