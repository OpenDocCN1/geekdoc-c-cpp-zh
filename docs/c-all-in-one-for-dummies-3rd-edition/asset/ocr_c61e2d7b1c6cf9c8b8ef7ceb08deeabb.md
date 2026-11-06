# # Finding your files

Whenever you open a new file, you must know where the file is, not just what the file is called. In other words, you need to supply both a path and a filename, not just a filename. You can obtain a path for your file in different ways, depending on your application. For example, you may be saving all your files in a particular directory; you would then precede your filenames with that directory (that is, path) name. The string class makes this easy, as in this code:

```
    const string MyPath = "c:\\
        GreatSoftware";
    string Filename = MyPath + "\\" +
        "MyFile.txt";
    ofstream outfile(Filename.c_str());
```

The reason we had to call `c_str` on the string is that the `ofstream` class doesn't have a constructor for a string instance, only a C-style string. The `c_str` function returns a pointer to a C-style string equivalent of the string. Also, remember to add `#include <string>` when you use the `string` class! Also, when you're using a constant path as we did in this example, you may, instead, store the pathname in some initialization file that lives somewhere on your user's computer, rather than *hard-code* it in your application as we did in this example. You may also include an Options window where your users can change the value of this path.

The short application in Listing 1-1 opens a file called `MyFile.txt`. (The “`./`” part of the file path places the file in the parent directory for the example, which is the Chapter01 folder — see the “Finding your files” sidebar for details.) It does this by creating a new instance of `ofstream`, which is a class for writing to a file. The next line of code writes the string `"Hi!"` to the file. It uses the insertion operator, `<<`, just as `cout` does. In fact, `ofstream` is derived from the very class that `cout` is an instance of, and so that means all the things you can do with `cout` you can also do with your file! Wow! We know we're excited!

When we're finished writing to the file, we close it by calling the `close` member function. This is important!

If you want to open an existing file and append to it, you can modify Listing 1-1 slightly. All you do is change the arguments passed to the constructor as follows:

```
    ofstream outfile("MyFile.txt", ios_base::app);
```

The `ios::app` item is an enumeration inside a class called `ios`, and the `ios_base::app` item is an enumeration in the class called `ios_base`.

The `ios` class is the base class from which the `ofstream` class is derived. The `ios` class also serves as a base class for `ifstream`, which is for reading files.

Book V
Chapter 1
Filing Information with the Streams Library