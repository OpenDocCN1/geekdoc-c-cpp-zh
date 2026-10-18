# FIGURE 10.4

Structure of the ℓ₁ℓ₂ℓ₃ iteration space with valid and invalid iterations shown.

Adding threads to the ℓ₁ loop would give an MPI/OpenMP hybrid code that could scale to use O(1000) coprocessors with 2000 parallel tasks per coprocessor. Although this sounds like a great idea, the problem with this setup is that the triangular structure of the nested loops would lead to load imbalance in the ℓ₁ loop, which is visualized in Figure 10.5 for four threads. Imbalanced loops in OpenMP are typically handled through the use of dynamic scheduling or task-based parallelism. In our experiments, we found that these approaches suffered from poor cache behavior and low levels of data reuse, due to an inability to bind particular groups of parallel tasks to the same core. Furthermore, this approach only puts a plaster over the problem and does not address the underlying algorithmic issue.

An ideal solution is to flatten the entire ℓ₁ℓ₂ℓ₃ loop nest into a one-dimensional iteration space and divide the iterations between threads as evenly as possible. OpenMP provides the collapse pragma to do precisely this; however, it cannot be used in cases like ours where there are dependencies between loop bounds. We instead choose to manually restructure the loop such that it can be run from a specified start ℓ₁ℓ₂ℓ₃ triple to a specified end triple, as shown in Figure 10.6. This way, the work assigned to a given parallel task on the coprocessor can be represented neatly by six bounds: (lower_l1, lower_l2, lower_l3, upper_l1, upper_l2, upper_l3).

To determine these bounds we first execute a “trial run” of the entire loop nest to count the total number of iterations N. Next, we evenly divide the iterations between our P parallel workers, spreading the remainder across the first N mod P workers. Finally, another pass through the loop records the ℓ₁ℓ₂ℓ₃ bounds for each of the workers, based on the number of iterations assigned to them. This gives an

Valid (ℓ₁, ℓ₂) and ℓ₃

Valid (ℓ₁, ℓ₂) but invalid ℓ₃