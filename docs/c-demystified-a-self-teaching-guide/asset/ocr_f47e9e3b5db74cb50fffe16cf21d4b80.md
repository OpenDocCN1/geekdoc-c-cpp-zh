statements open file in binary mode and append rather than to overwrite. The two file mode flags are combined using the bitwise operator (\|):

```
ofstream outfile;
outfile.open("students.dat", ios::binary ios::app);
```

**Note** The bitwise operator | is not the same as the logical or operator || even though they share the same name or the keystroke |.

While you do not need to specify any file mode flags if you use the *fstream* object to open a file. Whereas an *ofstream* object may only be used to open a file for writing and not reading, an *fstream* object may be used for both purposes. Therefore, you should specify whether you are using the open member function of the *fstream* object to open the file for writing, or both.

The following code fragment uses the open member function of the *fstream* object to open the file for writing only:

```
fstream a;
afile.open("students.dat", ios::out);
```

# The fstream or ofstream Constructor

You may also use the *fstream* or *ofstream* constructor to open a file for writing. A *constructor* is a function that is automatically called when you want to create an instance of an object.

An object instance is akin to a variable of a primitive data type, such as an int. For example, the following statement could be characterized as creating an instance, named age, of an integer:

```
int age;
```

Similarly, the following statement creates an *fstream* instance named *afile*

```
fstream afile;
```

Object constructors can be overloaded, that for the same object there may be a constructor with no arguments, a constructor with one argument, a constructor with two arguments, and so forth. For example, the previous statement, *fstream afile*, is called the no-argument constructor of the *fstream* object.

The following statement calls the no-argument constructor of the *ofstream* object, both creating an *ofstream* instance and opening the file *students.dat* for output:

```
ofstream outFile("students.dat", ios::out);
```

The following statement calls the two-argument constructor of the *fstream* object, both creating an *fstream* instance and opening the file *students.dat* for output:

```
fstream afile("students.dat", ios::out);
```

In essence, an *ofstream* (or *fstream*) variable in one statement and calling the open member function in a second statement is analogous to declaring a primitive variable in one statement and then assigning it a value in a second statement, such as:

```
int age;
age = 39;
```

By contrast, using the one or two argument *ofstream* (or *fstream*) constructor is