```
cout.setf(ios::right);
cout << "*a" << setw(5) << 123 << "*a" << endl;
```

# 10. What output will be produced when the following lines are executed?

```
cout << "*a" << setw(5) << 123 << "*a"
<< 123 << "*a" << endl;
cout.setf(ios::showpos);
cout << "*a" << setw(5) << 123 << "*a"
<< 123 << "*a" << endl;
cout.unsetf(ios::showpos);
cout.setf(ios::left);
cout << "*a" << setw(5) << 123 << "*a"
<< setw(5) << 123 << "*a" << endl;
```

# 11. What output will be sent to the file stuff.txt when the following lines are executed?

```
ofstream fout;
fout.open("stuff.txt");
fout << "*a" << setw(5) << 123 << "*a"
<< 123 << "*a" << endl;
fout.setf(ios::showpos);
fout << "*a" << setw(5) << 123 << "*a"
<< 123 << "*a" << endl;
fout.unsetf(ios::showpos);
fout.setf(ios::left);
fout << "*a" << setw(5) << 123 << "*a"
<< setw(5) << 123 << "*a" << endl;
```

# 12. What output will be produced when the following line is executed (assuming the line is embedded in a complete and correct program with the proper include and using directives)?

```
cout << "*a" << setw(3) << 12345 << "*a" << endl;
```

# Example CLEANING UP A FILE FORMAT

The program in Display 12.7 takes its input from the file rawdata.txt and writes its output, in a neat format, both to the screen and to the file neat.txt. The program copies numbers from the file rawdata.txt to the file neat.txt, but it uses formatting instructions to write them in a neat way. The numbers are written one per line in a field of width 12, which means that each number is preceded by enough blanks so that the blanks plus the number occupy 12 spaces. The numbers are written in ordinary notation; that is, they are not written in e-notation. Each number is written with five digits after the decimal point and with a plus or minus sign. The program uses a function, named makeNeat, that has formal parameters for the input-file stream and the output-file stream.