Files saved with the .py extension are called modules and can be called individually at the command line or within a program, similar to header files in other languages. If your program is going to import other modules, you will need to make sure they are all saved in the same directory on the computer. More information on working with modules can be found later in this book or in the Python documentation.

Depending on the program, certain arguments can be added to the command line when launching the program. This is similar to adding switches to a Windows DOS prompt command. The arguments tell the program what exactly it should do. For example, perhaps you have a Python program that can output it’s processed data to a file rather than to the screen. To invoke this function in the program you simply launch the program like so:

# Listing 4.8: Launching a Python program with arguments

```
```python
$python foo.py -f
```
```

The “-f” argument is received by the program and calls a function that prints the data to a designated location within the computer’s file system instead of printing it to the screen.

If you have multiple versions of Python installed on your computer, e.g. the system default is version 2.5 but you want to play around with Python 3.x, you simply have to tell the OS which version to use (see Listing 4.9). This is important since many older Python programs aren’t immediately compatible with Python 3.x. In many cases, an older version of Python must be retained on a computer to enable certain programs to run correctly; you don’t want to completely overwrite older Python versions.

# Listing 4.9: Selecting a Python version

```
```python
$python2.5 sample.py    #force use of Python 2.5
$python3.0 sample.py    #force use of Python 3.0
```
```

# 4.6 Integrated Development Environments

I should take the time now to explain more about programming environments. Throughout this book, most of the examples involve using