```
int c;
ifstream in;
ofstream out;
in.open("in.dat");
if (in.fail())
{
    cout << "Input file opening failed.\n";
    exit(1);
}
in >> c;

out.open("out.dat");
if (out.fail())
{
    cout << "Output file opening failed.\n";
    exit(1);
}
out << c;

out.close();
in.close();
```

10. This is the "starting over" the text describes at the beginning of this chapter. The file must be closed and opened again. This action puts the read position at the start of the file, ready to be read again.

11. The two names are the external file name and the stream name. The external file name is the one used by the operating system. It is the real name of the file, but it is used only in the call to the function open, which connects the file to a stream. The stream name is a stream variable (typically of type ifstream or ofstream). After the call to open, your program always uses the stream name as the name of the file.

```
* 123*123*
* 123*123*
```

Each of the spaces contains exactly two blank characters. Notice that a call to width or call to setw only lasts for one output item.

```
* 123*123 * 123*
```

Each of the spaces consists of exactly two blank characters.

```
* 123*123*
* +123*+123*
*123 *123 *
```

There is just one space between the * and the + on the second line. Each of the other spaces contains exactly two blank characters.