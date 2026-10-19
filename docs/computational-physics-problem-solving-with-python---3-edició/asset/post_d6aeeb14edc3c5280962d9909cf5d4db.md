
![](img/bccda43674e4a93dee81c749eba8d2f7_52_0.png)

![](img/bccda43674e4a93dee81c749eba8d2f7_52_1.png)

(a)

(b)

Figure 1.12 (a) A Mayavi visualization of the contours of the scalar field φ(x, y, z) = sin(xyz)/xyz. (b) A volume rendering of the same scalar field.

components of the vector field as functions of the other arrays. The new command here is quiver3d which provides a collection of arrows (cute name).

If the field we wish to visualize is a scalar field, such as φ(x, y, z) = sin(xyz)/xyz, then the appropriate visualization would be an iso-surface (a 3D contour plot of equal values) throughout a 3D space. We do that with the contour3d command:

```
import numpy as np
from mayavi import mlab
x, y, z = np.ogrid[-10:10:20j, -10:10:20j, -10:10:20j]
scalar = np.sin(x*y*z)/(x*y*z)
mlab.contour3d(scalar)
mlab.show()
```

Figure 1.12a shows the output, which is periodic, but not obviously trigonometric.

We now take our visualization of the same scalar field and show how some other Mayavi methods yield different views of the field. First, a volume rendering to produce the nebulous view in Figure 1.12b:

```
import numpy as np
from mayavi import mlab
x, y, z = np.ogrid[-10:10:20j, -10:10:20j, -10:10:20j]
s = np.sin(x*y*z)/(x*y*z)
mlab.pipeline.volume(mlab.pipeline.scalar_field(s))
mlab.show()
```

Next, we take the same field and replace the mlab.contour3d(s) command with the pipeline command:

```
mlab.pipeline.volume(mlab.pipeline.scalar_field(s))
```

This produces the nebulous visualization in Figure 1.12b. Next, we produce the visualization in Figure 1.13a by having some planes cut through the scalar field:

## 1.7 Python's Algebraic Tools

While this book's focus is on the use of Python for numerical simulations, this is not to discount the importance of computational symbolic manipulations (even though that may be the way we feel). Python actually has (at least) two packages that can be used for symbolic manipulations, and they are quite different. As indicated in Section 1.4.3, the Sage package is very much in the same class as Maple and Mathematica, with a notebook graphical interface that lets the user create publication quality text, within which Python programs can be run, or the equations can be manipulated symbolically. Yet Sage is a big and powerful package that goes beyond pure Python by including multiple computer algebra systems as well as visualization tools and more. Using the multiple features of Sage can get to be quite complicated, and, in fact, books have been written and workshops taught on the use of Sage. We refer the interested reader to the online Sage documentation page at www.sagemath.org/help.html.

The SymPy package for symbolic manipulations runs very much like any other Python package from within your regular Python shell. It can be downloaded from https://github.com/sympy/sympy/releases, or you can use the Canopy distribution that includes SymPy. Now we give some simple examples of SymPy's use, but you really need to start with the SymPy Tutorial http://docs.sympy.org/latest/tutorial/ if you want to use SymPy. (Note, despite the fact that we are working within a Python shell, SymPy has automatically found an LATEXapplication and used it to format the output.) To start, we will take some derivatives to show that SymPy knows calculus:

```
>>> from sympy import *
>>> x, y = symbols('x y')
>>> y = diff(tan(x),x); y tan²(x) + 1
>>> y = diff(5*x**4 + 7*x**2, x, 1); y
>>> y = diff(5*x**4 + 7*x**2, x, 2); y
```

We see here that we must first import methods from SymPy and then use the symbols command to declare the variables x and y as algebraic. The rest is rather obvious, with diff being the derivative operator and the x argument in diff indicating what we are taking the derivative with respect to x. Now let us try expansions:

```
>>> from sympy import *
>>> x, y = symbols('x y')
>>> z = (x + y)**8; z
>>> expand(z) x^8 + 8x^7 y + 28x^6 y^2 + 56x^5 y^3 + 70x^4 y^4 + 56x^3 y^5 + 28x^2 y^6 + 8x y^7 + y^8
```

SymPy knows about infinite series and different expansion points:

