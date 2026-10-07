# Object Oriented Programming using C#

# An Introduction to Object Oriented Programming

# Compilation

The compiler translates the source code into machine code for the relevant hardware / operating system combination.

Strictly speaking there are two stages: compilation of program units (usually files), followed by 'linking' when the complete executable program is put together including the separate program units and relevant library code etc.

The compiled program then runs as a 'native' application for that platform.

This is the oldest model, used by early languages like Fortran and Cobol, and many modern ones like C#. It allows fast execution speeds but requires re-compilation of the program each time the code is changed or each time we want to run this code on a machine with a different operating system.

![](bbox=[0.318, 0.335, 0.742, 0.493])

# Interpretation

Here the source code is not translated into machine code. Instead an interpreter reads the source code and performs the actions it specifies.

We can say that the interpreter is like a 'virtual machine' whose machine language is the source code language.

No re-compilation is required after changing the code, but the interpretation process inflicts a significant impact on execution speed.

Scripting languages tend to work in this way.