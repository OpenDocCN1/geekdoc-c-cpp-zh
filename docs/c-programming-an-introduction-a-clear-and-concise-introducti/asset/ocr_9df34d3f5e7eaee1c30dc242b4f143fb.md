```
```cpp
return 0;
}
```
```

To examine the contents of the file, open a command prompt window and enter the following command (again assuming you are using the same file system structure I am using):

```
```text
type c:\data\grades.txt
```
```

You should see a listing of the grades you entered into the file when you ran the program above. If not, run the program again and enter the type command again.

# Reading Data From a Text File

We discussed reading text from a file in Chapter 8, but we will cover the material again now that you know more about how files and streams work in C++.

The technique for reading data from a file is similar to how we read data from the console and with how we created a text file earlier. We need a file object; we have to associate that object with an input stream, and we read data from the file into a variable.

Instead of creating a file object for output, to read data from a text file we create a file object for input. This means that we have to use the ifstream data type instead of the ofstream data type. The statement needed to open a file for input looks like this:

```
```cpp
ifstream inFile("c:\\data\\grades.txt");
```
```

Next, you need to create a variable to store the data being read. Then you can read the data from the file into the variable, using a statement like this (the variable declaration is included, as well):