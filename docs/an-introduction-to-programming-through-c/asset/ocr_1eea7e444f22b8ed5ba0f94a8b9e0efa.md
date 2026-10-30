or their square and so on. Such estimates cannot be used to decide how many seconds will be needed to execute the program. However, if we know that one program sorts in time proportional to n, and another in time proportional to n², then for large n, the first algorithm will be better. Usually, we care about the time taken only when the problem size, n in this case, is large. So our qualitative analysis, whether the time is proportional to n or n² is quite useful.

To analyze the time for SelSort we must first analyze the time for argmax. The function argmax simply goes over the subarray on which it is called and finds the maximum. It examines every element and thus its time can be considered to be proportional to L, the second argument. In selection sort, we merely call argmax several times, with the value of the second argument being n, n−1, n−2 and so on till 2. Thus we can see that the time is proportional to

n + (n − 1) + (n − 2) + … + 2 = Σ_{i=2}^{n} i ≈ n²/2

Thus we estimate the time taken by Selection sort as being proportional to n², where n is the length of the array being sorted.

# 13.6 Representing Polynomials

A program will deal with real life objects such as stars, or roads, or a collection of circles. It might also deal with mathematical objects such as polynomials. How to represent polynomials on a computer and perform operations on them are therefore important questions.

A polynomial A(x) = Σ_{i=0}^{n−1} a_i x^i is completely determined if we specify the coefficients a0, …, a_{n−1}. Thus to represent the above polynomial we will need to store these coefficients. This most conveniently done in an array.⁴ We use an array a of length n and store a_i in a[i].

Next comes the question of how we operate on polynomials. It is natural to ask; suppose we have two arrays representing two polynomials A(x), B(x). Can we construct the representation of the polynomials C(x), D(x) obtained by adding and multiplying A(x), B(x) respectively?

First we know that the sum will have degree n − 1 because the addends A(x), B(x) have degree n − 1. Thus the array c that we can use to represent the polynomial C(x) must be defined as float c[n]. We also know that c_i = a_i + b_i. Thus we know how to set the elements of the array c as well.

```
for(int i=0; i<n; i++)  c[i] = a[i] + b[i];
```

Can we write this as a function addp which adds two polynomials? The polynomials to be added will be passed as arguments. What about the result polynomial? We could allocate a new array inside the function addp, but this array cannot be returned back – it gets destroyed

> ⁴There is a simple rule here – if a collection of objects is described using one subscript, use a one dimensional array, which is what we have studied so far. If a collection of mathematical object is described using two subscripts, say the entries of a matrix, then we will need two dimensional arrays, which we will see later.