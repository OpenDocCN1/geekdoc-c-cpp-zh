```
//close all files.
fin.close();
fout.close();
return 0;
}
```

If the data file `sensor.dat` contained the following data,

```
0 45
1 48
2 56
3 -1
4 10
-5 8
-6 -4
6 12
```

The output displayed to standard error, in this case the screen, would be as follows:

```
Bad data encountered on line 4
3 -1
Bad data encountered on line 6
-5 8
Bad data encountered on line 7
-6 -4
```

The file `checkedSensor.dat` would then contain the following data:

```
0 45
1 48
2 56
4 10
6 12
```

# ifstream Class

The `ifstream` class is derived from the `istream` class, thus it inherits all of the functionality of the `istream` class including the input operator and the member functions `eof()`, and `fail()`. Additional member functions required to open and close data files are also provided in the `istream` class.

Each data file used for input in a program must have an `ifstream` object associated with it. A type declaration statement is used to define an object of type `ifstream`, as in

```
ifstream sensori;
```

After an `ifstream` object is defined, it must then be associated with a specific file. The `ifstream` class includes a member function named `open()`. This function is called by the `ifstream` object and a file name is passed as an argument to this function. The file name needs to be a string constant or a C-style string object. Thus, the following statement specifies that the `ifstream` object `sensori` is going to be used with a file named `sensor1.dat` from which we will read information:

```
sensori.open("sensor1.dat");
```