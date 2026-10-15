# Appendix D: The Numerical Libraries numxlib.py and numxlib.h

The numerical libraries numxlib.py and numxlib.h are located, respectively, in the folders /INF/modules/ and /INF/include/. They have identical structure and include the partial Python and, respectively, C/C++ libraries developed in Chapters 4 through 13. The contained routines have identical names and functionalities. There is a single exception to the identical naming convention, regarding the files random1.py and random.h, which is due to the existence of a standard Python module random.py. In addition to the corresponding partial libraries, numxlib.h also includes memalloc.h, containing dynamic memory allocation routines for vectors and matrices (see Appendix A). The concrete content of the files numxlib.py and numxlib.h is provided in Listings D.1 and D.2, respectively.

Listing D.1 The numxlib.py Numerics Library for Python (Python Coding)

```
#----------------------------------- numxlib.py -----------------------------------
# Library of numerical methods for Python
# Author: Titus Beu, 2013
#-----------------------------------------------------------------------------------

from sort import *                     # sorting and indexing

from specfunc import *                 # special functions

from roots import *                    # roots of equations

from linsys import *                   # systems of linear equations

from eigsys import *                   # eigenvalue problems

from modfunc import *                  # modeling of tabulated functions

from integral import *                 # integration of functions

from random1 import *                  # generation of random numbers

from ode import *                      # ordinary differential equations

from pde import *                      # partial differential equations

from utils import *                    # utility functions
```