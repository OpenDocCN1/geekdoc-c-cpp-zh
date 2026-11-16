a correction in coordinate n - 1 of x'y(x) produces a correction in coordinate n - 1 - i of y(x). This version of Meggitt decoding allows the use of shift-registers whose internal stages do not need to be directly accessed and modified and allows for fewer wires in the circuit. For those interested in the circuit design, consult [21]. We illustrate this in the binary case by continuing with Example 4.6.6.

# Example 4.6.7

After computing the syndrome polynomials of y(x), xy(x), and x^2y(x), we conclude there is an error in coordinate 14 of x^2y(x), that is, coordinate 12 of y(x). Thus we modify x^7y(x) in coordinate 14 to obtain x^7y'(x) = x^2 + x^4 + x^9 + x^11 + x^12 (where y'(x) = 1 + x^4 + x^7 + x^9 + x^10 is y(x) corrected in coordinate 12). This changes the syndrome as well. Fortunately, the change is simple to deal with as follows. S(x^7y'(x)) = R_g(x)(x^7y'(x))) = R_g(x)(x^7y(x)) - R_g(x)(x^14 + x^14) = S(x^7y(x)) - R_g(x)(x^14) because x^7y'(x) = x^7y(x) - x^14 since we changed only coordinate 14 of x^7y(x). But S(x^7y(x)) - R_g(x)(x^14) = x + x^7 + x^4 + x^7 - x^7 = x^7 + x^4 + x^3 from Example 4.6.6 as R_g(x)(x^22) = R_g(x)(x^7) = x^7. Thus to get the new syndrome for x^7y'(x), we take S(x^7y(x)) and subtract x^7. This holds in general: namely, to obtain the new syndrome polynomial after error has been corrected, take the old syndrome and subtract x^7. This simple modification in the syndrome polynomial is precisely why the definition of syndrome S(u(x)) as R_g(x)(x^{k-1}u(x)) was given; had we used the more natural R_g(x)(u(x)) as the definition of the syndrome polynomial of u(x), we would have had a more complicated modification of the syndrome at this juncture. So we compute and obtain the following table:

| Syndrome of | Syndrome | Syndrome of | Syndrome |
| :--- | :--- | :--- | :--- |
| x^3y'(x) | x^2+x^4+x^5+x^6 | x^8y'(x) | x^3 |
| x^4y'(x) | x^3+x^5+x^6+x^7 | x^9y'(x) | x^4 |
| x^5y'(x) | 1 | x^{10}y'(x) | x^5 |
| x^6y'(x) | x | x^{11}y'(x) | x^6 |
| x^7y'(x) | x^2 | x^{12}y'(x) | x^7 |

We see that none of our syndromes is in the list from Step I until that of x^{12}y'(x). Hence we change coordinate 14 of x^{12}y'(x) = x + x^4 + x^7 + x^{11} + x^{12} to obtain x^{12}y''(x) = x + x^4 + x^9 + x^7 + x^{12} + x^{14} (where y''(x) = 1 + x^4 + x^4 + x^7 + x^9 + x^{10} is y(x) changed in coordinate 2). As above, the syndrome of x^{12}y''(x) is x^7 - x^7 = 0. We could stop here, if our circuit is designed to check for the zero syndrome polynomial. Otherwise we compute the syndromes of x^{13}y'(x) and x^{14}y'(x), which are both 0 and not on the list, indicating that the procedure should halt as we have considered all cyclic shifts of our received vector. So the correct vector is y''(x) and in fact turns out to be the vector output of the shift-register circuit used in this version of Meggitt decoding.

# Exercise 277 Verify the results in Example 4.6.7.

In the binary case where we correct only the high-order errors one at a time, it is unnecessary to store the error polynomial corresponding to each syndrome. Obviously the speed of our decoding algorithm depends on the size of the list and the speed of the pattern