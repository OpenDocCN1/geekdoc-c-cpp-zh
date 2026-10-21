```
file.close();
```

Calling close method ensures all data stored in the buffer related to the file will be written to the disk and all links will be broken. Always make a practice of closing a file when you are done with the file.

# (b) ifstream rdfile;

```
rdfile.open ("demo.txt");
```

This is the second method of opening the file. Here first an object of ifstream class type is created. We then open the file using the open function of the ifstream class.

On the similar ground we can open a file for writing only the ofstream class as :

```
(a) ofstream wrfile("demo.txt");
(b) ofstream wrfile;
wrfile.open("demo.txt");
```

Explanation for the above methods is similar to the explanation as given for the ifstream class. The data can be written to the file as :

```
wrfile<<"hello";
```

The file can be closed as :

```
wrfile.close ();
```

The ifstream and ofstream class are suitable only when we want to read only from file or write only to the file. In situations when we want to perform reading and writing to the same file. There are two ways :

+   - First is to create two separate objects of ifstream and ofstream class. When writing is done, close the file and open the file for reading using an object of ifstream class.
+   - The second method is to create just one object of class fstream class and use as :

```
fstream file;
file.open("demo.txt",ios ::out);
//perform writing operation;
file.close();
file.open("demo.txt",ios ::in);
//perform reading operation;
```

In the open function of fstream class, second argument is the file opening mode. The mode ios ::in is for reading and ios ::out for writing only. The modes are defined as enumeration constants in the class ios so scope resolution operator is used with it. We discuss more modes later in this chapter.

Note that there is no ios ::in or ios ::out default mode for fstream objects. You must specify both modes if your fstream object read and write files. We can also have constructor method of fstream for creating and opening a file as :

```
fstream file("num.txt"ios ::in);
char str[10];
file>>str;
cout<<str<<endl;
```

Let's have some programming examples first then we will see what other modes we can have for handling the files.