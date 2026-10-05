# # Appendix C

# ## Developing C++ Programs with the GNU Tools

The tools provided by the GNU Compiler Collection (http://gcc.gnu.org), or GCC for short, include one of the most up-to-date standards compliant C++ compilers. The GNU tools are free and available for the major computing platforms:

+   * **Microsoft Windows XP-Windows 8.1**nWindows-based GCC tools can be found at the MinGW website http://www.mingw.org. The Nuwen site offers an easy to install custom distribution of MinGW with some additional C++ libraries.

+   * **Apple Macintosh OS X**nThe MacPorts website (http://www.macports.org/ports.php?by=variant&substr=gcc48) brings the GCC toolkit to Mac developers.

+   * **Linux**nLinux-based GCC tools are readily available for all the major Linux distributions. To get them, simply install the g++ development packages.

In this appendix we focus on building C++ programs with the GCC C++ compiler. We will concentrate on the GCC tools, the code in this text is not specific GCC. The code herein aims to be C++ standards compliant and platform independent.

The name of the C++ compiler is g++. It is a command-line tool, which means it is launched from a command shell—CMD.EXE in Windows or bash in the Mac and Linux environments.

There are few commands that are essential for using the command-line environment. Our discussion assumes the Windows CMD.EXE shell, and we will note differences with Mac and Linux as needed. Mac OS X and Linux are both Unix-like operating systems.

When you run CMD.EXE in Windows, the Terminal application, or a bash terminal in Linux, the operating system presents a text-console window. You type commands into this window and receive feedback. Most of the commands are programs that you launch by typing their name. The following lists common commands for using the command-line GCC C++ tools: