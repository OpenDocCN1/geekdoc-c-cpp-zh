The most recent Gnu g++ compiler can be obtained from http://gcc.gnu.org. If the compiler that is made available in the Cygnus distribution lags behind the latest version, the sources of the latest version can be downloaded after which the compiler can be built using an already available compiler. The compiler's webpage (mentioned above) contains detailed instructions on how to proceed. In our experience building a new compiler within the Cygnus environment works flawlessly.

# ### 2.2.3.2 Compiling a C++ source text

Generally the following command can be used to compile a C++ source file 'source.cc':

```
```
g++ source.cc
```
```

This produces a binary program (a.out or a.exe). If the default name is inappropriate, the name of the executable can be specified using the -o flag (here producing the program source):

```
```
g++ -o source source.cc
```
```

If a mere compilation is required, the compiled module can be produced using the -c flag:

```
```
g++ -c source.cc
```
```

This generates the file source.o, which can later on be linked to other modules. As pointed out, provide the compiler option -std=c++0x (note: two dashes). to activate the features of the C++11 standard.

C++ programs quickly become too complex to maintain 'by hand'. With all serious programming projects program maintenance tools are used. Usually the standard make program is used to maintain C++ programs, but good alternatives exist, like the icmake⁹ or ccbuild¹⁰ program maintenance utilities.

It is strongly advised to start using maintenance utilities early in the study of C++.

# ## 2.3 C++: advantages and claims

Often it is said that programming in C++ leads to 'better' programs. Some of the claimed advantages of C++ are:

+   - New programs would be developed in less time because old code can be reused.
+   - Creating and using new data types would be easier than in C.
+   - The memory management under C++ would be easier and more transparent.
+   - Programs would be less bug-prone, as C++ uses a stricter syntax and type checking.
+   - 'Data hiding', the usage of data by one program part while other program parts cannot access the data, would be easier to implement with C++.

Which of these allegations are true? Originally, our impression was that the C++ language was somewhat overrated; the same holding true for the entire object-oriented programming (OOP) approach. The enthusiasm for the C++ language resembles the once uttered allegations about Artificial-Intelligence (AI) languages like Lisp and Prolog: these languages were supposed to solve the most difficult AI-problems 'almost without effort'. New languages are often oversold: in the end, each problem can be

⁹ http://icmake.sourceforge.net/
¹⁰ http://ccbuild.sourceforge.net/