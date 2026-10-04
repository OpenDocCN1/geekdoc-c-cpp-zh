# #3

# # MATRICES AND ARRAYS

![](bbox=[0.171, 0.431, 0.355, 0.568])

By now, you have a solid handle on using vectors in R. A *matrix* is simply several vectors stored together. Whereas the size of a vector is described by its length, the size of a matrix is specified by a number of rows and a number of columns. You can also create higher-dimensional structures that are referred to as *arrays*. In this chapter, we'll begin looking at how to work with matrices before increasing the dimension to form arrays.

# ## 3.1 Defining a Matrix

The matrix is an important mathematical construct, and it's essential to many statistical methods. You typically describe a matrix $A$ as an $m \times n$ matrix; that is, $A$ will have exactly $m$ rows and $n$ columns. This $A$ will have a total of $mn$ entries, with each entry $a_{i,j}$ having a unique position given by its specific row ($i = 1, 2, \dots, m$) and column ($j = 1, 2, \dots, n$).