# 10.4.2 Operating Characteristics of RAR designs via Monte Carlo Simulation

By simulating a RAR trial (say, 10,000 times) one can generate empirical distributions of important design characteristics, such as treatment allocation proportion, number of treatment failures, etc. This can enable a comparison of various randomization designs under different experimental scenarios. Supplemental program ch10.4.2.sas can be used to simulate operating characteristics of five types of randomization procedures:

+   I. Completely Randomized Design (CRD)

II. Permuted Block Design (PBD)

III. SMLE procedure

IV. DBCD(γ = 2) procedure

V. ERADE procedure

For procedure I, every patient is randomized between E and C with probability 1/2. For procedure II, treatment assignments are made at random in blocks of size $2m_0$ (where $m_0$ is a pre-specified positive integer) that treatment balance is achieved after every cohort of $2m_0$ patients. For procedures III, IV, and V, first permuted block randomization, and the remaining patients are randomized between E and C using according to a RAR algorithm with RSIHR target allocation $ho = PRSIHR = \frac{\sqrt{E}}{\sqrt{E\|+\sqrt{C}}$

The design characteristics include the following:

+   - Allocation proportion $N_E(n)/n$;
- Number of trial subjects assigned to superior treatment: $N_E(m)\{p_E \ge p_C\} + N_C(m)\{p_E < p_C\}$;