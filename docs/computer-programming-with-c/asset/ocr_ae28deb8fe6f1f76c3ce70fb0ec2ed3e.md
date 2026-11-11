opened using the `ofstream` class, the file will be opened in write only mode, because `ofstream` can only perform output/write operations on the file. The following are the statements to open a file Student.dat in write only mode using an instance of the class `ofstream`, which we have named `fout`:

```
ofstream fout; /* fout is created as an object of class ofstream*/
fout.open("Student.dat"); /*invoke function open (), to open the file Student.dat*/
```

You can also achieve the same effect by opening the file using a constructor as shown:

`ofstream fout ("Student.dat");`

> **How to specify the full directory path explicitly when opening the file?**
> 
> If you want to specify the full location of the file in windows environment you can do so by using the `\\` symbol in the directory path. For example, if the actual path of the file is `C:\Data\Student.dat`, you can specify it as
> 
> ```cpp
> ofstream fout; /* fout is created as an object of class ofstream*/
> fout.open("C:\\Data\\Student.dat"); /*invoke function open (), to open the file Student.dat*/
> ```
> 
> If the file exists on Linux environment at location `/home/Data/Student.dat`, then you can specify it as
> 
> ```cpp
> ofstream fout; /* fout is created as an object of class ofstream*/
> fout.open("/home/Data/Student.dat"); /*invoke function open (), to open the file Student.dat*/
> ```
> 
> We have given the example of `ofstream` object but similar path syntax works for all other objects to access the file at a specific directory location.

Now that we understand how to open a file using `ifstream` and `ofstream` classes, let us understand how to open a file for performing read as well as write operations together. This is possible, because we have a generic class `fstream` that can support opening of the file in read as well as write operations. However, C++ makes it mandatory for the programmer to specify the mode in which the file needs to be opened and if the file is to be opened using the `fstream` class. Different modes in which the file can be opened are specified as flags in the `ios` class as shown in the Table 15.4.

For example, you can invoke a file Employee.dat in read only mode using the class `fstream` as shown below:

```
fstream file;
file.open("Employee.dat", ios::in);
```

Any of the ios modes can be used in combination with the bitwise or the operator. So, if you want to open a file named Student.dat in read as well as write mode, you can invoke the function open as shown below:

```
fstream file;

file.open("Employee.dat", ios::in|ios::out);
```