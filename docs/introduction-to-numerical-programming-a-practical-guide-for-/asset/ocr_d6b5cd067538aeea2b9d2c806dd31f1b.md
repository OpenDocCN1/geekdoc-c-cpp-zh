The goal of step $k$ ($k = 1,2,\ldots,n-1$) is to eliminate the unknown $x_k$ from the last $n-k$ equations and to bring the system to the form:

\begin{bmatrix} 1 & a_{12}^{(1)} & \cdots & a_{1k}^{(1)} & a_{1k+1}^{(1)} & \cdots & a_{1n}^{(1)} \\ 0 & 1 & \cdots & a_{2k}^{(2)} & a_{2k+1}^{(2)} & \cdots & a_{2n}^{(2)} \\ \vdots & \vdots & \ddots & \vdots & \vdots & & \vdots \\ 0 & 0 & \cdots & 1 & a_{kk+1}^{(k)} & \cdots & a_{kn}^{(k)} \\ 0 & 0 & \cdots & 0 & a_{k+1k+1}^{(k)} & \cdots & a_{k+1n}^{(k)} \\ \vdots & \vdots & & \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & 0 & a_{nk+1}^{(k)} & \cdots & a_{nn}^{(k)} \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_k \\ x_{k+1} \\ \vdots \\ x_n \end{bmatrix} = \begin{bmatrix} b_1^{(1)} \\ b_2^{(2)} \\ \vdots \\ b_k^{(k)} \\ b_{k+1}^{(k)} \\ \vdots \\ b_n^{(k)} \end{bmatrix}. \tag{7.11}

The updated coefficients of the pivot row $k$ are given by

\begin{cases} a_{kk}^{(k)} = 1, \\ a_{kj}^{(k)} = a_{kj}^{(k-1)}/a_{kk}^{(k-1)}, \quad j = k+1,\ldots,n, \\ b_k^{(k)} = b_k^{(k-1)}/a_{kk}^{(k-1)}, \end{cases} \tag{7.12}

while the new elements of the nonpivot rows below the pivot line read:

\begin{cases} a_{ik}^{(k)} = 0, \\ a_{ij}^{(k)} = a_{ij}^{(k-1)} - a_{ik}^{(k-1)} a_{kj}^{(k)}, \quad j = k+1,\ldots,n,\ i = k+1,\ldots,n, \\ b_i^{(k)} = b_i^{(k-1)} - a_{ik}^{(k-1)} b_k^{(k)}. \end{cases} \tag{7.13}

It can be noticed that, at step $k$, one actually modifies only the elements delimited by the row and column $k$ in the bottom-right part of the coefficient matrix, the rest of the elements remaining unchanged as compared to the previous step.

At the last elimination step, $k = n$, one only divides the last equation by the last pivot element $a_{nn}^{(n-1)}$ to create a 1 on the diagonal:

\begin{cases} a_{nn}^{(n)} = 1, \\ b_n^{(n)} = b_n^{(n-1)}/a_{nn}^{(n-1)}. \end{cases} \tag{7.14}

Finally, the system takes the form

\begin{bmatrix} 1 & a_{12}^{(1)} & \cdots & a_{1k}^{(1)} & a_{1k+1}^{(1)} & \cdots & a_{1n}^{(1)} \\ 0 & 1 & \cdots & a_{2k}^{(2)} & a_{2k+1}^{(2)} & \cdots & a_{2n}^{(2)} \\ \vdots & \vdots & \ddots & \vdots & \vdots & & \vdots \\ 0 & 0 & \cdots & 1 & a_{kk+1}^{(k)} & \cdots & a_{kn}^{(k)} \\ 0 & 0 & \cdots & 0 & 1 & \cdots & a_{k+1n}^{(k+1)} \\ \vdots & \vdots & & \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & 0 & 0 & \cdots & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_k \\ x_{k+1} \\ \vdots \\ x_n \end{bmatrix} = \begin{bmatrix} b_1^{(1)} \\ b_2^{(2)} \\ \vdots \\ b_k^{(k)} \\ b_{k+1}^{(k+1)} \\ \vdots \\ b_n^{(n)} \end{bmatrix}, \tag{7.15}