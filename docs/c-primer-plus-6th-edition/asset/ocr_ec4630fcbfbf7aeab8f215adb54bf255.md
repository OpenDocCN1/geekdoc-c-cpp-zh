# File Input and Output 1123

If the ifstream and ofstream constructors and the open() methods take two arguments, how have we gotten by using just one in the previous examples? As you have possibly guessed, the prototypes for these class member functions provide default values for the second argument (the file mode argument). For example, the ifstream open() method and constructor use ios_base::in (for reading) as the default value for the mode argument, and the ofstream open() method and constructor use ios_base::out | ios_base::trunc (for writing and truncate the file) as the default. The bitwise OR | is used to combine two bits into a single value that can be used to set bits. The fstream class does not provide a default mode, so you have to provide a mode explicitly when creating an object of that.

Note that the ios_base::trunc flag means an existing file is truncated when opened to receive program output; that, its previous contents are discarded. This behavior considerably minimizes the danger of running out of disk space, you can possibly imagine situations in which you don't want to open a file when you want it. Of course, C++ provides other options. If, for example, you want to preserve the file contents and add (append) new material to the end of the file, you can use the ios_base::app mode:

```
ofstream fout("bags", ios_base::out | ios_base::app);
```

Again, the code uses | operator to combine modes. So ios_base::out | ios_base::app invokes both the out mode and the app mode (see Figure 17.6). You can find some differences among other C++ implementations. For example, allow you to omit the ios_base::out in the previous example, and some of you don't use the default mode, the safest approach is to provide all the mode elements explicitly. Some compilers don't support all the choices in Table 17.6, and some may choose those in the table. One consequence of these differences is that you may have to make some alterations in the following examples to use on your system. The good news is that the development of the C++ Standard is providing greater uniformity.

Standard C++ defines parts of file I/O in terms of ANSI C standard I/O equivalents. A C++ statement like

```
ifstream fin(filename, cmode);
```

is implemented if it uses the C fopen() function:

```
fopen(filename, cmode);
```

Here c++mode is a type open value, as ios_base::in, and cmode is the corresponding C-mode string, such as "r". Table 17.8 shows the correspondence between C++ modes and C modes. Note that ios_base::out by itself causes truncation but it doesn't cause truncation when combined with ios_base::in. Unlisted combinations, such as ios_base::in | ios_base::trunc, prevent the file from being opened. The is_open() method detects this failure.