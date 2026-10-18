the second one for specifying the file mode. The general form of the function open() with two arguments is:

> stream-object.open("filename", mode);

The second argument mode (called file mode parameter) specifies the purpose for which the file is opened. How did we then open the files without providing the second argument in the previous examples?

The prototype of these class member functions contain default values for the second argument and therefore they use the default values in the absence of the actual values. The default values are as follows:

> ios::in for ifstream functions meaning open for reading only. ios::out for ofstream functions meaning open for writing only.

The file mode parameter can take one (or more) of such constants defined in the class ios. Table 11.2 lists the file mode parameters and their meanings.

\begin{tabular}{cc}
_Parameter_ & _Meaning_ \\
ios :: app & Append to end-of-file \\
ios :: ate & Go to end-of-file on opening \\
ios :: binary & Binary file \\
ios :: in & Open file for reading only \\
ios :: nocreate & Open fails if the file does not exist \\
ios :: noreplace & Open fails if the file already exists \\
ios :: out & Open file for writing only \\
ios :: trunc & Delete the contents of the file if it exists \\
\end{tabular}