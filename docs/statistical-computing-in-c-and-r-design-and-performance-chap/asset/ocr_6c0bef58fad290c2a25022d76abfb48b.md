# NUMERICAL OPTIMIZATION

```
int main(int argc, char** argv) {
int itMax = atoi(argv[1]);
int nSearch = atoi(argv[2]);
int seed = atoi(argv[3]);
double delta = atof(argv[4]);
Functor f(&fun, &fun1, &fun2);
Opt Opt Opt = Opt(itMax, delta);
int nFail = 0;

double fMin = opt.ranNewton(f, 0, 1, nSearch, seed, &nFail);
std::cout << "The approximate minimizer is " << fMin << std::endl;
std::cout << "The number of failures is " << nFail << std::endl;
return 0;
}
```

The values of itMax, nSearch, delta and the starting seed for the random number generator are taken from command line input and the addresses of the function and its first two derivatives are used to create a Functor object. The ranNewton method is then applied with both the approximate minimizer and the number of starting values that caused difficulties being reported on completion of the optimization process programs were compiled and linked using themakefile ranNewton.mk is shown in the following:

```
opt : optDriverTri.o optim ranGen.o
g++ -Wall optDriverTri.o optim ranGen.o -o opt
anGen.o : ranGen.cpp ranGen.h
g++ -Wall -c ranGen.cpp

optim.o : optim.cpp optim ranGen.h functor.o
g++ -Wall -c optim.cpp -o optim

optDriverTri.o : optDriverTri.cpp optim.h functor.o
g++ -Wall -c optDriverTri.cpp
```

```
$ make -f ranNewton.mk
g++ -Wall -c optDriverTri.cpp
g++ -Wall -c optim.cpp
g++ -Wall -c ranGen.cpp
g++ -Wall optDriverTri.o optim.o ranGen.o -o opt
./.opt 38 9 123 .00000001
The approximate minimizer is 0.619058
The number of failures is 3
./.opt 38 10 123 .00000001
The approximate minimizer is 0.9373377
The number of failures is 3
```

This was employed to produce the results

The ranNewton method therefore requires five more searches to find the minimizer did ranGolden. However, in this instance the Newton approach converges much faster to local minimizers using only three to six of the 38 allotted iterations while the golden section based search tends to use all 38 cycles.

There are (at least) two functions that carry out Newton optimization in R: optim