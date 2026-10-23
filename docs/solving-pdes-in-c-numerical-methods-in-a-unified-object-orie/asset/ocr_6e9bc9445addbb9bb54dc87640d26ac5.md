R_{i,j,k,l,m,n} \equiv |A|^{-1} (-1)^{i+j+k+l+m+n} \left| \left( \left( A^{[j,i]} \right)^{[k,l]} \right)^{[m,n]} \right| 
= (-1)^{i+j} |A|^{-1} |A^{[j,i]}| (-1)^{k+l} |A^{[j,i]}|^{-1} \left| \left( A^{[j,i]} \right)^{[k,l]} \right| 
\cdot (-1)^{m+n} \left| \left( A^{[j,i]} \right)^{[k,l]} \right|^{-1} \left| \left( \left( A^{[j,i]} \right)^{[k,l]} \right)^{[m,n]} \right| 
= A_{i,j}^{-1} \left( A^{[j,i]} \right)_{l,k}^{-1} \left( \left( A^{[j,i]} \right)^{[k,l]} \right)_{n,m}^{-1} 
= S_{i,j,k,l} \left( \left( \left( A^{[j,i]} \right)^{[k,l]} \right)^{-1} \right)_{n,m}

If, on the other hand, k > j > m, then one can still modify the above definition and revise its right-hand sides by replacing k by k − 1 to account for the row indexing in A^{[j,i]} that is different from the original row indexing in A due to the missing jth row. Alternatively, one could use the skew-symmetry discussed above to define

R_{i,k,j,l,m,n} \equiv - R_{i,j,k,l,m,n}.

The other possible orders of the triplets j, k, and m and i, l, and n are handled in the same spirit.

This tensor provides the Jacobian of S with respect to A:

\frac{\partial S}{\partial A} = \frac{\partial (|A| S / |A|)}{\partial A} 
= |A|^{-1} \frac{\partial (|A| S)}{\partial A} + |A| S \otimes \frac{\partial |A|^{-1}}{\partial A} 
= |A|^{-1} |A| R - |A| S \otimes |A|^{-1} A \,' 
= R - S \otimes A^t .

As a result, we have the following tensor of six indices:

\frac{\partial^2 A^{-1}}{\partial A^2} = \frac{\partial (S - A^{-1} \otimes A^{-t})}{\partial A} 
= R - S \otimes A^{-t} - \left( \left( \frac{\partial A^{-1}}{\partial A} \otimes A^{-t} \right)^t - A^{-1} \otimes \left( \frac{\partial A^{-1}}{\partial A} \right)^t \right).

We are now ready to calculate b''(e):

b'' = (w' w')' 
= w'' w' + w' w'' 
= ||w'||^2 + w' w'' 
= \left\| \left( \left( \frac{\partial A^{-1}}{\partial A} \right) A' \right)^t f \right\|^2 + w'^t \left( \left( \left( \frac{\partial^2 A^{-1}}{\partial A^2} \right) A' \right) A' \right) f + w'^t \left( \left( \frac{\partial A^{-1}}{\partial A} \right) A'' \right) f .