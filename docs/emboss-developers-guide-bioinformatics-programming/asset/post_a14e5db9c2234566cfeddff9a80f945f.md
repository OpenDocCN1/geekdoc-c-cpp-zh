
## Your first EMBOSS application

Most programming books begin with a program to write a simple phrase to the screen, and that phrase is invariably “Hello World!”. This section will lead you through the process of writing helloworld under EMBOSS. You’ll cover the basic elements common to every EMBOSS program and introduce the steps used to create applications.

Some of the examples below use myemboss (Section 3.2, ‘Integration and compilation’), so you must first install and configure this package. myemboss is a special EMBASSY package and is found in the normal EMBASSY application directory, e.g.

```
/home/auser/emboss/emboss/embassy/myemboss
```

## 2.1 helloworld in C

Here is the source code of a C program that prints “Hello World!” to the screen:

```
#include <stdio.h>
int main(void)
{
  printf("Hello World!\n");
  return 0;
}
```

The first line is a preprocessor directive telling the compiler to include the header file stdio.h. The angle brackets around the name of the file to be included tell the preprocessor to look in the default location for stdio.h. On a Linux system this default location is typically the directory /usr/include.

The program consists of a single function (main) which has no parameters and an integer return type, in this case it returns 0 to the operating system after printing “Hello World!” to the screen.

If you save the source code to a file called helloworld.c, then to get an executable (runnable) version of the program, you have to compile the source by typing one of the following commands.

Using gcc, an ANSI C compiler:

```
gcc helloworld.c -o helloworld
```

Using cc, the default C compiler:

```
cc helloworld.c -o helloworld
```

If there are no compilation errors you will end up with an executable file called helloworld. If you omitted -o helloworld the executable would be called a.out. To run your program you simply type helloworld at the UNIX prompt:

```
% helloworld
Hello World!
%
```

People running a csh shell may need to type rehash first.

## 2.2 helloworld in EMBOSS

You probably write your programs to a standard pattern: you write a file of source code, compile the source code, then debug the resulting executable program. You finally run your debugged binary.

There are a couple of additional steps when writing an EMBOSS program. The key difference is that in addition to writing the source code, you must also write an ACD file for your new application. An ACD file contains a description of the command line interface. It specifies exactly what input values are required and how to verify them and what is written. It controls the behaviour of the application on the command line, in particular the user input operations.

All of the required parameters are prompted for before the application proper begins. The input values are read and held in memory, files are opened as required and so forth, so that all the parameters are available when the application proper starts. An EMBOSS application cannot ask the user for more information after several hours of processing!

It's good practice to write your ACD file before the source code because this forces you to think closely about the application inputs and outputs and exactly what's required from the user. You should then test the ACD file by using an EMBOSS application called acdc (see below). In addition, you must integrate your application into EMBOSS or EMBASSY.

So, the basic steps to writing your first EMBOSS application are:

- 1. Write ACD file
- 2. Test ACD file
- 3. Write source code
- 4. Integrate application into EMBOSS or EMBASSY (e.g. myemboss)
- 5. Compile.

Additionally, there are several other considerations with any software project:

- - Planning and design – think about the problem and design the software
- - Debugging – get it to run without crashing or obvious problems
- - Testing – ensure it works correctly under all conditions
- - Documentation – describe how it works
- - Installation and distribution
- - Maintenance, support and training.

### 2.2.1 Planning and design

You should think carefully about the task at hand and plan or design your software before coding. Think about the inputs and outputs and the major logical steps in the source code. **helloworld** is a very simple program which must:

- 1. Read and process the ACD file
- 2. Print “Hello World!” to the screen
- 3. Exit cleanly

Software planning is covered in Section 3.1, ‘EMBOSS programming’.

### 2.2.2 Writing the ACD file

The input and output of **helloworld** is trivial. All the program has to do is print “Hello World!” to the screen and so nothing is required from the user. It’s no surprise then that the ACD file is pretty sparse. As a minimum though, all ACD files must contain an _application definition_ with a single _documentation:_ attribute:

