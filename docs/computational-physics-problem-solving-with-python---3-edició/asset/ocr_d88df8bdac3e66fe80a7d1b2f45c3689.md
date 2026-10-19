Here >>> represents the prompt for a Python shell. Some of the typing can be avoided by assigning a symbol to the package name:

```
>>> import visual.graph as p
>>> y1 = p.gcurve(color = blue, delta = 3)
```

There is also a starred version of from that copies all of the methods of a package (here Matplotlib called pylab) so that you can leave off prefixes:

```
>>> from pylab import * # Import all pylab methods
>>> plot(x, y, '-.', lw=2) # A pylab method without prefix
```

# 1.4.2 This Book's Packages

We are about to describe some of the packages that make Python such a rich environment. If you are anxious to get started now, or worry about getting overwhelmed by the Python packages, you may just want to load VPython now and move on to the next chapter. You will need some more stuff to do visualizations and matrices, but you can always upgrade your knowledge when you feel more comfortable with Python.

Because all too often you do not know what you do not know, or what you need to know, we list here a few, basic Python packages and what each does. The packages used in the text are underlined and described more fully later.

+   **Boost.Python** A C++ library that enables seamless interoperability between C++ and Python, thus extending the lifetime of legacy codes and making use of the speed of C, www.boost.org/doc/libs/1_55_0/libs/python/doc/.

+   **Cyth on: C Extensions for Python** A superset of the Python language that supports calling C functions and intermixing Python and C for legacy purposes and for high performance, http://cython.org/.

+   **f2py: Fortran to Python Interface Generator** that provides connection between Python and Fortran languages; great for steering legacy codes, http://cens.ioc.ee/projects/f2py2e/.

+   **IPython: Interactive Python** An advanced shell (command line interpreter) that extends Python's basic interpreter IDLE. IPython has enhanced interactivity and interactive visualization capabilities that encourage exploratory computing. IPython also has a browser-based notebook like Mathematica that permits embedded code executions, as well as capabilities for parallel computing, http://ipython.org/.

+   **Matplotlib: Mathematics Plotting Library** A 2D and 3D graphics library that uses NumPy (Numerical Python), and produces publication quality figures in a variety of hard copy formats, and permits interactive graphics. Similar to MATLAB's plotting (except Matplotlib is free and doesn't need its li...