# # 1.4 This Book's Language: The Python Ecosystem

Standard for the explorative and interactive computing that typifies the present-day scientific research. These rapid developments of Python have also led to a succession of new versions, and the inevitable incompatibilities. Most of the codes in this book were written using Python 2, which was released in 2000, and specifically Python 2.6 with the Visual package (also known as “VPython”). However, there have been major changes to the Python development process as well as in features, and this has led to the release of Python 3.0 in December 2008. Unfortunately, some of the changes in Python 3 were not backward compatible with Python 2.6 and 2.7, and so advances in both Python 2 and 3 and their associated packages have been occurring in parallel. (For our codes, the major difference is in the print statement using a parenthesis in 3, which is not hard to correct.) Furthermore, there have been new versions of operating systems and processors from 32- to 64-bit CPUs, and this also has led to the variety of Python versions and associated packages.

To be honest, we have sometimes felt frustrated by these changes and resulting incompatibilities; however, we are intent on not sharing that! While we will describe the packages and distribution briefly, we indicate here that we have adapted to the real world by having both independent Python 2 and 3 implementations exist on our computers. Specifically, our Visual package programs use Python 3.2, while the others use the Enthought Canopy Distribution Version 1.3.0, which at present uses Python 2.7.3. (The Visual package is not available in Enthought.)

# ## 1.4.1 Python Packages (Libraries)

The Python language plus its family of packages comprise a veritable ecosystem for computing. A package or module is a collection of related methods or classes of methods that are assembled together into a subroutine library.¹ Inclusion of the appropriate packages extends the language to meet the specialized needs of various science and engineering disciplines, and lets one obtain state-of-the-art computing for free. In fact, the May/June 2007 and March/April 2011 issues of Computing in Science and Engineering (Perez et al., 2010) focus on scientific computing with Python, and we recommend them.

```
>>> from visual.graph import * # Import from visual package
>>> y1 = visual.graph.gcurve(color = blue, delta = 3) # Use of graph
```

+   1) The Python Package Index (PYPl, 2014), a repository of free Python packages, currently contains more than 40 000 packages!