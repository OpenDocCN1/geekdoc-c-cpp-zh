# ### 6.6.1 Types of Membership Functions

In principle any function of the form A:X→[0,1] describes a membership function associated with a fuzzy set A that depends not only on the concept to be represented, but also on the context in which it is used. The graphs of the functions may have different shapes and may have specific properties. Whether a particular shape is suitable can be determined only in the application context. In certain cases, however, the meaning semantics captured by fuzzy sets is not too sensitive to variations in the shape, and simple functions are convenient. In many practical instances fuzzy sets can be represented explicitly by families of parameterized functions, the most common being the following:

+   1. Triangular Function
+   2. Γ -Function
+   3. S-Function
+   4. Trapezoidal Function
+   5. Gaussian Function
+   6. Exponential Function

The membership function definitions for the above mentioned common membership functions are given in the following sections:

# ### Triangular Function

The membership definition for a triangular function is given as:

```
```math
A(x) = \begin{cases}
0, & \text{if } x \le a \\
\frac{x-a}{b-a}, & \text{if } x \in [a,b] \\
\frac{c-x}{c-b}, & \text{if } x \in [b,c] \\
0, & \text{if } x \ge a
\end{cases} \tag{6.3}
```
```

where m is a modal value, and a and b denote the lower and upper bounds, respectively, for nonzero values of A(x). Sometimes it is more convenient to use the notation explicitly highlighting the membership functions' parameters; in this case,

```
```math
A(x; a, m, b) = \max\{\min[(x-a)/(m-a), (b-c)/(b-m)], 0\} \tag{6.4}
```
```