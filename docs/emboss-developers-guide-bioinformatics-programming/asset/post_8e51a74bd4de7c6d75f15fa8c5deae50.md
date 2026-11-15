
values, can be difficult to understand. Review your code and establish whether the variable really needs to be in the object or whether it's best moved somewhere else.

### C.1.6 Avoid redundancy

Where two or more different objects share common elements there is likely scope for removing redundancy throughout your code. Consider whether a new object encapsulating the common elements would make your code easier to understand and maintain.

### C.1.7 Manage your variables

Functions with very long lists of variables are difficult to understand and maintain. Where a group of variables are always used together, consider encapsulating them in a new object, especially where the group occurs elsewhere in your code.

### C.1.8 Long functions

Big functions are difficult to understand. Smaller functions are easier to document and therefore easier for the programmer to identify. Functionality split into smaller functions is more likely to be reused. Consider breaking big functions down into smaller ones. If necessary, retain the function with the original name which can call the new, smaller functions. Do not overdo it though and try to avoid too many levels of function calls (see Section C.1.10, ‘Nesting of functions’).

### C.1.9 Long parameter lists

Functions with many parameters are difficult to understand, use and maintain. Where possible, you should pass an object pointer rather than the individual elements of a single object. If the parameters do not belong to an object, consider defining a new object to encapsulate them and pass a pointer to that instead.

### C.1.10 Nesting of functions

Code which uses deeply nested chains of functions can be extremely difficult to understand. Design your code to avoid this.

## C.2 Code layout

### C.2.1 Application code layout

Use the following order for laying out the application C source code:

- 1. Application standard header
- 2. Inclusion of system header files
- 3. Inclusion of local header files
- 4. Definition of constants
- 5. Definition of data types
- 6. Global variables (try to avoid these altogether)
- 7. Function prototypes
- 8. main() function
- 9. Functions.

A template application C source code file is provided in the myemboss applications directory, e.g.:

```
../embassy/myemboss/src/template.c
```

The file is shown below:

```
** @source_ApplicationName_
**
** _ShortDescription_
**
** @author Copyright (C) _Year_ _AuthorName_
** @version _VersionNumber_ _description of version_
** @modified _EditDate_ _EditorName_ _description of edit_
** @@
**
** This program is free software; you can redistribute it and/or
** modify it under the terms of the GNU General Public License
** as published by the Free Software Foundation; either version 2
** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
*******************************************************************************/
/* ======================================================================= */
/* ======================================================================= */
/* ================= include files ======================================= */
/* ======================================================================= */
/* ======================================================================= */
#include "emboss.h"
/* Inclusion of system and local header files goes here */
/* ======================================================================= */
/* ======================================================================= */
/* ================= constants =========================================== */
/* ======================================================================= */
/* ======================================================================= */
/* #define and enum statements go here */

/* ---------------------------------------------------------- */
/* ---------------------------------------------------------- global variables ---------------------------------------------------------- */
/* ---------------------------------------------------------- */

/* Global variables definitions go here */

/* ---------------------------------------------------------- */
/* ---------------------------------------------------------- data ---------------------------------------------------------- */
/* ---------------------------------------------------------- */

/* Definition of datatypes go here */

/* ---------------------------------------------------------- */
/* ---------------------------------------------------------- function prototypes ---------------------------------------------------------- */
/* ---------------------------------------------------------- */

/* Function prototypes for public (external) functions go here */

/* @prog __ApplicationName ***************************************************************
**
** __ShortDescription__
******************************************************************************************/

int main(int argc, char **argv)
{
}

/* ---------------------------------------------------------- */
/* ---------------------------------------------------------- functions ---------------------------------------------------------- */
/* ---------------------------------------------------------- */
```

### C.2.1.1 Standard file sections

Standard sections in the file ../embassy/myemboss/src/template.c are summarised below.

### C.2.1.1.1 Application standard header

All application source code files must begin with the standard documentation header (see Appendix D, Code documentation standards).

### C.2.1.1.2 Inclusion of header files

The EMBOSS header file emboss.h is included first followed by includes for any required system files. For example:

```
#include "emboss.h"
#include <limits.h>
#include <float.h>
```

emboss.h includes the EMBOSS header file ajax.h which has the following includes:

```
#include <stdio.h>
#include <stdarg.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
```

There is therefore no need to include these files explicitly in the application source code.

### C.2.1.1.3 Definition of constants

These should be given in a block and documented where necessary. For example:

```
#define TIMEOUT 30			/* Arbitrary pipe timeout (secs) */
#define TIMEBUFFER 256		/* Arbitrary length buffer for time printing */
#define PUTTIMEOUT 120		/* Max no. of secs to write a file */
#define R_BUFFER 2048		/* Arbitrary length buffer for reentrant syscalls */
```

Or:

```
enum blastdbtype [BLAST1P, BLAST1N, BLAST2P, BLAST2N] ;
```

### C.2.1.1.4 Definition of global variables

You should not use global variables unless absolutely necessary. Where they are used they should be documented.

### C.2.1.1.5 Definition of data types

Any unions and C data structure definitions that are specific to the application should be given next. All datatypes should be defined in the EMBOSS style. It is recommended, but not strictly required, that application data structures are documented in a standard way (see Appendix D, Code Documentation Standards).

### C.2.1.1.6 Function prototypes

All functions must be prototyped using the full ANSI C style.

### C.2.1.1.7 main() function

The main function is preceded with a standard documentation header (see Appendix D, Code documentation standards). The main() function should be given before other functions. This saves people from having to wade through many functions before they find it, and also helps avoid accidental implicit function declarations.

### C.2.1.1.8 Functions

Functions should be listed in the order they are prototyped and separated by whitespace (four newlines). All application-specific functions should be declared static and have a name that begins with the application name. All application functions should, ideally, be documented in a standard way (see Appendix D, Code documentation standards).
