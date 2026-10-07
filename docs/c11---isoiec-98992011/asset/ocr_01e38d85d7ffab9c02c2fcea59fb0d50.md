# © ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

designator, which is used to call the function; it returns an int.
If the declaration occurs outside of any function, the identifiers have file scope and linkage. If the declaration occurs inside a function, the identifiers of the functions f and have block scope and either internal or external linkage (depending on what file scope declarations these identifiers are visible), and the identifier of the pointer pfi has block scope and no linkage.

+   17 EXAMPLE 2 The declaration
int (*apfi3)(int *x, int *y);
declare an apfi of three pointers to functions returning int. Each of these has parameters that are pointers to int. The identifiers x and y are declared for descriptive purposes and only go out of scope at the end of the declaration of apfi.

+   19 EXAMPLE 3 The declaration
int (*fppi)(int (*long), int), ...ndeclare a function fppi that returns a pointer to a function returning int. The function fppi has two parameters: to a function returning int (with one parameter of type long int), and an int. The pointer returned by fppi to a function that has one parameter and accepts zero or more arguments of any type.

+   20 EXAMPLE 4 The following prototype has a variably modified parameter.
void addscalar(int n, int m, double a[n*300], double x);

int main() {
double b[4][308];
addscalar(4, 2, b, 2.17);
return 0;
}
\void addscalar(int n, int m, double a[n*300], double x) {
  for (int i = 0; i < n; i++) {
    for (int j = 0, k = n*m+300; j < k; j++) {
      // a is a pointer to a VLA with n*m+300 elements
      a[i][j] += x;
    }
  }
}

+   21 EXAMPLE 5 The following are all compatible prototype declarations.
double maximum(int n, int m, double a[n][m]);
double maximum(int n, int m, double a[*]);
double maximum(int n, int m, double a[][]);
double maximum(int n, int m, double a[][]);

as are:
void f(double (*restrict a [5]);
void f(double arestrict)[5]);
void f(double arestrict 3[5]);
void f(double arestrict static 3[5]);

# $6.7.6.3 Language 135