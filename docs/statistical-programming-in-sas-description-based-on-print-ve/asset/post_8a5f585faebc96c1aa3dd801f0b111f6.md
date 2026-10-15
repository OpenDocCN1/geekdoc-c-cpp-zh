
## Display 11.3 (continued)

```
*put second column of C on diagonal;
    D = DIAG( C[,2] );
    print '2nd column of C into a diag, matrix (D) =DIAG(C[,2]) ->' D;
*make a vector out of the diagonal;
    CC= VECDIAG(D);
    print 'convert diagonal (of D) into vector (CC) = VECDIAG(D) ->' CC;
*put C next to itself - column binds C with itself;
    E = C || C;
    print 'Column bind C with itself yielding E = C||C =' E;
*put a row of 2s below C - row bind;
    F = C // SHAPE(2,1,3);
    print "Row bind C with vector of 2s (F) = C // SHAPE(2,1,3) ->" F;
* . . . also adds (2 2 2) as another row on C;
    F2 = C // J(1, 3, 2);
    print "Using J(nrow,ncol,value) to add row to C (F2) = " F2;
*create a 6x6 matrix [C // C // C] || [C // C // C];
    K = REPEAT(C,3,2);
    print '6x6 matrix = ' K;
quit;
```

Executing this program generates the output in Display 11.4.

## Display 11.4 Output from summarizing, extracting, shaping, and manipulating vectors and matrices

```
2x3 example matrix C = {1 2 3,4 5 6} -
    C
      1   2   3
      4   5   6
1x3 column sums of C = C[+,] =
    C1
      5   7   9
2x1 row sums of C = C[,+] =
    C2
      6
     15
extract 2nd column of C into new vector (F) = C[,2] -
    F
      2
      5
put 2nd column of C into a diagonal matrix (D) = DIAG(C[,2]) -
    D
      2   0
      0   5
convert diagonal (of D) into vector (CC) = VECDIAG(D) =
    CC
      2
      5
```

In Display 11.5, using elementwise operations and multiplying matrices are illustrated.

```
PROC IML;
C = {1 2 3,4 5 6}; * a 2x3 matrix;
D = {1, 1, 1}; * a 3x1 column vector;

* matrix multiplication - C post-multiplied by D;
row_sum = C*D;
print 'row_sum = ' row_sum;

* raise each entry of columns 2 & 3 of C to the third power then multiply by 3 and add 3;
G = 3+3*(C[2:3]##3);
print '3 + 3*(col2&3)^3 (G) = ' G;

* raise each entry of C to itself;
H = C##C;
print 'raise each C element to itself (H) = C##C - ' H;

* multiply each entry of C by itself;
J = C # C;
print 'elementwise multiplication of C with itself (J) = C#C - ' J;
quit;
```

Executing this program generates the output in Display 11.6.

```
row_sum = 6

15

G

27 84

378 651

H

1 4 27

256 3125 46656

J

1 4 9

16 25 36
```

In Display 11.5, a column vector has entries all equal to one in a matrix multiplication calculation. The assignment D = {1, 1, 1} created this column vector. One of the following assignments can be used to construct this column vector:

```
c1 = shape(1,3,1)
c3 = T({1 1 1})
c4 = T({[3] 1})
```

Vector c1 uses the shape function to define a 3×1 vector of value 1. Vector c3 defines a 1×3 vector of value 1, and then transposes it with the SAS/IML function T. Vector c4 uses the repetition factor [3] for the value 1 to define a 1×3 vector that is then transposed. There is an order in which matrix operations are evaluated, and parentheses can help avoid confusion in coding.

## 11.4 Importing a Data Set into SAS/IML and Exporting Matrices from SAS/IML to a Data Set

Up to now, you have entered matrices directly in PROC IML. You can imagine that it would be painful to enter and manipulate a large matrix in SAS. The SAS/IML functions USE and READ can be used to construct a matrix from a SAS data set. And, the SAS/IML functions CREATE and APPEND can be used to construct a SAS data set from a SAS/IML matrix.

### 11.4.1 Creating matrices from SAS data sets and vice versa

Suppose you have a SAS library containing a data set named nitrofen¹ that has a number of variables including total and conc. Display 11.7 illustrates importing these data into SAS/IML, and then adding three new columns. One column contains CONC², and the other two columns contain (CONC − C̄) and (CONC − C̄)², where C̄ is the average concentration. A new data set n2 is exported from SAS/IML using the create and append commands. The create command opens a new data set. The append command adds the contents of the matrix nitro2 to the n2 data set. A vector varnames that contains the names of the variables in the output data set is defined. The colname argument is specified as part of the create statement.

¹ Nitrofen data set from Bailer, A. John, and James T. Oris. 1994. "Assessing Toxicity of Pollutants in Aquatic Systems." Chapter 2 in Case Studies in Biometry. Nicholas Lange, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. New Jersey: John Wiley & Sons, Inc. Reprinted with permission of John Wiley & Sons, Inc.

## Display 11.7 Reading a SAS data set named nitrofen

