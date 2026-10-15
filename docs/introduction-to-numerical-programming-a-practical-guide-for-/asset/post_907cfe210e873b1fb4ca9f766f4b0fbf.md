
```
for (i=1; i<=n; i++)
    for (j=1; j<=m; j++) {
        t = 0e0;
        for (k=1; k<=l; k++) t += a[i][k] * b[k][j];
        c[i][j] = t;
    }
}
//============================================================================
double MatNorm(double **a, int n, int m)
//--------------------------------------------------------------------------
// Returns the max norm of matrix a[1:n][1:m], i.e. max|a[i][j]|
//--------------------------------------------------------------------------
{
    double norm;
    int i, j;
    norm = 0e0;
    for (i=1; i<=n; i++)
        for (j=1; j<=m; j++)
            if (norm < fabs(a[i][j])) norm = fabs(a[i][j]);
    return norm;
}
#endif
```

The function MatPrint displays matrices in formatted tabular form. While in Python, iterative printing of several items on the same line is obtained by explicitly inhibiting the default new line after each item, in C/C++, one specifically sends a final newline character to complete the line.

MatTrans transposes its square input matrix of order n by swapping the pairs of symmetric elements. The function MatDiff returns the difference between two n×m matrices, a and b. The output matrix c can safely coincide with either of the input matrices. The function MatProd calculates the product of the n×1 matrix a with the 1×m matrix b. The n×m result is returned in array c.

Last but not the least, the function MatNorm returns the max-norm of the input matrix:

‖A‖max = max{|a_ij|},

that is, the maximum absolute value of its elements.

The Python and C/C++ versions of the program for checking the matrix identity (2.1), given in Listings 2.18 and 2.19, request as sole input the size of the square matrices A and B. The program then

**Listing 2.18 Check of Matrix Identity (Python Coding)**

```
# Checks identity (A B)_trans = B_trans A_trans for random arrays A and B
from random import *
from matutil import *

# main

n = int(input("n = "))

A = [[0]*(n+1) for i in range(n+1)]          # define arrays
B = [[0]*(n+1) for i in range(n+1)]
C = [[0]*(n+1) for i in range(n+1)]
D = [[0]*(n+1) for i in range(n+1)]

for i in range(1,n+1):                     # array A: random sub-unitary elements
    for j in range(1,n+1): A[i][j] = random()
print("Array A:")
MatPrint(A,n,n)

for i in range(1,n+1):                     # array B: random sub-unitary elements
    for j in range(1,n+1): B[i][j] = random()
print("Array B:")
MatPrint(B,n,n)

MatProd(A,B,C,n,n,n)                                   # A*B
MatTrans(C,n)                                          # (A*B)_trans

MatTrans(A,n)                                          # A_trans
MatTrans(B,n)                                          # B_trans
MatProd(B,A,D,n,n,n)                                   # B_trans* A_trans

MatDiff(C,D,D,n,n)                                     # (A*B)_trans - B_trans * A_trans
print("Norm ((A*B)_trans - B_trans * A_trans) =",MatNorm(D,n,n))
```

**Listing 2.19 Check of Matrix Identity (C/C++ Coding)**

```
// Checks identity (A B)_trans = B_trans A_trans for random matrices A and B
#include <stdio.h>
#include "memalloc.h"
#include "matutil.h"

int main()
{
    double **A, **B, **C, **D;
    int i, j, n;

    printf("n = "); scanf("%i", &n);

    A = Matrix(1,n,1,n); B = Matrix(1,n,1,n);                 // allocates arrays
    C = Matrix(1,n,1,n); D = Matrix(1,n,1,n);

    for (i=1; i<=n; i++)                      // array A: random sub-unitary elements
        for (j=1; j<=n; j++) A[i][j] = rand()/(RAND_MAX+1e0);
    printf("Array A:\n");
    MatPrint(A,n,n);

    for (i=1; i<=n; i++)                      // array B: random sub-unitary elements
        for (j=1; j<=n; j++) B[i][j] = rand()/(RAND_MAX+1e0);
    printf("Array B:\n");
    MatPrint(B,n,n);

    MatProd(A,B,C,n,n,n);                                   // A*B
    MatTrans(C,n);                                          // (A*B)_trans

    MatTrans(A,n);                                          // A_trans
    MatTrans(B,n);                                          // B_trans
    MatProd(B,A,D,n,n,n);                                   // B_trans* A_trans

    MatDiff(C,D,D,n,n);                                     // (A*B)_trans - B_trans * A_trans
    printf("Norm ((A*B)_trans - B_trans * A_trans) = %e\n",MatNorm(D,n,n));
}
```