```
>>> sin(x).series(x, 0)
# Usual sin x series about 0
x - x^3/6 + x^5/120 + O(x^7)
>>> sin(x).series(x,10)
# sin x about x = 10
sin(10) + x cos(10) - x^2 sin(10)/2 - x^3 cos(10)/6 + x^4 sin(10)/24 + x^5 cos(10)/120 + O(x^6)
```

```
>>> z = 1/cos(x); z
1/cos(x)
>>> z.series(x, 0)
1 + x**2/2 + 5*x**4/24 + O(x**6)
# A division, not an inverse
# Expand 1/cos x about x = 0
```

One of the classic difficulties with computer algebra systems is that even if the answer is correct, if it is not simple, then it probably is not useful. And so, SymPy has a simplify function as well as a factor function (and collect, cancel and apart which we will not illustrate):

```
>>> factor(x**2 -1)
(x - 1)(x + 1)
# A nice answer
>>> factor(x**3 - x**2 + x - 1)
(x - 1)(x**2 + 1)
>>> simplify((x**3 + x**2 - x - 1)/(x**2 + 2*x + 1))
x - 1
# Much better!
>>> simplify(x**3+3*x**2*y+3*x*y**2+y**3)
x**3 + 3*x**2*y + 3*x*y**2 + y**3
# No help!
>>> factor(x**3+3*x**2*y+3*x*y**2+y**3)
(x + y)**3
# Much better!
>>> simplify(1 + tan(x)**2)
cos(x)**(-2)
>>> simplify(2*tan(x)/(1+tan(x)**2))
sin(2*x)
```

## 2

## Computing Software Basics

This chapter discusses some computing basics starting with computing languages, number representations, and programming tools. The limits and consequences of using floating-point numbers are explored. Related topics dealing with hardware basics are found in Chapter 10.

### 2.1

### Making Computers Obey

> The best programs are written so that computing machines can perform them quickly and human beings can understand them clearly. A programmer is ideally an essayist who works with traditional aesthetic and literary forms as well as mathematical concepts, to communicate the way that an algorithm works and to convince a reader that the results will be correct.
> 
> Donald E. Knuth

As anthropomorphic as your view of your computer may be, keep in mind that computers always do exactly as they are told. This means that you must tell them exactly everything they have to do. Of course, the programs you run may have such convoluted logic that you may not have the endurance to figure out the details of what you have told the computer to do, but it is always possible in principle. So your first problem is to obtain enough understanding so that you feel well enough in control, no matter how illusory, to figure out what the computer is doing.

Before you tell the computer to obey your orders, you need to understand that life is not simple for computers. The instructions they understand are in a basic machine language¹) that tells the hardware to do things like move a number stored in one memory location to another location or to do some simple binary arithmetic. Very few computational scientists talk to computers in a language computers can understand. When writing and running programs, we usually com-

1) The Beginner's All-Purpose Symbolic Instruction Code (BASIC) programming language of the original PCs should not be confused with basic machine language.

municate to the computer through shells, in high-level languages (Python, Java, Fortran, C), or through problem-solving environments (Maple, Mathematica, and Matlab). Eventually, these commands or programs are translated into the basic machine language that the hardware understands.

A shell is a command-line interpreter, that is, a set of small programs run by a computer that respond to the commands (the names of the programs) that you key in. Usually you open a special window to access the shell, and this window is called a shell as well. It is helpful to think of these shells as the outer layers of the computer’s operating system (OS) (Figure 2.1), within which lies a kernel of elementary operations. (The user seldom interacts directly with the kernel, except possibly when installing programs or when building an OS from scratch.) It is the job of the shell to run programs, compilers, and utilities that do things like copying files. There can be different types of shells on a single computer or multiple copies of the same shell running at the same time.

![](img/bccda43674e4a93dee81c749eba8d2f7_57_0.png)

Figure 2.1 A schematic view of a computer’s kernel and shells. The hardware is in the center surrounded by increasing higher level software.

Operating systems have names such as Unix, Linux, DOS, MacOS, and MS Windows. The operating system is a group of programs used by the computer to communicate with users and devices, to store and read data, and to execute programs. The OS tells the computer what to do in an elementary way. The OS views you, other devices, and programs as input data for it to process; in many ways, it is the indispensable office manager. While all this may seem complicated, the purpose of the OS is to let the computer do the nitty-gritty work so that you can think higher level thoughts and communicate with the computer in something closer to your normal everyday language.
