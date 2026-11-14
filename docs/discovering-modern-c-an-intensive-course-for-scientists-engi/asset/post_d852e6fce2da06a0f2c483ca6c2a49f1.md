
corresponding matrix—or part of this column. Conversely, a row vector can be extracted from a matrix with an integer as a row index and a range for the columns.

This is an interesting example of how to deal with the limitations as well as the possibilities of C++. Other languages have ranges as part of their intrinsic notation; e.g., Python has a symbol : for expressing ranges of indices. C++ does not provide such a symbol, but we can introduce a new type—like MTL4's range—and define the behavior of operator[] for this type. This leads to an extremely powerful mechanism!

## Extending Operator Functionality

Since we cannot introduce new operators into C++, we define new types and give operators the desired behavior when applied to those types. This technique allows us to provide a very broad functionality with a limited number of operators.

The operator semantics on user types must be intuitive and must be consistent with the operator priority (see an example in §1.3.10).

Back to our algorithm. We store the result of the solver in a vector and then we assign it to a matrix column. In fact, we can assign the triangular solver's result directly:

```
Inv[trange(0, n)][k] = upper_trisolve(A, unit_vector(k, n));
```

The range of all indices is predefined as tail:

```
Inv[tail][k] = upper_trisolve(A, unit_vector(k, n));
```

Next, we explore some mathematical background. The inverse of an upper triangular matrix is also upper triangular. Thus, we only need to compute the upper part of the result and set the remainder to 0—or the whole matrix to zero before computing the upper part. Of course, we need smaller unit vectors now and only sub-matrices of A. This can be nicely expressed with ranges:

```
Inv = 0;
for (unsigned k= 0; k < n; ++k)
    Inv[trange(0, k+1)][k]=        upper_trisolve(A[trange(0, k+1)][trange(0, k+1)],
                       unit_vector(k, k+1));
```

Admittedly, the trange makes the expression hard to read. Although it looks like a function, trange is a type, and we just created objects on the fly and passed them to the operator[]. As we use the same range three times, it is shorter to create a variable (or a constant) for it:

```
for (unsigned k= 0; k < n; ++k) {
    const trange r(0, k+1);
    Inv[r][k]= upper_trisolve(A[r][r], unit_vector(k, k+1));
}
```

This not only makes the second line shorter, it is also easier to see that this is the same range every time.

Another observation: after shortening the unit vectors, they all have the 1 in the last entry. Thus, we only need the size of the vector and the position of the 1 is implied:

```
dense_vector<double> last_unit_vector(unsigned n)
{
    dense_vector<double> v(n, 0.0);
    v[n-1] = 1;
    return v;
}
```

We choose a different name to reflect the different meaning. Nonetheless, we wonder if we really want such a function. What is the probability that we will need this again? Charles H. Moore, the creator of the programming language Forth, once said that “the purpose of functions is not to hash a program into tiny pieces but to create highly reusable entities.” All this said, we prefer the more general function that is much more likely to be useful later.

After all these modifications, we are now satisfied with the implementation and go to the next function. We still might change something at a later point in time, but having it made clearer and better structured will make the later modification much easier for us (or somebody else). The more experience we gain, the fewer steps we will need to achieve the implementation that makes us happy. And it goes without saying that we tested the inverse_upper repeatedly while modifying it.

Now that we know how to invert triangular matrices, we can do the same for the lower triangular. Alternatively we can just transpose the input and output:

```
Matrix inverse_lower(Matrix const& A)
{
    Matrix T(trans(A));
    return Matrix(trans(inverse_upper(T)));
}
```

Ideally, this implementation would look like this:

```
Matrix inverse_lower(Matrix const& A)
{
    return trans(inverse_upper(trans(A)));
}
```

The explicit creation of the two Matrix objects is a technical artifact.5 With future C++ standards or later versions of MTL4, we will certainly not need this artifact any longer.

