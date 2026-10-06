# 18 Introduction to Programming and Problem-Solving Using Scala

only concern ourselves with one of these: scala.$^1$ The scala command actually runs scala
programs. There is a second command, scalac, that is used to compile scala text files into
bytecode that is compatible with the Java or .NET platform. We will only use scalac
in the last chapter of this book, but we will begin using the scalac command immediately.

### Scala on your Machine

If you only use Scala on a machine in a computer lab, hopefully everything will
been set up for you that you can simply type the name of a command and it will
Run to Scala on your machine you can follow the instructions below.

# Installation

Scala requires Java® to run so if you do not have Java installed you should go
to http://java.oracle.com and download then the most recent version of the
Java SE JDK. When you install Java, you can go with the default installations.
After you have installed Java you can install Scala. To download Scala to http:
//www.scala-lang.org. On this site download the latest version of Scala. The code
in this book was written to work with Scala 2.12.

# Dealing with the PATH

If you are using Scala on your machine, it is possible that entering scala or
scala, bat on the command line could produce a message telling you that the command
or program scala could not be found. This happens because the location of the installed
programs are not in your default PATH.
The PATH is a set of directories that are checked whenever you run a command. The
first match that is found for any executable file in a directory in the PATH will be run.
If more of the programs in the PATH matches what you entered, you get an error.

When you installed Scala, a lot of different stuff was what you installed into the directory.
That included a subdirectory called "bin" with different files in it for the different
executables. If you are on a Windows machine, odds are that you installed the program
in C:\Program Files\scala (x86)\scala to the scala.bat file that you want to run is in
C:\Program Files\scala-bin\scala.bat. You can type that in full command or you
add the bin directory to your PATH. To do this go to Control Panel, System and
Security, Environment Variables, and edit the PATH to add
C:\Program Files\bin to the path.

Under Unix/Linux you can do this from the command line. Odds are that Scala
installed in a directory called scala in your user space. To add the bin directory
to your path you do this the following:

```
export PATH=$PATH:home/username/scala/bin
```

Replace "username" with your username.
If it does not work for you, you can do a little searching on the web for how
add directories to your path in whatever you are running. To make it that you
d not have to do this every time you open a terminal, add that line to the appropriate
configuration in your home directory. If you are running the Bash on Linux
this would be .bashrc.

> ^1On a Windows system this command should be followed by ".bat".