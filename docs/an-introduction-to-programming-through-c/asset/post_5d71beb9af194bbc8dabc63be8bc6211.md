
This may be called using the following main program.

```
main(){
    char a[40], b[40];
    cin.getline(a,40);
    cin.getline(b,40);
    cout << a << " " << compare(a,b) << " " << b << endl;
}
```

If you execute this program, it would expect you to type two lines. Say you typed:

```
Mathematics
Biology
```

then it would print out > and stop, because “Mathematics” appears after “Biology” in the dictionary order.

## 14.1.4 Address arithmetic

C++ programs processing char arrays often use arithmetic on addresses.

Suppose x is the name of an array of some type T. We have already said that x has value equal to the address of the zeroth element of the array. Suppose further that i is an integer expression. Then the expression

```
x+i
```

is valid in C++ programs, and has the value equal to the address of x[i]. Note that in general, a single element of type T may require some s bytes. Thus while x+i seems to be adding i to the address x, the actual value added is i*s because the address of x[0] and of x[i] differ by i*s and not just i. Indeed, in general, if x is of type T*, then x+i is the address obtained by adding i*s to the address denoted by x. Since this can be somewhat confusing, we have not discussed such address arithmetic so far.

However, if x is of type char*, then s equals 1. In that case, when we write x+i, we indeed mean the address obtained by adding i. So perhaps for this reason, address arithmetic is quite common in character processing. Thus the scopy function would more commonly be written as:

```
void scopy(char *destination, char *source){
    while(*source != '\0'){
        *destination = *source;
        destination++;
        source++;
    }
}
```

## 14.2 Two dimensional Arrays

Sequences of numbers are naturally represented as arrays. However, we will run into objects like matrices which are collections of elements described using two indices. For such cases, C++ provides two dimensional arrays.

Here is an example of how a two dimensional array might be defined:

```
double a[m][n];
```

This causes space for m*n variables of type double to be allocated. These variables are accessed as a[i][j] where we require 0 ≤ i < m, and 0 ≤ j < n. The variables are stored in the so called row major order in memory, i.e. in the order a[0][0], a[0][1], ... a[0][n-1], a[1][0], ... a[1][n-1], ... a[m-1][n-1]. The numbers m,n are said to be the first and second dimension of the array. We will also refer to them as the number of rows and the number of columns respectively.

Manipulating two dimensional arrays is similar to one dimensional – we commonly use a loop to go over each dimension. As an example, consider the problem of multiplying two matrices. Remember that if A is an m × n matrix, and B an n × p matrix, then there product is an m × p matrix C where

c_ij = Σ_{k=1}^{n} a_ik b_kj

where we have let the array indices start at 1, as is customary in Mathematics. The code below, of course, starts indices at 0. The code also shows how a two dimensional array can be initialized in the definition itself if you wish. The values for each row must appear in braces, and these in turn in an outer pair of braces.

```
double a[3][2]={{1,2},{3,4},{5,6}}, b[2][4]={{1,2,3,4},{5,6,7,8}}, c[3][4];
```

```
for(int i=0; i<3; i++)        // compute c = a * b.
    for(int j=0; j<4; j++){
        c[i][j] = 0;
        for(int k=0; k<2; k++)
            c[i][j] += a[i][k]*b[k][j];
    }
```

```
for(int i=0; i<3; i++) {        // print out c.
    for(int j=0; j<4; j++) cout << c[i][j] << " ";
    cout << endl;
}
```

### 14.2.1 Linear simultaneous equations

One of the most important uses of matrices and two dimensional arrays is to represent linear simultaneous equations. Say we are given simultaneous equations:

3x₂ + 5x₃ = 10
2x₁ + 6x₂ + 8x₃ = 38
7x₁ + 4x₂ + 9x₃ = 22

Then they can be conveniently represented by the matrix equation

[ 0 3 5 ]   [ x₁ ]   [ 10 ]
[ 2 6 8 ] × [ x₂ ] = [ 38 ]
[ 7 4 9 ]   [ x₃ ]   [ 22 ]

Denoting the matrix by A, the vector of unknowns by x and the right hand side vector by b, we have the matrix equation Ax = b in which we are to solve for x given A, b.

The direct way to solve a system of equations is by a process called Gaussian elimination², in fact a form of it called Gauss-Jordan elimination.