Somebody may argue that the transpositions and copies are more expensive. In addition, we know that the lower matrix has a unit diagonal and we did not exploit this property, e.g., for avoiding the divisions in the triangular solver. We could even ignore or omit the diagonal and treat this implicitly in the algorithms. This is all true. However, we prioritized here the simplicity and clarity of the implementation and the reusability aspect over performance.6

We now have everything to put the matrix inversion together. As above, we start with checking the squareness:

```
Matrix inverse(Matrix const& A)
{
    const unsigned n = num_rows(A);
    assert(num_cols(A) == n); // Matrix must be square
}
```

Then, we perform the LU factorization. For performance reasons this function does not return the result but takes its arguments as mutable references and factorizes in place. Thus, we need a copy of the matrix and a permutation vector of appropriate size:

```
Matrix PLU(A);
dense_vector<unsigned> Pv(n);
lu(PLU, Pv);
```

The upper triangular factor PU of the permuted A is stored in the upper triangle of PLU. The lower triangular factor PL is (partly) stored in the strict lower triangle of PLU. The unit diagonal is omitted and implicitly treated in the algorithm. We therefore need to add the diagonal before inversion (or alternatively handle the unit diagonal implicitly in inversion).

```
Matrix PU(upper(PLU)), PL(strict_lower(PLU) + matrix::identity(n, n));
```

The inversion of a square matrix according to Eq. (A.1) can then be performed in one single line:7

```
return Matrix(inverse_upper(PU) * inverse_lower(PL) * permutation(Pv));
```

In this section, we have seen that most of the time we have alternatives for how to implement the same behavior—most likely you have had this experience before. Despite our possibly giving the impression that every choice we made is the most appropriate, there is not always THE single best solution, and even while trading off pros and cons of the alternatives, one might not come to a final conclusion and just pick one. We also illustrated that the choices depend on the goals; for instance, the implementation would look different if performance was the primary goal.

This section showed as well that that non-trivial programs are not written in a single sweep by an ingenious mind—exceptions might prove the rule—but are the result of a gradually improving development. Experience will make this journey shorter and more direct, but we will not write the perfect program at the first go.

## A.4 Class Details

### A.4.1 Pointer to Member

Pointers to Members are class-local pointers that can store the address of a member relative to the class:

```
double complex::* member_selector = &complex::i;
```

The variable `member_selector` has the type double complex::*; a pointer to a double within the class complex. It refers to the member i (which is public in this example).

With the operator .* we can access the member i of any complex object and likewise with ->* that member for a pointer to complex:

```
double complex::* member_selector = &complex::i;

complex c(7.0, 8.0), c2(9.0);
complex *p = &c;

cout << "c's selected member is " << c.*member_selector << '\n';
cout << "p's selected member is " << p->*member_selector << '\n';

member_selector = &complex::r; // focus on another member
// point to another complex
p = &c2;

cout << "c's selected member is " << c.*member_selector << '\n';
cout << "p's selected member is " << p->*member_selector << '\n';
```

Class-related pointers can also be used to choose a function out of a class's methods during run time.

### A.4.2 More Initialization Examples

An initializer list can end with a trailing , to distinguish it from a listing of arguments. In the example above, it did not change the interpretation of the argument list. Here are some more combinations of wrapping and listing:

```
vector_complex vi = {2};
vector_complex vd{{2}};

vector_complex v2 = {2, 3};
vector_complex v2d = {{2, 3}};
vector_complex v2cd = {{2, 3}, };
vector_complex v2cd = {{2, 3 }, };
vector_complex v2cd = {{2, 3}, {}};
vector_complex v2cd = {{2, 3}, {{2}, 3}}};

vector_complex v3 = {2, 3, 4};
vector_complex v3d = {{2, 3, 4}};
vector_complex v3cd = {{2, 3}, 4};
```

The resulting vectors are

```
v1 is [{2,0}]
vd is [{2,0}]

v2 is [{2,0}, {3,0}]
v2d is [{2,3}]
v2dc is [{2,3}]
v2cd is [{2,3}]
```
