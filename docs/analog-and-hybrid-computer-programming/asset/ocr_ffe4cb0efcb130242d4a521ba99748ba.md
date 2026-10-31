![](bbox=[0.15, 0.08, 0.88, 0.38])

Fig. 6.77. Divergent behaviour of the computer setup shown in figure 6.76

direct approach might convert (6.62) into (6.68) by means of a preliminary step performed on a stored-program digital computer.

Nevertheless, a purely analog implementation of this approach can be achieved by computing the error resulting from an initial setting of x by

$$\mathbf{A}^T \mathbf{A}\tilde{x} - \mathbf{A}^T b = \tilde{\zeta}$$

and setting

$$\dot{\tilde{x}} = -\tilde{\zeta}$$

as before. Factoring out $\mathbf{A}^T$ yields

$$\mathbf{A}^T(\mathbf{A}\tilde{x} - \tilde{b}) = \mathbf{A}^T\tilde{\zeta} = \tilde{\zeta} = -\dot{\tilde{x}}.$$

This can be now split into two sets of coupled equations:

$$\varepsilon_i = \sum_{j=1}^{n} a_{ij}x_j - b_i \qquad (6.69)$$

$$\dot{x}_i = - \sum_{j=1}^{n} a_{ji}\varepsilon_i \qquad (6.70)$$

with $1 \le i \le n$. These equations can now be transformed into an analog computer setup as shown in figure 6.78. Compared with the simple program shown in figure 6.75, this one requires twice the number of coefficient potentiometers (note the transposed indices!) and the number of summers. This seemingly profligate use of computing elements is nevertheless justified given the very good convergence behaviour of this setup.

Figure 6.79 shows the complete setup using this advanced indirect method for solving the $3 \times 3$ system shown in equation 6.67 and the rapidly converging results