You can use the format flags (detailed in the upcoming section), as well as precision and width specifiers, when writing to your files — and also when writing to cout. Because cout is a stream object in the iostream hierarchy, it accepts the same specifiers as output files. So have at it!

![](bbox=[0.141, 0.118, 0.239, 0.189])

# ## Formatting with flags

The folks who made the ISO C++ standard gave us a slew of format flags.

![](bbox=[0.141, 0.284, 0.239, 0.353])

If you're using a compiler that includes a library that’s not fully ANSI-compliant, you will be able to use most of these format flags but not all of them. Therefore, in this section, we’re giving you lists for

+   - ios_base (for ANSI-compliant libraries)
+   - ios (for noncompliant libraries)

To use the following format flags, you call the setf member function for the file object. (This can be either your own file object or the cout object.) For example, to turn on scientific notation, you would do this:

```
```
cout.setf(ios_base::scientific);
cout << 987654.321 << endl;
```
```

or, if you're using a non-ANSI-compliant library:

```
```
cout.setf(ios::scientific);
cout << 987654.321 << endl;
```
```

To turn off scientific mode, you call the unsetf member function:

```
```
cout.unsetf(ios_base::scientific);
cout << 987654.321 << endl;
```
```

or, if you're using a non-ANSI library:

```
```
cout.unsetf(ios::scientific);
cout << 987654.321 << endl;
```
```

And if you’re using your own file, you would do something like this (as found in the FileWrite02 example):

```
```
ofstream myfile("numbers.txt");
myfile.setf(ios_base::scientific);
myfile << 154272.524 << endl;
myfile.close();
```
```

or, for the non-ANSI folks:

```
```
ofstream myfile("numbers.txt");
myfile.setf(ios::scientific);
myfile << 154272.524 << endl;
myfile.close();
```
```