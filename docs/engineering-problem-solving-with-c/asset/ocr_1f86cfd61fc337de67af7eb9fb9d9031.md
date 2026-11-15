# # TWO-DIMENSIONAL ARRAYS

# ## CHAPTER OUTLINE

+   - Objectives
+   - 8.1 Two-Dimensional Arrays
+   - 8.2 Problem Solving Applied: Terrain Navigation
+   - 8.3 Two-Dimensional Arrays and the `vector` Class
+   - 8.4 Matrices
+   - 8.5 Numerical Technique: Solution to Simultaneous Equations
+   - 8.6 Problem Solving Applied: Electrical-Circuit Analysis
+   - 8.7 Higher-Dimensional Arrays
+   - Summary, Key Terms, C++ Statement Summary, Style Notes, Debugging Notes, Problems

# ## OBJECTIVES

+   In this chapter, we develop problem solutions containing:
+   - matrix computations
+   - input from data files
+   - functions to compute sums and averages
+   - techniques for solving a system of simultaneous equations
+   - vectors to implement the concept of two-dimensional arrays

# ### 8.1 Two-Dimensional Arrays

A set of data values that is visualized as a row or column is easily represented by a one-dimensional array. However, there are many examples in which the best way to visualize a set of data is with a grid or a table of data.

Suppose we wanted to display a table of temperature values recorded at eight-hour intervals over a period of four days. The values could be displayed as shown in the following array which has four rows corresponding to the number of days and three columns corresponding to the number of temperatures recorded during a 24-hour period:

```
row 0 --> 50 70 60
row 1 --> 48 78 62
row 2 --> 51 69 60
row 3 --> 52 78 63
         col 0 col 1 col 2
```