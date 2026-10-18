is an input-file stream, then the stream is connected to a file before the function is called, so copyLine will not open or close any files.) For example, the first of the following two calls to copyLine will copy a line from the file stuff.dat to the screen, and the second will copy a line from the keyboard to the screen:

```
ifstream fin;
fin.open("stuff.dat");
copyLine(fin);
copyLine(cin);
```

31. Define a function called sendLine that takes one argument that is an output stream. When called, sendLine reads one line of input from the keyboard and outputs the line to the output stream given as its argument. You should be able to call your function using either cout or an output-file stream as the argument to your function sendLine. (If the argument is an output-file stream, then the stream is connected to a file before the function is called, so sendLine will not open or close any files.) For example, the first of the following calls to sendLine copies a line from the keyboard to the file morestuf.dat, and the second copies a line from the keyboard to the screen:

```
ofstream fout;
fout.open("morestuf.dat");
cout << "Enter 2 lines of input:\n";
sendLine(fout);
sendLine(cout);
```

32. (This exercise is for those who have studied the optional section on default arguments.) What output does the following function provide in response to the following calls?

```
void func(double x, double y = 1.1, double z = 2.3)
{
    cout << x << " " << y << " " << z << endl;
}
```

Calls:

+   a. func(2.0);
+   b. func(2.0, 3.0);
+   c. func(2.0, 3.0, 4.0);

33. (This exercise is for those who have studied the optional section on default arguments.) Write several functions that overload the function name to get the same effect as all the calls in the default function arguments in the previous Self-Test Exercise.