Observe first that if the matrix A was the identity matrix, i.e. aᵢᵢ = 1 and aᵢⱼ = 0 for all i, j ≠ i, then the problem is very easy. Multiplying out we would get x = b. Thus for this b is itself the solution. This suggests a strategy. We will make modifications to A, b such that the modifications do not change the solution of Ax = b. If at the end of the sequence of modifications, our matrix A becomes the identity matrix then the value of b at that time would itself be the solution.

It turns out that several operations performed on the system of equations (and hence A, b) indeed do not change the solutions to the system. One such operation is to multiply any equation by a constant. This is akin to multiplying a row of the matrix A and the corresponding element of the vector b by a (the same) constant. Another operation is to add one equation to another, and replace the latter equation by the result. In our example, say we add the first equation to the second. Thus we get the equation 2x₁ + 9x₂ + 13x₃ = 48. We replace the second equation with this equation. This is succinctly done in the matrix representation: we merely add the first row of A to the second row, and the first element of b to the second element of b. Thus the second row of A would then become [2 9 13] and the second element of b would become 48, while the other elements remained the same.

We now show how we can change A, b, without changing the solution, so that the first column of A becomes 1,0,0 (read top to bottom), i.e. identical to the first column of the identity matrix. The same process can then be adapted for the other columns.

- 1. If the coefficient of x₁ is zero in the first equation, pick any equation which has a non zero coefficient for x₁. Suppose the iᵗʰ equation has a non-zero coefficient for x₁. Then exchange equation 1 and equation i. This corresponds to exchanging row 1 and row i of A and also element 1 and element i of b. Doing this for our example we get:

[ 2 6 8 ]   [ x₁ ]   [ 38 ]
[ 0 3 5 ] × [ x₂ ] = [ 10 ]
[ 7 4 9 ]   [ x₃ ]   [ 22 ]

2. Divide the first equation by the coefficient of a11. We thus get

[ 1 3 4 ] [ x1 ]   [ 19 ]
[ 0 3 5 ] [ x2 ] = [ 10 ]
[ 7 4 9 ] [ x3 ]   [ 22 ]

3. For each i, add −a1i times the first equation to equation i. Say we do this for row 2. Thus we must add −a21 = 0 times the first row. So nothing need be done. So we then consider row 3. Since a31 = 7, we add -7 times the first equation to equation 3. Thus we now have:

[ 1   3    4 ] [ x1 ]   [ 19 ]
[ 0   3    5 ] [ x2 ] = [ 10 ]
[ 0 -17 -19 ] [ x3 ]   [ -111 ]

It should be clear that the above process would indeed make the first column identical to the first column of the identity matrix. In a similar manner, you should be able to get the other columns to match the identity matrix.

The first step in the above description deserves more explanation. Suppose you have managed to make the first j − 1 columns of A resemble the first j − 1 columns of the identity matrix. Now the first step above instructs you to find an equation in which the coefficient of xj is non-zero. For this, you should only look at equations j through n, and not consider the first j − 1 equations. This step may or may not succeed. It will not succeed if akj = 0 for all k = j … n. In this case, it turns out that the system of equations does not have a unique solution; it may have many solutions or no solutions at all. In this case you should report failure.

The code for doing all this is left as an exercise.

### 14.2.2 Two dimensional char arrays

We may define two dimensional arrays of chars, with initialization, which is of course optional. For example we could write:

```
char countries[6][20] = {"India","China","Sri Lanka","Nepal",
"Bangladesh","Pakistan"};
```

Here the first string, "India" is deemed to initialize the zeroth row, and so on for the six strings.

Applying only one index to the name of a two dimensional array returns the address of the zeroth element of the corresponding row. For character arrays, this is the way to refer to one of the strings stored. Thus countries[i] will return the address of the zeroth character of the ith string stored in the array, in other words, the address of the ith string. So if we write compare(countries[0], countries[1]), where compare is as defined in Section 14.1.3, it would return '<' as the result because India will precede Sri Lanka in the dictionary order.

Here is a program which has two arrays, countries which lists countries, and capitals which lists corresponding capitals. It takes as input a string from the keyboard. It prints out the name of the corresponding capital if the string is in the list of countries stored in countries. This check is made using our compare function.
