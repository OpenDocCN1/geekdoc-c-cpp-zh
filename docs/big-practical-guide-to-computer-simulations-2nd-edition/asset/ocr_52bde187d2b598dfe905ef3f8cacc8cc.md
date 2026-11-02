```
\item Design data types and functions
\item Code in C
\item Test and debug
\end{enumerate}
\item Perform simulations and analyse data
\begin{enumerate}
\item For standard case, to compare with analytics
\item For the two-dimensional case
\item For the three-dimensional case.
\end{enumerate}
\end{enumerate}
```

This will result in:

+   (1) Write program
+   (a) Design data types and functions
+   (b) Code in C
+   (c) Test and debug
+   
+   (2) Perform simulations and analyse data
+   (a) For standard case, to compare with analytics
+   (b) For the two-dimensional case
+   (c) For the three-dimensional case.

Arbitrary lists can be defined using the list environment; please have a look at the LaTeX documentation.

The \verb command used in the above list allows an arbitrary string to be printed in a typewriter font as it stands. Here, the string to be printed is not given as an argument, but is embraced in ! ! . In this way arbitrary symbols can be contained in the string, also ‘{’ and ‘}’. Always the first symbol after the \verb is taken as bracketing symbol here. Hence, one could write also \verb?\\?\ in the above example. The string is not allowed to extend beyond the limits of one line. For longer texts which should be printed verbatim, there is the verbatim environment. Thus, you have to embrace the text by \begin{verbatim} and \end{verbatim}, which is used in this book, for example, to display the C source codes.