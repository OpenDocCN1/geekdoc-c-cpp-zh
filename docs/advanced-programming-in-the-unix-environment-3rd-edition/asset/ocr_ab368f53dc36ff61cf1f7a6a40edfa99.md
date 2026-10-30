# Pseudo Terminals

# 19.1 Introduction

In Chapter 9, we saw that terminal logins come in through a terminal device, automatically providing terminal semantics. A terminal line discipline (Figure 18.2) exists between the terminal and the programs that we run, so we can set the terminal’s special characters (e.g., backspace, line erase, interrupt) and the like. When a login arrives on a network connection, however, a terminal line discipline is not automatically provided between the incoming network connection and the login shell. Figure 9.5 showed that a pseudo terminal device driver is used to provide terminal semantics.

In addition to network logins, pseudo terminals have other uses that we explore in this chapter. We start with an overview on how to use pseudo terminals, followed by a discussion of specific use cases. Next we provide functions to create pseudo terminals on various platforms, and then we use these functions to write a program that we call pty. We’ll show various uses of this program: making a transcript of all the character input and output on the terminal (the script(1) program) and running coprocesses to avoid the buffering problems we encountered in the program from Figure 15.19.

# 19.2 Overview

The term pseudo terminal implies that it looks like a terminal to an application program, but it’s not a real terminal. Figure 19.1 shows the typical arrangement of the processes involved when a pseudo terminal is being used. The key points in this figure are the following.