## 3 Elements of Scientific Graphics

### 3.1 The Tkinter Package

Tk is an open-source cross-platform toolkit for building graphical user interfaces (GUIs) for various programming languages. Developed in 1991 by John Ousterhout, Tk provides a library of basic widgets (such as frames, buttons, menus, etc.), which are commonly used in modern application software. Widget is the generic term used for the building blocks of GUI applications, or, in general, for stand-alone applications that can be embedded in third-party applications.

Tkinter (from “Tk interface”) is the object-oriented interface of Python to the Tk toolkit. Tkinter was written by Fredrik Lundh in 1999 (Lundh, 2013a) and has become Python’s standard GUI package, being available, along with Tk, on most Unix-like, Windows, and Macintosh systems. Tkinter consists of several Python modules, the most important being the tkinter module. It contains all the classes and functions required to work with the Tk toolkit.

The simplest Tkinter application is the one creating an empty Tk widget (Listing 3.1). Any program resting upon Tkinter first needs to import the tkinter module. Tkinter is initialized by creating a Tk root widget, and this is accomplished in our sample program by the statement root = Tk(). The root widget (see Figure 3.1) is, basically, an ordinary window with the “look and feel” specific to the particular operating system and window manager that are being used. Notably, any program should operate with a single root widget, and this should be created prior to any other widgets, which would relate to the root as subordinated “child” objects.

**Listing 3.1 Creating a Tk Root Widget (Python Coding)**

```
from tkinter import *          # import Tkinter module

root = Tk()                   # create Tk root widget

root.mainloop()               # enter Tkinter event loop
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_52_0.png)

FIGURE 3.1 Empty Tk widget created with Tkinter.

With the code composed of just the first two statements and the root widget merely created, the window would not be effectively displayed. For the application window to appear, the execution must enter the Tkinter event loop and this is implemented as a call to the method root.mainloop(). The program will stay idle in the event loop until the window is closed. In the broader picture, the event loop handles the operations queued by Tkinter along with events triggered by the user (e.g., mouse clicks) or the windowing system (e.g., window redraws). Typical operations queued by Tkinter concern widget resizing (as initiated by the pack method) and widget redrawing (as caused by the update method).

The root widget can control other subordinated widgets. A Label widget, for instance, can be used to display text or an image on the screen. In Listing 3.2, we create a Label widget as a child to the root.

**Listing 3.2 Creating a tkinter Label Widget (Python Coding)**

```
from tkinter import *                 # import Tkinter module

root = Tk()                           # create Tk root widget
w = Label(root, text="This is a Label widget")  # create label widget: child to root
w.pack()                              # resize label to fit text; make it visible

root.mainloop()                       # enter Tkinter event loop
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_52_1.png)

FIGURE 3.2 Label widget created with Tkinter.

### 3.2 The Canvas Widget

The Canvas is a general-purpose widget, providing versatile graphics facilities. The Canvas widget is most appropriate for drawing pictures, graphs, plots, and even more complex layouts, and also for creating custom widgets.

The image displayed on the Canvas results by the successive creation of canvas items. The items are placed in a stack, with the new items drawn, by default, on top of those already existing. The standard items supported by the Canvas widget are arc, bitmap, image, line, oval, polygon, rectangle, text, and window. Several items defined by closed boundaries (such as chords, pie slices, ovals, polygons, and rectangles) feature an outline and an interior area, which can be colored or made transparent separately. Window items can be used to display other Tkinter widgets on the canvas.
