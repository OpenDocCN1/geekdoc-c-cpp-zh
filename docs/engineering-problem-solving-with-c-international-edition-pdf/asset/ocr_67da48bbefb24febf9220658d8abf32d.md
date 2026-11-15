# ## 3. HAND EXAMPLE

By using the resistor values and the voltage values, a system of three equations can be defined, using this rearranged set of equations from the definition of the problem:

(R_1 + R_2)i_1 - R_2i_2 + i_3 = V_1,
-R_2i_1 + (R_2 + R_3 + R_4)i_2 - R_4i_3 = 0,
0i_1 - R_4i_2 + (R_4 + R_5)i_3 = -V_2.

For example, suppose that each of the resistor values is 1 ohm and that both of the voltage sources are 5 volts. Then the corresponding set of equations is the following:

2i_1 - i_2 + i_3 = 5,
-i_1 + 3i_2 - i_3 = 0,
0i_1 - i_2 + 2i_3 = -5.

Once the system of equations is determined, the solution follows the steps illustrated in the hand example in the previous section. For this set of equations, the solution is i_1 = 2.5, i_2 = 0, and i_3 = -2.5.

# ## 4. ALGORITHM DEVELOPMENT

We first develop the decomposition outline, because it breaks the solution into a series of sequential steps:

*Decomposition Outline*

+   1. Read the resistor values and the voltage values.
+   2. Specify the coefficients for the system of equations.
+   3. Perform Gauss elimination to determine currents.
+   4. Print currents.

In step 1 we read the information necessary to specify the circuit values, and in step 2 we use this information to specify the coefficients for the system of equations. Then, in step 3, we develop the details of the elimination and back-substitution steps. To keep the main function short and readable, functions are used for both the elimination and the back substitution. The structure chart for this solution was used in Figure [?].

The coefficients of the simultaneous equations are stored in a two-dimensional array; the solution is stored in a one-dimensional array. The variable index indicates which variable is being eliminated in the elimination function; this variable ranges from 0 to n - 1 to match the subscripting in C++.

The algorithm for Gauss elimination is a difficult algorithm to describe in pseudo-code because of the detailed subscripting that must be specified. Go through this pseudo-code with the hand example to be sure that you are comfortable with the subscript handling.