```
application: helloworld
[
    documentation: "Prints 'Hello World!' to the screen."
]
```

This definition must come first in the file. The definition consists of the `application:` token, followed by the application name and a block of attributes held between square brackets. Each attribute is a `name: value` pair. The definition above contains a single `documentation:` attribute. The text should be a succinct description of the program and will be printed to screen when the program is run. If the `documentation:` attribute is missing, a warning will be issued when you run the program.

Typically you will develop new code in a special EMBASSY package called **myemboss** that is reserved for applications that are not yet ready to be incorporated into the main EMBOSS or EMBASSY packages (see Section 3.1, ‘EMBOSS programming’). Save your ACD file in the **myemboss** ACD directory:

```
../myemboss/emboss_acd
```

If the program were to be added to EMBOSS itself then directory would be:

```
../emboss/acd
```

ACD files have a filename of the form ApplicationName.acd, where ApplicationName is the name of the application. The file extension .acd is mandatory. It's sensible (but not mandatory) that the filename (without the .acd extension) is identical to the name of the C source code file.

For further information, see the detailed information on the ACD syntax (Appendix A, ACD syntax reference) and ACD file development (Section 4.1, 'Introduction to ACD file development').

### 2.2.3 Testing the ACD file

Special utilities (Section 4.6, 'ACD utilities') are provided to help you test and validate your ACD files. The main one you'll need is called acdc (the ACD compiler) which, when given the name of an ACD file as the first argument on the command line, will parse the file, validate it, parse the command line and 'run' the application command line interface as if the application proper was running.

So, testing the ACD file is easy. You simply run acdc, giving your application name as an argument:

```
acdc ApplicationName
```

where ApplicationName is the name of the application. So, for helloworld:

```
% acdc helloworld
Prints 'Hello World!' to the screen.
%
```

acdc reads helloworld.acd and reads in any required data just as if the application itself was running. It will also test anything on the command line and report errors in exactly the same way as the real application. In this case there is no required data and nothing else on the command line. As acdc didn't report an error in the example above, then we can assume all is well.

### 2.2.4 Writing the source code

Happy in the knowledge you have a working ACD file you can turn to the C source code itself, which should look something like this:

```
/* @source helloworld Prints "Hello World!" to the screen.
 *
 * @author: Copyright (C) Arthur Geek (ageek@ebi.ac.uk)
 *
 * @#
 *
 * This program is free software; you can redistribute it and/or
 * modify it under the terms of the GNU General Public License
 * as published by the Free Software Foundation; either version 2
 * of the License, or (at your option) any later version.
 *
 * This program is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with this program; if not, write to the Free Software
 * Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
 ************************************************************************/

#include "emboss.h"

/* @prog helloworld *********************************************************
 *
 * Prints "Hello World!" to the screen.
 *
 *****************************************************************************/

int main(int argc, char **argv)
{
    embInit("helloworld", argc, argv);
    ajFmtPrint("Hello World!\n");
    embExit();
    return 0;
}
```

There are three main parts to the helloworld.c file and, indeed, to all EMBOSS programs:

- The standard EMBOSS application documentation header
- #include statements
- The application code proper

In C (and EMBOSS code is no exception), every program must have a main() function. For helloworld.c the program itself consists of the main() function only, but most programs have other functions besides main().

The source begins with the standard EMBOSS header. This block of comments includes the name of the program and its short description, copyright notice, licence information, disclaimer, author name and contact details. The tags, for instance @source, allow EMBOSS to generate documentation automatically from the code. EMBOSS applications are licensed under the GNU General Public License, so these comments must be included in the source.

Next there is the preprocessor directive #include "emboss.h". In contrast to #include <stdio.h>, this imports the entire EMBOSS interface, i.e. makes all the EMBOSS library calls available to you. This must be included at the start of every EMBOSS program.