```
libname mydat 'folder-containing-nitrofen-data';

proc iml;
/* read SAS data in IML */
use mydat.nitrofen;
read all var { total conc } into nitro;

/* alternative coding */
use mydat.nitrofen var{ total conc };
read all into nitro2;

nitro = nitro || nitro[,2]##2;  * adding column with conc^2;

* add column with centered concentration;
nitro2 = nitro2 || (nitro2[,2]- nitro2[,2]/nrow(nitro2));

* adding column with scaled conc^2;
nitro2 = nitro2 || nitro2[,3]##2;

show names;  * show matrices constructed in IML;
*print nitro;
*print nitro2;

* creates SAS data set n2 from matrix nitro;
*   with variable names from the COLNAME argument;
varnames = ('total'||'conc'||'c_conc'||'c_conc2');
print nitro2 varnames;
create n2 from nitro2 [colname=varnames];
append from nitro2;

quit;

proc print data=n2;
title 'print of data constructed in SAS/IML';
run;
```

# Try this at home: Rewrite the code using the subscript reduction operators : and ##.

The matrix is produced and manipulated in SAS/IML, and then exported to a SAS data set that is shown in Display 11.8. The data set includes total young, nitrofen concentration, centered concentration, and (centered concentration)².

## Display 11.8 Data set produced by SAS/IML

print of data constructed in SAS/IML
Obs total conc c_conc c_conc2
1 27 0 -157 24649
2 32 0 -157 24649
3 34 0 -157 24649
4 33 0 -157 24649
5 36 0 -157 24649
... (rows deleted) ...
44 0 310 153 23409
45 15 310 153 23409
46 5 310 153 23409
47 6 310 153 23409
48 4 310 153 23409
49 6 310 153 23409
50 5 310 153 23409

Let’s get SAS/IML to do a little work. In the next case study, the task of estimating π using a Monte Carlo integration is tackled.

## 11.5 Case Study 1: Monte Carlo Integration to Estimate π

In the SAS/IML code in Display 11.9, π is estimated by the proportion of randomly generated points that are below a circle in the first quadrant. In Section 8.8, “Case Study 2: Monte Carlo Integration to Estimate an Integral,” loops are used in a DATA step program to calculate a Monte Carlo estimate of the area corresponding to Pr(0<Z<1.645) for Z~N(0,1). In Display 11.9, 4000 (X,Y) coordinate pairs are generated and uniformly distributed in the first quadrant. There is one invocation of the randgen routine where the seed is set with randseed. These data are stored in the temp_mat matrix. A third column is added using the || column binding operator. This third column is 1 if the randomly generated Y is less than or equal to √1−x², which is coded as the following:

```
(temp_mat[,2]<= sqrt(J(nsim,1,1)-temp_mat[,1]##2))
```

The area of a circle of radius 1 centered at (0,0) in the first quadrant is π/4. (The area of the circle is π, and ¼ of the circle centered at (0,0) falls in the first quadrant.) Thus, the proportion of randomly generated points in the first quadrant that are less than the equation of the circle is an estimate of π/4. The rest of this code generates the estimate of π, places a bound on the error of estimation, and generates a confidence interval (CI) for estimating π using a normal approximation to the binomial. The J function.

J(nsim,2,0). initializes the matrix temp_mat to have nsim rows, and for two columns to have all zeros.

## Display 11.9 Using SAS/IML to estimate π using Monte Carlo integration (pts. in first quadrant)

```
proc iml;
nsim = 4000;
temp_mat = J(nsim,2,0);

/* Generate (X,Y) with single call using 'randgen' */
call randseed(21509);   * set seed for randgen;
call randgen(temp_mat,'uniform');

temp_mat = temp_mat || (temp_mat[,2]<= sqrt(J(nsim,1,1)- temp_mat[,1]#2));

pi_over4 = temp_mat[+,3]/nsim;

pi_est = 4*pi_over4;
se_est = 4*sqrt(pi_over4*(1-pi_over4)/nsim);
pi_LCL = pi_est - 2*se_est;
pi_UCL = pi_est + 2*se_est;

* ------------------------------------------------------------;
print 'Estimating PI using MC simulation methods with ' nsim 'data points';
print 'PI-estimate = ' pi_est se_est pi_LCL pi_UCL;
quit;
```

Executing this program generates the following output:

PI EST      SE EST      PI LCL      PI_UCL
PI-estimate =      3.161 0.0257492 3.1095017 3.2124983

## 11.6 Case Study 2: Bisection Root Finder

There are many problems in which you need to find the root of an equation. For example, you need to find x such that f(x)=0 when x is in some interval (say, [a,b] where f(a)<0<f(b) or f(a)>0>f(b). The following example solves √3 by finding the root of f(x)=x-√3. (This example is used by my colleague, Bob Noble, to illustrate SAS/IML coding in his class. It is included in this section.) The lower limit lo and upper limit hi are specified to be 0 and 3, respectively. The bisection method finds the midpoint of the current interval, mid=(lo+hi)/2, and checks to determine whether mid-√3>0, or, equivalently, whether mid²>3. If it is, then the guess for the solution, mid, is too high. Thus, hi is set to mid, and the process begins again. If it is not, then lo is set to mid,
