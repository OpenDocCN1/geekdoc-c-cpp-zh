It is also possible to further specialize this function if for some call sites the remaining arguments (or already partially evaluated function) have specific values. For the example in the previous figure (right), we could further propagate the value of N and create another data specialization version of this function as shown as follows:

```
void funcRelaxSelON16(){
int i, j;
for (j = 1; j <= 15; j++){
for (j = 1; j < 15; j++){
A[1][j] = (A[1-1][j]A[1+1][j]+A[1][j-1]+A[1][j+1])/4;
}
}
}
```

Given now the knowledge of the loop bounds the compiler can apply other transformations such as loop unrolling or scalar replacement to further improve the performance of this specific variant of the funcRelax function.

# 5.7.3 FUNCTION APPROXIMATION

If the resultant accuracy is adequate, the use of approximate functions instead of exact functions may increase performance, reduce power and/or energy consumption. The methods used for approximate computing of functions include:

+   • Lookup tables;
+   • Lookup tables and interpolation, e.g., generating the table by using the Ramer-Douglas-Peucker algorithm ;
+   • Lower cost functions;
+   • Iterative methods such as Taylor's series [17] and the Newton-Raphson method [18].

Lookup tables can be an efficient scheme to substitute functions such as the trigonometric functions. A function can be substituted by a table with values for a number of input values and the values not present in the table for a given number of inputs can be obtained by approximating to the closest ones or by interpolating between the two closest points. This is an effective and efficient method, especially in the context of custom hardware, but does not scale for nontrivial functions as this table can become quite large and infeasible for applications that target embedded systems.

An option to generate an approximation of a given function is to use the Ramer-Douglas-Peucker algorithm. This algorithm reduces the number of points in a curve by considering for each pair of points a line between them, and then identify a point between the two with the largest vertical distance to that line (this process is repeated a number of times while considering the addition of points under a certain maximum distance).