The cout statement would print the following output to the screen:

```
10.5
40
556
r
```

No specifiers are required with cin. The >> operator interprets the input value according to the data type of the variable that follows it. The >> operator also discards all white space. For some applications requiring character data, it may not be desirable to discard white space. The member function get can be used with istream objects to get a single character from the input stream. The statements

```
char ch;
cin.get(ch);
```

will read the next character from the keyboard and assign the character to the variable ch. The get function does not discard white space; it treats white space as valid character data.

# Defining File Streams

We have been using cin to read input from the keyboard and cout to print output to the screen. If we want to read values from a file or print information to a file, we must define a file stream object and associate this object with a file.

C++ provides two file stream classes: one for file input and one for file output. The ifstream class is used to define objects that stream input from a file, and the ofstream class is used to define objects that stream output to a file. The ifstream class and the ofstream class are defined in the header file fstream. Declaration statements are used to define ifstream and ofstream objects, as shown in the following statements:

```
ifstream indata; //defines indata as an input file stream object
ofstream outdata; //defines outdata as an output file stream object
```

After a file stream-object has been defined, it must then be associated with a specific file. The member function open is called by the file stream object, and a file name is passed as an argument. Thus, the following statements associate a data file with the objects indata and outdata, respectively:

```
indata.open("sensor1.txt"); //opens the file sensor1 for input
outdata.open("plot1.txt"); //opens the file plot1 for output
```

Now that the objects indata and outdata have been defined and each has been associated with a data file, they can be used for input and output in the same way that cin and cout are used. If we assume that the data file sensor1 holds some experimental data values, we can read one value from the file with the following statement:

```
indata >> x;
```

We can write the value of x, along with the natural log of x and e^x to the output file plot1.txt, with the following statement:

```
outdata << x << " " << log(x) << " " << exp(x) << endl;
```

White space is printed to separate the values.